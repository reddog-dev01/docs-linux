### 1. **Giao thức định tuyến là gì?**
Giao thức định tuyến (Routing Protocol) là một tập hợp các quy tắc và phương pháp mà các router (hoặc thiết bị mạng) sử dụng để trao đổi thông tin và xác định con đường (định tuyến) tối ưu cho dữ liệu từ nguồn đến đích trong mạng. Mỗi giao thức định tuyến có một cách thức riêng để tính toán và chia sẻ thông tin về các tuyến đường có sẵn trong mạng.

### 2. **Tại sao cần giao thức định tuyến?**
Giao thức định tuyến là cần thiết vì:
- **Quản lý lưu lượng mạng**: Các giao thức giúp các router quyết định con đường tối ưu để chuyển tiếp các gói dữ liệu, từ đó giảm độ trễ và đảm bảo hiệu suất mạng tốt.
- **Khả năng phục hồi**: Khi có sự cố mạng (như một liên kết bị hỏng), giao thức định tuyến giúp tìm ra các con đường thay thế để duy trì hoạt động mạng.
- **Khả năng mở rộng**: Giao thức định tuyến cho phép các mạng lớn và phức tạp có thể dễ dàng mở rộng mà không cần phải cấu hình thủ công cho từng router.
- **Tự động hoá**: Các giao thức định tuyến động giúp tự động cập nhật bảng định tuyến khi có sự thay đổi trong cấu trúc mạng, giảm thiểu công việc quản trị viên hệ thống.

### 3. **Các loại giao thức định tuyến**

#### 3.1 **Định tuyến tĩnh (Static Routing)**
- **Định nghĩa**: Là phương pháp cấu hình các tuyến đường một cách thủ công trong bảng định tuyến của router. Các tuyến đường này không thay đổi trừ khi quản trị viên thay đổi cấu hình.
- **Ưu điểm**: 
  - Đơn giản và dễ quản lý cho các mạng nhỏ hoặc không thay đổi.
  - Ít tốn tài nguyên hệ thống.
- **Nhược điểm**: 
  - Không linh hoạt, nếu có sự thay đổi về mạng hoặc liên kết bị hỏng, cần phải thay đổi thủ công cấu hình.
  - Không tự động cập nhật khi có sự thay đổi trong mạng.

#### 3.2 **Định tuyến động (Dynamic Routing)**
Định tuyến động sử dụng các giao thức để tự động học hỏi và cập nhật các tuyến đường trong bảng định tuyến của router. Các giao thức này giúp router tự động chia sẻ và đồng bộ thông tin định tuyến với các router khác trong mạng.

Các giao thức định tuyến động được chia thành 3 loại chính:

##### **A. Giao thức định tuyến dựa trên khoảng cách (Distance-Vector Protocols)**

- **Đặc điểm**: Các router sử dụng khoảng cách (số bước nhảy) và hướng (điểm tới đích) để xác định tuyến đường. Các router thông báo thông tin định tuyến của mình cho các router lân cận.
- **Ví dụ**:
  - **RIP (Routing Information Protocol)**: Đây là một trong những giao thức định tuyến lâu đời nhất, sử dụng số bước nhảy (hop count) làm chỉ số để chọn con đường. RIP giới hạn số bước nhảy tối đa là 15, làm cho nó phù hợp với các mạng nhỏ.
  - **IGRP (Interior Gateway Routing Protocol)**: Giao thức của Cisco, có thể sử dụng các yếu tố như băng thông, độ trễ để tính toán tuyến đường tối ưu.

##### **B. Giao thức định tuyến dựa trên liên kết trạng thái (Link-State Protocols)**

- **Đặc điểm**: Mỗi router trong mạng duy trì bản đồ mạng đầy đủ và sử dụng các thuật toán để tính toán tuyến đường tối ưu. Thông tin trạng thái liên kết (link state) được chia sẻ giữa các router để cập nhật bảng định tuyến.
- **Ví dụ**:
  - **OSPF (Open Shortest Path First)**: Giao thức định tuyến phổ biến trong các mạng lớn, sử dụng thuật toán Dijkstra để tính toán đường đi ngắn nhất. OSPF chia mạng thành các khu vực (area) để giảm thiểu kích thước bảng định tuyến.
  - **IS-IS (Intermediate System to Intermediate System)**: Tương tự OSPF, nhưng chủ yếu được sử dụng trong các mạng của nhà cung cấp dịch vụ và không dựa trên IP.

##### **C. Giao thức định tuyến hỗn hợp (Hybrid Routing Protocols)**

- **Đặc điểm**: Kết hợp giữa các yếu tố của cả giao thức định tuyến dựa trên khoảng cách và trạng thái liên kết. Các giao thức này thường sử dụng một số loại thông tin để xác định đường đi, giúp tối ưu hóa việc tính toán và khả năng mở rộng.
- **Ví dụ**:
  - **EIGRP (Enhanced Interior Gateway Routing Protocol)**: Là một giao thức của Cisco, kết hợp các yếu tố của cả định tuyến dựa trên khoảng cách và liên kết trạng thái. Nó hỗ trợ các tính toán phức tạp hơn và cho phép tính toán nhanh hơn so với RIP.

#### 3.3 **Giao thức định tuyến ngoài (Exterior Gateway Protocols)**

- **Đặc điểm**: Được sử dụng để định tuyến giữa các hệ thống tự trị khác nhau, ví dụ như giữa các tổ chức hoặc nhà cung cấp dịch vụ Internet (ISP).
- **Ví dụ**:
  - **BGP (Border Gateway Protocol)**: Giao thức định tuyến ngoài phổ biến nhất, sử dụng thông tin đường đi và các chính sách định tuyến để chia sẻ thông tin giữa các hệ thống tự trị. BGP giúp xác định các tuyến đường giữa các mạng khác nhau, chủ yếu được sử dụng trong các mạng toàn cầu như Internet.

### 4. **Kết luận**
Các giao thức định tuyến giúp mạng máy tính có thể tối ưu hóa việc truyền tải dữ liệu và duy trì sự ổn định của hệ thống mạng. Chúng được chia thành các loại cơ bản như định tuyến tĩnh và định tuyến động, với nhiều giao thức khác nhau phù hợp với từng mục đích và môi trường mạng. Trong khi định tuyến tĩnh thích hợp với mạng nhỏ và không thay đổi, định tuyến động lại rất hữu ích trong các mạng lớn và phức tạp, nơi các router cần tự động cập nhật và chia sẻ thông tin để duy trì sự linh hoạt và hiệu quả.
