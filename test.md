### **Tầng Liên Kết Dữ Liệu (Link Layer) trong Mô Hình TCP/IP**

Tầng **Liên Kết Dữ Liệu** (Data Link Layer) trong mô hình **TCP/IP** là tầng thứ hai và nằm dưới **Tầng Mạng** (Internet Layer). Nó đóng vai trò quan trọng trong việc xử lý dữ liệu truyền giữa các thiết bị trong cùng một mạng cục bộ (LAN) hoặc giữa các thiết bị trực tiếp kết nối với nhau.

Tầng Liên Kết Dữ Liệu chịu trách nhiệm đảm bảo rằng dữ liệu có thể được truyền tải chính xác qua phương tiện vật lý (như cáp đồng, cáp quang, sóng radio), và nó cung cấp các cơ chế để kiểm soát lỗi và truyền thông giữa các thiết bị trong mạng cục bộ.

### **Chức Năng Chính của Tầng Liên Kết Dữ Liệu**

1. **Đóng gói và định dạng dữ liệu (Framing)**:
   - Tầng Liên Kết Dữ Liệu sẽ đóng gói dữ liệu từ Tầng Mạng thành các **frame** (khung dữ liệu). Mỗi frame chứa địa chỉ MAC (Media Access Control) của thiết bị nguồn và thiết bị đích, và cũng có thể chứa thông tin kiểm tra lỗi (checksum).
   - Mỗi frame này sẽ được gửi qua phương tiện truyền dẫn (như cáp Ethernet hoặc sóng Wi-Fi).

2. **Địa chỉ MAC (Media Access Control)**:
   - Tầng này sử dụng **địa chỉ MAC** để xác định các thiết bị trong mạng LAN. Địa chỉ MAC là một địa chỉ vật lý duy nhất cho mỗi thiết bị mạng (ví dụ: card mạng của máy tính).
   - Địa chỉ MAC giúp các thiết bị xác định và giao tiếp với nhau trong mạng cục bộ.

3. **Kiểm tra lỗi (Error Detection and Correction)**:
   - Tầng Liên Kết Dữ Liệu cung cấp cơ chế để kiểm tra và phát hiện lỗi trong quá trình truyền tải dữ liệu.
   - Các phương pháp phổ biến để kiểm tra lỗi bao gồm **CRC (Cyclic Redundancy Check)**, được sử dụng để xác định liệu dữ liệu có bị thay đổi hoặc mất mát trong quá trình truyền.

4. **Kiểm soát luồng (Flow Control)**:
   - Tầng Liên Kết Dữ Liệu có thể thực hiện một số cơ chế kiểm soát luồng, đảm bảo rằng dữ liệu không bị truyền quá nhanh mà không được nhận kịp thời.
   - Điều này giúp tránh việc mất dữ liệu do quá tải hoặc truyền tải quá nhanh trong các mạng có băng thông hạn chế.

5. **Điều khiển truy cập phương tiện (Media Access Control)**:
   - Tầng Liên Kết Dữ Liệu xác định cách thức các thiết bị trong mạng LAN sẽ truy cập phương tiện truyền dẫn và tránh xung đột khi nhiều thiết bị muốn truyền dữ liệu cùng lúc.
   - Một trong những giao thức phổ biến cho điều khiển truy cập phương tiện là **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)**, thường được sử dụng trong mạng Ethernet.

### **Cấu Trúc Frame trong Tầng Liên Kết Dữ Liệu**

Một **frame** trong Tầng Liên Kết Dữ Liệu có thể bao gồm các thành phần chính sau:

1. **Địa chỉ MAC nguồn**: Địa chỉ MAC của thiết bị gửi.
2. **Địa chỉ MAC đích**: Địa chỉ MAC của thiết bị nhận.
3. **Dữ liệu**: Phần dữ liệu từ các tầng trên (Tầng Mạng).
4. **Thông tin kiểm tra lỗi (CRC)**: Dùng để phát hiện lỗi trong quá trình truyền tải dữ liệu.

### **Các Giao Thức trong Tầng Liên Kết Dữ Liệu**

1. **Ethernet**:
   - **Ethernet** là một giao thức phổ biến trong mạng LAN sử dụng **địa chỉ MAC** để định tuyến các frame giữa các thiết bị trong mạng.
   - Ethernet sử dụng **CSMA/CD** để kiểm soát việc truy cập vào phương tiện truyền dẫn. Nếu hai thiết bị gửi tín hiệu đồng thời, sẽ xảy ra xung đột, và hệ thống sẽ yêu cầu các thiết bị chờ một khoảng thời gian ngẫu nhiên trước khi thử lại.

2. **Wi-Fi (Wireless LAN)**:
   - **Wi-Fi** sử dụng giao thức **IEEE 802.11** và cũng dựa vào địa chỉ MAC để truyền dữ liệu không dây giữa các thiết bị.
   - Tương tự như Ethernet, Wi-Fi cũng có cơ chế **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) để tránh xung đột khi truyền tín hiệu trong môi trường không dây.

3. **PPP (Point-to-Point Protocol)**:
   - **PPP** được sử dụng trong các kết nối điểm-điểm (point-to-point) như kết nối dial-up, kết nối qua cáp, hoặc kết nối VPN.
   - PPP cung cấp tính năng xác thực, mã hóa, và nén dữ liệu, giúp tạo ra một kết nối đáng tin cậy giữa hai thiết bị.

4. **ARP (Address Resolution Protocol)**:
   - **ARP** giúp ánh xạ giữa địa chỉ IP và địa chỉ MAC trong một mạng LAN. Khi một thiết bị biết địa chỉ IP nhưng không biết địa chỉ MAC của thiết bị đích, nó sẽ gửi yêu cầu ARP để tìm địa chỉ MAC tương ứng.
   
5. **HDLC (High-Level Data Link Control)**:
   - **HDLC** là một giao thức điều khiển liên kết dữ liệu được sử dụng trong mạng LAN, WAN, và các kết nối điểm-điểm. HDLC cung cấp các cơ chế để truyền dữ liệu một cách đáng tin cậy với kiểm tra lỗi và kiểm soát luồng.

### **Quá Trình Hoạt Động của Tầng Liên Kết Dữ Liệu**

1. **Tạo frame**:
   - Khi nhận dữ liệu từ Tầng Mạng, Tầng Liên Kết Dữ Liệu sẽ đóng gói dữ liệu này vào các frame, thêm địa chỉ MAC của thiết bị nguồn và đích, và mã kiểm tra lỗi.
   
2. **Truyền frame qua phương tiện truyền dẫn**:
   - Các frame được truyền qua phương tiện vật lý (cáp Ethernet, sóng Wi-Fi, v.v.) tới thiết bị đích.

3. **Nhận và kiểm tra lỗi**:
   - Khi một thiết bị nhận được frame, nó sẽ kiểm tra dữ liệu với CRC để đảm bảo không có lỗi xảy ra trong quá trình truyền.
   - Nếu dữ liệu không có lỗi, nó sẽ chuyển lên Tầng Mạng. Nếu có lỗi, frame sẽ bị loại bỏ, và yêu cầu gửi lại có thể được đưa ra (tùy thuộc vào giao thức).

4. **Xử lý xung đột và kiểm soát luồng**:
   - Nếu có nhiều thiết bị trong mạng cùng truyền dữ liệu, tầng Liên Kết Dữ Liệu sẽ sử dụng các cơ chế kiểm soát truy cập như **CSMA/CD** hoặc **CSMA/CA** để giảm thiểu xung đột và điều chỉnh luồng dữ liệu.

### **Tóm Tắt Tầng Liên Kết Dữ Liệu (Link Layer)**:

| **Chức Năng Chính**                    | **Giao Thức Chính**                         | **Đặc Điểm**                                             | **Ứng Dụng**                              |
|----------------------------------------|--------------------------------------------|---------------------------------------------------------|------------------------------------------|
| **Đóng gói dữ liệu thành frame**      | Ethernet, PPP, HDLC, ARP                   | Đóng gói dữ liệu từ Tầng Mạng thành các frame, thêm địa chỉ MAC, kiểm tra lỗi. | Mạng LAN (Ethernet, Wi-Fi), VPN, kết nối dial-up. |
| **Địa chỉ MAC**                        | Ethernet, Wi-Fi, ARP                       | Dùng địa chỉ MAC để xác định thiết bị trong mạng.      | Mạng LAN, Wi-Fi, ARP trong mạng nội bộ. |
| **Kiểm tra lỗi**                       | Ethernet (CRC), PPP, HDLC                 | Kiểm tra lỗi trong quá trình truyền tải dữ liệu.       | Ethernet, PPP.                          |
| **Điều khiển truy cập phương tiện**    | CSMA/CD (Ethernet), CSMA/CA (Wi-Fi)        | Điều khiển cách thiết bị truy cập phương tiện truyền dẫn. | Ethernet, Wi-Fi.                        |
| **Kiểm soát luồng**                    | PPP, HDLC                                  | Điều chỉnh tốc độ truyền tải giữa các thiết bị.        | Kết nối điểm-điểm (VPN, dial-up).       |

Tầng Liên Kết Dữ Liệu là một phần không thể thiếu trong việc đảm bảo sự truyền tải dữ liệu chính xác và hiệu quả giữa các thiết bị trong mạng cục bộ hoặc trong các kết nối điểm-điểm, đóng vai trò quan trọng trong việc quản lý kết nối vật lý và bảo vệ dữ liệu trong quá trình truyền tải.
