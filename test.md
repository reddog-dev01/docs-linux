### Giao thức định tuyến là gì?

**Giao thức định tuyến** (Routing Protocol) là một tập hợp các quy tắc, quy trình và phương pháp mà các router hoặc thiết bị mạng sử dụng để quyết định con đường tối ưu (tuyến đường) để chuyển tiếp các gói tin từ nguồn đến đích trong mạng máy tính. Các giao thức này cho phép các router trao đổi thông tin về các tuyến đường khả dụng, từ đó cập nhật và duy trì bảng định tuyến của mình để đảm bảo dữ liệu được gửi đến đúng đích qua con đường tối ưu.

### 1. **Tại sao cần giao thức định tuyến?**

Giao thức định tuyến là yếu tố quan trọng trong việc vận hành mạng, đặc biệt là các mạng lớn và phức tạp. Các router trong mạng không thể hoạt động hiệu quả nếu không có thông tin về cách xác định các tuyến đường, thông tin này thường được chia sẻ thông qua các giao thức định tuyến. 

#### Lý do cần giao thức định tuyến:
- **Tối ưu hóa lưu lượng mạng**: Giao thức định tuyến giúp các router chọn lựa con đường tối ưu cho việc chuyển tiếp gói tin, từ đó giảm độ trễ và tăng hiệu suất mạng.
- **Khả năng phục hồi và chịu lỗi**: Khi một liên kết mạng bị hỏng, giao thức định tuyến có thể giúp tìm ra con đường thay thế để đảm bảo sự tiếp tục của việc truyền tải dữ liệu.
- **Quản lý mạng động**: Mạng máy tính không phải lúc nào cũng có cấu trúc cố định. Giao thức định tuyến giúp mạng thích nghi với sự thay đổi của cấu trúc mạng, thêm hoặc bớt các router, liên kết mới mà không cần cấu hình thủ công.
- **Khả năng mở rộng**: Khi mạng phát triển lớn hơn, các giao thức định tuyến giúp quản lý các tuyến đường và duy trì hiệu suất mạng mà không cần điều chỉnh thủ công.
  
### 2. **Các loại giao thức định tuyến**

Có hai loại giao thức định tuyến chính: **Định tuyến tĩnh** và **Định tuyến động**.

#### 2.1 **Định tuyến tĩnh (Static Routing)**
- **Đặc điểm**: Các tuyến đường trong bảng định tuyến được cấu hình thủ công bởi người quản trị hệ thống. Các tuyến đường này không thay đổi trừ khi quản trị viên thay đổi cấu hình.
- **Ưu điểm**: 
  - Đơn giản, dễ kiểm soát và không yêu cầu tài nguyên hệ thống nhiều.
  - Dễ dàng kiểm soát lưu lượng mạng trong các mạng nhỏ.
- **Nhược điểm**:
  - Không linh hoạt, khi có sự thay đổi trong mạng, cần phải thay đổi cấu hình thủ công.
  - Không tự động phục hồi khi một liên kết bị hỏng.

#### 2.2 **Định tuyến động (Dynamic Routing)**
Định tuyến động là phương pháp mà các router sử dụng giao thức định tuyến để tự động trao đổi thông tin và xác định các tuyến đường tối ưu. Các giao thức định tuyến động chia sẻ thông tin giữa các router, giúp tự động cập nhật bảng định tuyến.

##### **Các loại giao thức định tuyến động:**

##### **A. Giao thức định tuyến dựa trên khoảng cách (Distance-Vector Routing Protocols)**
- **Đặc điểm**: Các router sử dụng khoảng cách (số bước nhảy) và hướng (điểm tới đích) để quyết định tuyến đường. Các router trao đổi thông tin định tuyến với nhau định kỳ.
- **Ví dụ**:
  - **RIP (Routing Information Protocol)**: Sử dụng số bước nhảy (hop count) làm chỉ số để tính toán và chọn tuyến đường tối ưu. RIP có thể quản lý mạng có quy mô nhỏ và trung bình, nhưng có giới hạn tối đa 15 bước nhảy, khiến nó không phù hợp với các mạng quá lớn.
  - **IGRP (Interior Gateway Routing Protocol)**: Giao thức của Cisco, sử dụng các yếu tố như băng thông, độ trễ, độ tin cậy, và tải để tính toán tuyến đường tối ưu.

##### **B. Giao thức định tuyến dựa trên trạng thái liên kết (Link-State Routing Protocols)**
- **Đặc điểm**: Các router duy trì một bản đồ toàn bộ mạng và sử dụng thuật toán để tính toán con đường tốt nhất đến đích. Thông tin trạng thái liên kết (link-state) được chia sẻ giữa các router, giúp mỗi router có một cái nhìn tổng quan về cấu trúc mạng.
- **Ví dụ**:
  - **OSPF (Open Shortest Path First)**: Là giao thức định tuyến phổ biến trong các mạng lớn, sử dụng thuật toán Dijkstra để tính toán đường đi ngắn nhất. OSPF chia mạng thành các khu vực (area), giúp giảm thiểu kích thước bảng định tuyến và tăng tính hiệu quả.
  - **IS-IS (Intermediate System to Intermediate System)**: Một giao thức định tuyến khác sử dụng thuật toán trạng thái liên kết, nhưng chủ yếu được sử dụng trong các mạng của nhà cung cấp dịch vụ Internet.

##### **C. Giao thức định tuyến hỗn hợp (Hybrid Routing Protocols)**
- **Đặc điểm**: Kết hợp giữa các yếu tố của cả hai giao thức dựa trên khoảng cách và trạng thái liên kết. Mục đích là kết hợp ưu điểm của cả hai, giúp mạng vừa linh hoạt vừa tối ưu hóa.
- **Ví dụ**:
  - **EIGRP (Enhanced Interior Gateway Routing Protocol)**: Một giao thức của Cisco, kết hợp các yếu tố của định tuyến khoảng cách và trạng thái liên kết. EIGRP tính toán đường đi ngắn nhất dựa trên các yếu tố như băng thông, độ trễ và tải.

##### **D. Giao thức định tuyến ngoài (Exterior Gateway Protocols)**
- **Đặc điểm**: Được sử dụng để định tuyến giữa các hệ thống tự trị (AS) khác nhau, ví dụ như giữa các tổ chức hoặc các nhà cung cấp dịch vụ Internet (ISP).
- **Ví dụ**:
  - **BGP (Border Gateway Protocol)**: Giao thức định tuyến ngoài phổ biến nhất, BGP được sử dụng để chia sẻ thông tin giữa các hệ thống tự trị trong mạng Internet. BGP không sử dụng chỉ số khoảng cách mà thay vào đó dựa vào các chính sách định tuyến để xác định tuyến đường.

### 3. **Thuật toán trong giao thức định tuyến**

Các giao thức định tuyến thường sử dụng các thuật toán để tính toán và xác định tuyến đường tối ưu. Một số thuật toán phổ biến bao gồm:

- **Thuật toán Dijkstra**: Được sử dụng trong giao thức OSPF để tính toán đường đi ngắn nhất.
- **Thuật toán Bellman-Ford**: Được sử dụng trong các giao thức như RIP và IGRP để tính toán tuyến đường ngắn nhất.
- **Thuật toán SPF (Shortest Path First)**: Thuật toán của OSPF, là một dạng thuật toán Dijkstra.

### 4. **Tóm tắt các loại giao thức định tuyến**
- **Định tuyến tĩnh**: Cấu hình thủ công, không linh hoạt, thích hợp cho các mạng nhỏ và ổn định.
- **Định tuyến động**:
  - **Distance-Vector**: Dựa vào khoảng cách và chia sẻ thông tin định kỳ (RIP, IGRP).
  - **Link-State**: Dựa vào trạng thái liên kết, mỗi router có cái nhìn tổng quan về mạng (OSPF, IS-IS).
  - **Hybrid**: Kết hợp các yếu tố của Distance-Vector và Link-State (EIGRP).
- **Định tuyến ngoài**: Dùng để định tuyến giữa các hệ thống tự trị khác nhau (BGP).

### 5. **Kết luận**
Giao thức định tuyến là thành phần cốt lõi của mạng máy tính, giúp đảm bảo rằng các gói tin được chuyển tiếp hiệu quả từ nguồn đến đích. Chúng có thể được chia thành các loại khác nhau tùy thuộc vào cách thức hoạt động, bao gồm định tuyến tĩnh và định tuyến động, với các giao thức như RIP, OSPF, EIGRP, và BGP cung cấp các giải pháp cho các mạng có quy mô và độ phức tạp khác nhau.
