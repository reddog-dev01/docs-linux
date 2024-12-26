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

### **Tác dụng của ELK**

### **Tại sao phải dùng ELK**

ELK stack đóng vai trò quan trọng trong việc quản lý log, tìm kiếm và phân tích dữ liệu. Nó cho phép các tổ chức quy mô lớn thu thập, lưu trữ, tìm kiếm và phân tích khối lượng dữ liệu log lớn. ELK stack giúp việc khắc phục sự cố, xác định các vấn đề và thu thập thông tin chi tiết về hiệu suất hệ thống. Dưới đây là một số lý do tại sao nó rất quan trọng.

**Phân tích Log và Dữ liệu**
- ELK stack giúp phân tích các dữ liệu log một cách dễ dàng, cho phép nhận diện các vấn đề, hành vi bất thường và các sự kiện quan trọng trong hệ thống.

**Giám sát Thời gian Thực**
- ELK stack cung cấp khả năng giám sát hệ thống và ứng dụng trong thời gian thực, giúp phát hiện các sự cố hoặc vấn đề tiềm ẩn ngay lập tức.

**Bảo mật và Tuân thủ**
- ELK stack có thể được sử dụng để theo dõi và phân tích các sự kiện bảo mật, giúp đảm bảo tuân thủ các quy định và bảo vệ hệ thống khỏi các mối đe dọa.

**Trực quan hóa Dữ liệu**
- ELK stack hỗ trợ việc tạo các biểu đồ và bảng điều khiển (dashboards) trực quan để hiển thị các dữ liệu log và phân tích hệ thống, giúp người dùng dễ dàng nhận diện các mẫu dữ liệu quan trọng.

**Tìm kiếm Toàn văn**
- Với khả năng tìm kiếm toàn văn, ELK stack cho phép người dùng tìm kiếm dữ liệu nhanh chóng và chính xác, ngay cả trong các tập dữ liệu log rất lớn.

**Khả năng Mở Rộng và Hiệu Suất**
- ELK stack có khả năng mở rộng linh hoạt và xử lý khối lượng lớn dữ liệu mà không ảnh hưởng đến hiệu suất, giúp các tổ chức có thể phát triển mà không lo ngại về vấn đề tài nguyên.

**Mã Nguồn Mở và Cộng Đồng Lớn**
- ELK stack là phần mềm mã nguồn mở, với một cộng đồng lớn và năng động luôn hỗ trợ và phát triển các tính năng mới, giúp người dùng dễ dàng triển khai và tùy chỉnh phù hợp với nhu cầu của họ.

### **Cách hoạt động**

![image](https://github.com/user-attachments/assets/fd3cebf8-6a09-4421-a0fd-d3c1f02ea8fa)


### **1. Elasticsearch**
 
Elasticsearch là 1 công cụ tìm kiếm (search engine) và phân tích dữ liệu phân tán mã nguồn mở theo thời gian thực, dùng để lưu trữ và tìm kiếm dữ liệu. Tức là Được xây dựng bằng Java, với giao diện HTTP có hỗ trợ JSON.

#### **1.1 Các thành phần của Elasticsearch** 

![image](https://github.com/user-attachments/assets/f199478b-93de-4c51-9b68-29ff4d7796c8)

##### **Các node được sử dụng trong Elasticsearch**

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

##### **Cluster**

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

#### **Documents**

- Là dữ liệu mà Elasticsearch lưu trữ và tìm kiếm duới dạng cấu trúc JSON.
- Mỗi document thuộc về một index và được xác định duy nhất trong index đó bằng một ID. ID có thể tạo tự động hoặc chỉ định
- Tương tự như 1 hàng trong CSDL.

#### **Index**

- Tập hợp các documents có cấu trúc tương tự nhau.
- Tương tự như 1 bảng trong CSDL.
- Tên của index phải là duy nhất trong cluster.

**Inverted Index (Chỉ mục đảo ngược)** Chỉ mục đảo ngược không lưu trữ trực tiếp các chuỗi mà chia từng tài liệu thành các cụm từ tìm kiếm riêng lẻ. Nhờ đó, người dùng có thể tìm thấy các kết quả phù hợp nhanh chóng, kể cả trong các tệp dữ liệu với khối lượng lớn.

##### **Shard**

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


### **2. Logstash**

#### **Khái niệm**
- Logstash là một công cụ mã nguồn mở giúp thu thập, xử lý và chuyển tiếp dữ liệu từ nhiều nguồn khác nhau trước khi gửi đến Elasticsearch.

#### **Các thành phần của Logstash**

**INPUT** 

- Thu thập dữ liệu từ các nguồn như file, syslog

**FILTER** 

- Nơi xử lý dữ liệu và chuyển tiếp.
- Filter được sử dụng để thực hiện các biến đổi trên dữ liệu. Điều này bao gồm việc phân tích cú pháp, thêm hoặc xóa trường, thay đổi dữ liệu dựa trên điều kiện, đánh dấu dữ liệu (ví dụ, cho việc phân loại), và nhiều tác vụ khác. Một số plugin bộ lọc phổ biến bao gồm grok để phân tích cú pháp văn bản, mutate để thay đổi dữ liệu, và date để phân tích cú pháp và chuyển đổi ngày tháng.

**OUTPUT**

- Gửi dữ liệu đã qua xử lý tới Elasticsearch.

#### **Cách hoạt động**

![image](https://github.com/user-attachments/assets/c6c7bc7e-9b0c-40b7-b57d-f08e38e72a80)

Logstash hoạt động dựa trên mô hình pipeline, trong đó dữ liệu đi qua ba giai đoạn chính: thu thập (input), xử lý (filter), và xuất (output)

**Thu thập Dữ liệu (Input)**

![image](https://github.com/user-attachments/assets/c6400af1-07c9-445b-8fd6-6ff2ee6deddc)


- Logstash bắt đầu quy trình bằng việc thu thập dữ liệu từ các nguồn khác nhau thông qua input plugins. Các nguồn này có thể là file, log, cơ sở dữ liệu, message queues, và nhiều hơn nữa.
- Khi dữ liệu được thu thập, nó được chuyển đến giai đoạn tiếp theo dưới dạng các "events".

**Xử lý Dữ liệu (Filter)**

![image](https://github.com/user-attachments/assets/93288d32-c871-474f-b478-7befea5bc818)

- Các events được xử lý bằng một loạt filter plugins. Mỗi filter có thể được cấu hình để thực hiện nhiệm vụ cụ thể như phân tích cú pháp, làm giàu dữ liệu, thay đổi dữ liệu, hoặc loại bỏ thông tin không cần thiết.
- Các bộ lọc có thể được xếp chồng lên nhau, cho phép một chuỗi các thay đổi phức tạp được áp dụng cho mỗi event.

Xuất Dữ liệu (Output)

![image](https://github.com/user-attachments/assets/18ac93bd-9bde-4260-bea0-5b12e4f611c4)

- Dữ liệu được gửi đến một hoặc nhiều đầu ra thông qua output plugins.
- Logstash có thể định tuyến events đến nhiều đích khác nhau tùy thuộc vào nội dung của chúng. Ví dụ, dữ liệu có thể được gửi đến Elasticsearch, một hệ thống file, một cơ sở dữ liệu, hoặc qua HTTP đến một API.

Trong các giai đoạn thu thập và xuất dữ liệu, Logstash cũng có thể sử dụng codecs để mã hóa hoặc giải mã dữ liệu. Điều này giúp đơn giản hóa việc xử lý các định dạng dữ liệu phức tạp như JSON hoặc các dòng nhật ký đa dạng.

### **3. Kibana**

#### **Khái niệm**

Kibana là một công cụ trực quan hóa dữ liệu mã nguồn mở, hoạt động như giao diện chính cho Elasticsearch. Kibana cho phép người dùng dễ dàng tạo biểu đồ, bảng và các dashboard để phân tích dữ liệu được lưu trữ trong Elasticsearch. Thông qua Kibana, người dùng có thể thực hiện các tìm kiếm và phân tích theo thời gian thực trên dữ liệu, giúp việc giám sát, báo cáo và quản lý dữ liệu trở nên hiệu quả hơn

#### **Cách hoạt động của Kibana**

- Kết nối với Elasticsearch: Khi người dùng thực hiện truy vấn, Kibana gửi yêu cầu đến Elasticsearch để lấy dữ liệu cần thiết.
- Trực quan hóa dữ liệu: Sau khi nhận được dữ liệu từ Elasticsearch, Kibana cho phép người dùng tạo ra nhiều loại biểu đồ khác nhau như biểu đồ cột, biểu đồ đường, biểu đồ tròn và bản đồ nhiệt.
- Bảng điều khiển (Dashboard): Tạo bảng điều khiển tùy chỉnh để tổ chức các biểu đồ và báo cáo, chia sẻ với những người khác qua trình duyệt.
- Tính năng lọc và tìm kiếm: Kibana hỗ trợ các bộ lọc mạnh mẽ, cho phép người dùng dễ dàng tìm kiếm và phân tích dữ liệu theo các tiêu chí cụ thể.
- Hỗ trợ không gian địa lý: Với khả năng tích hợp thông tin địa lý, Kibana cho phép người dùng hiển thị dữ liệu trên bản đồ, hỗ trợ phân tích.

#### **Các chức năng quan trọng của Kibana**

**Discover** 
- Cho phép người dùng tìm kiếm và lọc dữ liệu từ các chỉ mục Elasticsearch nhanh chóng và hiệu quả.
- Người dùng có thể thực hiện tìm kiếm toàn văn trên dữ liệu, lọc kết quả bằng cách sử dụng các truy vấn KQL, xem chi tiết các trường dữ liệu.

**Visualize**
- Tận dụng sức mạnh của dữ liệu bằng cách tạo ra nhiều loại biểu đồ, bảng biểu và hình thức trực quan khác nhau.
- Linh hoạt trong việc lựa chọn kiểu hiển thị dữ liệu. Dễ dàng lựa chọn hình thức phù hợp nhất để diễn đạt ý nghĩa của dữ liệu đang phân tích.
- Khả năng tùy chỉnh từng yếu tố của trực quan hóa, từ màu sắc, đến kích thước và loại hình.

**Dashboard** 
- Kết hợp nhiều trực quan hóa thành một giao diện tổng quát, giúp dễ dàng theo dõi và phân tích. 
- Cho phép người dùng có cái nhìn tổng quát, từ đó nhanh chóng phát hiện các xu hướng hoặc mẫu hình nổi bật.
- Cung cấp khả năng tùy chỉnh cao, người dùng có thể điều chỉnh dữ liệu hiển thị, từ việc thay đổi phạm vi thời gian đến việc tùy chỉnh các bộ lọc.

**Canvas**
- Cho phép người dùng tạo ra các báo cáo và bản trình bày với thiết kế nghệ thuật
- Người dùng có thể kéo thả các thành phần, thêm văn bản, hình ảnh và kết nối với dữ liệu để tạo ra sản phẩm có các thông tin cần thiết và đẹp mắt.

**Machine Learning**
- Hỗ trợ người dùng phát hiện ra các vấn đề tiềm ẩn nhanh chóng mà đôi khi con người khó nhận ra.
- Định dạng và phát hiện các mẫu trưởng đột biến, xu hướng giảm giá trị, hay các trường hợp ngoại lệ.

### **4. Beats**

#### **Beats là gì?**

Là công cụ mã nguồn mở dùng để thu thập và gửi dữ liệu trực tiếp đến Elasticsearch hoặc qua Logstash.

- Filebeat: Thu thập và gửi các tệp nhật ký (log files).
- Metricbeat: Thu thập và gửi các chỉ số hệ thống (metrics), chẳng hạn như CPU, bộ nhớ, lưu lượng mạng, v.v.
- Packetbeat: Thu thập và gửi dữ liệu mạng (network data).
- Auditbeat: Thu thập và gửi thông tin liên quan đến bảo mật và hoạt động hệ thống (security and system activity).
- Winlogbeat: Thu thập và gửi các sự kiện từ nhật ký của Windows (Windows event logs).
