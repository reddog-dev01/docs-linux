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

**Các node được sử dụng trong Elasticsearch**

1 node là 1 phiên bản của Elasticsearch chạy trên 1 máy chủ. Mỗi node có thể được cấu hình để thực hiện các vai trò cụ thể của từ cluster như lưu trữ dữ liệu, xử lý truy vấn, quản lý cluster.

**a. Master node**
- Chịu trách nhiệm quản lý cluster như tạo hoặc xóa index (chỉ mục). Theo dõi node nào là của cluster và quyết định phân bổ shards cho node.
- Chỉ có một master node hoạt động tại một thời điểm, nhưng có thể có nhiều node đủ điều kiện để trở thành master để đảm bảo tính sẵn sàng và độ tin cậy. Chọn master node bằng cách bầu chọn dựa trên thuật toán Zen Discovery nếu 1 node được đa số phiếu bầu thì sẽ thành master node. Chỉ những node được cấu hình với node.master: true (để false nó sẽ không được tham gia) mới có thể tham gia vào quá trình bầu chọn master node. Các node này được gọi là master-eligible nodes.
 
**b. Data node**

- Chịu trách nhiệm lưu trữ và quản lý dữ liệu trong luster.
- Khi dữ liệu mới được thêm vào Elasticsearch, nó được lập chỉ mục tại các data nodes. Các data nodes quản lý các dữ liệu được đánh chỉ mục, tìm kiếm, tổng hợp dữ liệu.
- Data nodes chứa các shards thực tế (cả primary và replica shards) của các chỉ mục trong Elasticsearch để tăng khả năng chịu lỗi. Dữ liệu được lập chỉ mục và lưu trữ dưới dạng JSON trong các shards này.
- Khi một truy vấn được thực hiện, truy vấn đó được gửi đến các data nodes chứa các shards liên quan. Mỗi data node xử lý truy vấn đối với shards mà nó đang giữ và sau đó gửi kết quả truy vấn về coordinating nodes.

**c. Ingest node**

- Ingest node được sử dụng để xử lý dữ liệu documents trước khi được lập chỉ mục vào các data nodes.

**d. Coordinating-only node**

- 

