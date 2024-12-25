mô hình log ELK
- Nó là gì? Làm gì? Làm như thế nào?
- Chức năng nhiệm vụ của từng thành phần
- Mô hình kết nối
- Các vấn đề cần lưu ý khi xây dựng hệ thống này
- Dựng cụm lab để setup được mô hình trên

### **ELK là gì?**

Là từ viết tắt của bộ công cụ bao gồm 3 dự án Elasticsearch, Logstash, Kibana. Sử dụng cùng với nhau để 

![image](https://github.com/user-attachments/assets/26eae5a0-9d4c-494a-ace9-d80bb9a272cf)

Được sử dụng để tổng hợp nhật ký từ tất cả các hệ thống và ứng dụng, phân tích chúng và tạo trực quan hóa dữ liệu để giám sát, xử lý sự cố nhanh hơn, phân tích bảo mật...

#### **1 Elasticsearch**
 
Elasticsearch là 1 công cụ tìm kiếm (search engine) và phân tích phân tán mã nguồn mở theo thời gian thực, dùng để lưu trữ và tìm kiếm dữ liệu. Tức là Được xây dựng bằng Java, với giao diện HTTP có hỗ trợ JSON.

##### **1.1 Các thành phần của Elasticsearch** 

![image](https://github.com/user-attachments/assets/f199478b-93de-4c51-9b68-29ff4d7796c8)

###### **Các node được sử dụng trong Elasticsearch**

1 node là 1 phiên bản của Elasticsearch chạy trên 1 máy chủ. Mỗi node có thể được cấu hình để thực hiện các vai trò cụ thể của từ cluster như lưu trữ dữ liệu, xử lý truy vấn, quản lý cluster.

**a. Master node**
- Chịu trách nhiệm quản lý cluster như tạo hoặc xóa index (chỉ mục). Theo dõi node nào là của cluster và quyết định phân bổ shards cho node.
- Chỉ có một master node hoạt động tại một thời điểm, nhưng có thể có nhiều node đủ điều kiện để trở thành master (được cấu hình true) để đảm bảo tính sẵn sàng và độ tin cậy. Chọn master node bằng cách bầu chọn dựa trên thuật toán Zen Discovery nếu 1 node được đa số phiếu bầu thì sẽ thành master node. Chỉ những node được cấu hình với node.master: true (để false nó sẽ không được tham gia) mới có thể tham gia vào quá trình bầu chọn master node. Các node này được gọi là master-eligible nodes.
 
**b. Data node**

- Chịu trách nhiệm lưu trữ và quản lý dữ liệu trong luster.
- Khi dữ liệu mới được thêm vào Elasticsearch, nó được lập chỉ mục tại các data nodes. Các data nodes quản lý các dữ liệu được đánh chỉ mục, tìm kiếm, tổng hợp dữ liệu.
- Data nodes chứa các shards thực tế (cả primary và replica shards) của các chỉ mục trong Elasticsearch để tăng khả năng chịu lỗi. Dữ liệu được lập chỉ mục và lưu trữ dưới dạng JSON trong các shards này.
- Khi một truy vấn được thực hiện, truy vấn đó được gửi đến các data nodes chứa các shards liên quan. Mỗi data node xử lý truy vấn đối với shards mà nó đang giữ và sau đó gửi kết quả truy vấn về coordinating nodes.

**c. Ingest node**

- Ingest node được sử dụng để xử lý dữ liệu documents trước khi được lập chỉ mục vào các data nodes như là chuyển đổi định dạng, xóa sửa  dữ liệu.
- Phải được định dạng phù hợp với mapping đã được thiết lập cho chỉ mục.
- Ingest nodes có thể sửa đổi hoặc bổ sung dữ liệu để đảm bảo sự đồng nhất, giảm thiểu lỗi trong quá trình lập chỉ mục.

**d. Coordinating-only node (client node)**

- Chịu trách nhiệm định tuyến các yêu cầu đến các node master hoặc node dữ liệu. Hoạt động như load balancers.
- Tổng hợp kết quả từ các data node. Tức là khi truy vấn yêu cầu dữ liệu từ nhiều shard, coordinating node chịu trách nhiệm tổng hợp kết quả trước khi trả về cho client
- Phân phối các yêu cầu từ client đến các node master hoặc data thích hợp.

###### **Cluster**

**Cluster** là tập hợp các node hoạt động cùng với nhau. 

- Tên của 1 Cluster là duy nhất
- Mỗi node trong cluster có 1 ID duy nhất.

**Đặc điểm**

a. Khả năng mở rộng (Scalability):
-  Cluster có thể mở rộng bằng cách thêm nhiều node để tăng dung lượng lưu trữ hoặc hiệu suất xử lý.

b. Tính chịu lỗi (Fault Tolerance):
- Nếu một node bị lỗi, cluster vẫn tiếp tục hoạt động nhờ các shard replica được lưu trữ trên các node khác.

c. Phân tán (Distributed):
- Cluster phân tán dữ liệu và tác vụ tìm kiếm, giúp xử lý song song và cải thiện tốc độ.

##### **Documents**

- Là dữ liệu mà Elasticsearch lưu trữ và tìm kiếm duới dạng cấu trúc JSON.
- Mỗi document thuộc về một index và được xác định duy nhất trong index đó bằng một ID. ID có thể tạo tự động hoặc chỉ định
- Tương tự như 1 hàng trong CSDL.

##### **Index**

- Tập hợp các documents có cấu trúc tương tự nhau.
- Tương tự như 1 bảng trong CSDL.
- Tên của index phải là duy nhất trong cluster.

**Inverted Index (Chỉ mục đảo ngược)** Chỉ mục đảo ngược không lưu trữ trực tiếp các chuỗi mà chia từng tài liệu thành các cụm từ tìm kiếm riêng lẻ. Nhờ đó, người dùng có thể tìm thấy các kết quả phù hợp nhanh chóng, kể cả trong các tệp dữ liệu với khối lượng lớn.

###### **Shard**

- Lưu trữ các documents của index.
- Elasticsearch tự động chia dữ liệu của index đó thành các shard.

- Phân tán dữ liệu: Shard giúp chia nhỏ dữ liệu của một index để lưu trữ trên nhiều node trong cluster, từ đó cải thiện khả năng mở rộng.
- Xử lý song song: Nhờ việc chia nhỏ dữ liệu, Elasticsearch có thể xử lý truy vấn trên nhiều shard cùng lúc, giảm thời gian phản hồi.
- Chịu lỗi: Replica shard (bản sao) đảm bảo rằng dữ liệu vẫn có sẵn nếu một shard chính bị lỗi.

a. Primary Shard (Shard chính):
- Là nơi lưu trữ dữ liệu gốc của index.
- Mỗi index có một số lượng primary shard được xác định khi tạo index và không thể thay đổi sau đó.
- Khi dữ liệu được ghi vào index, nó sẽ được lưu vào một primary shard.
b. Replica Shard (Shard bản sao):
- Là bản sao của một primary shard.
- Replica shard không chỉ đóng vai trò dự phòng mà còn có thể xử lý các truy vấn đọc, cải thiện hiệu năng.
- Số lượng replica shard có thể được thay đổi linh hoạt sau khi index được tạo.

![image](https://github.com/user-attachments/assets/4117df73-bb50-4a60-b809-c2e2bf724b73)

