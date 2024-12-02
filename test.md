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

----------------

### **Lớp Liên Kết Dữ Liệu (Link Layer) trong Mô Hình TCP/IP**

Lớp **Liên Kết Dữ Liệu (Link Layer)** trong mô hình **TCP/IP** tương đương với **Tầng Liên Kết Dữ Liệu (Data Link Layer)** trong mô hình OSI. Lớp này chịu trách nhiệm quản lý và điều khiển dữ liệu giữa các thiết bị trong một mạng cục bộ (LAN) hoặc các kết nối trực tiếp giữa các thiết bị (point-to-point). Nó xử lý việc đóng gói dữ liệu thành các frame, xác định địa chỉ vật lý (địa chỉ MAC), kiểm tra lỗi và quản lý việc truy cập phương tiện truyền dẫn.

### **Chức Năng Chính của Lớp Liên Kết Dữ Liệu (Link Layer)**

1. **Đóng gói dữ liệu thành frame**:
   - Dữ liệu được truyền từ Lớp Mạng (Network Layer) sẽ được đóng gói thành các frame trong lớp Liên Kết Dữ Liệu.
   - Một **frame** chứa nhiều thành phần như địa chỉ MAC nguồn và đích, dữ liệu, và thông tin kiểm tra lỗi (CRC).
   - Frame giúp truyền dữ liệu qua mạng vật lý, từ thiết bị này sang thiết bị khác.

2. **Địa chỉ MAC (Media Access Control)**:
   - Lớp Liên Kết Dữ Liệu sử dụng **địa chỉ MAC** để xác định thiết bị trong mạng LAN. Đây là địa chỉ vật lý duy nhất được gán cho mỗi thiết bị mạng, ví dụ như card mạng trong máy tính.
   - Các địa chỉ MAC giúp các thiết bị trong mạng LAN giao tiếp và xác định thiết bị đích khi gửi dữ liệu.

3. **Kiểm tra lỗi (Error Detection)**:
   - Lớp này cung cấp cơ chế kiểm tra lỗi để đảm bảo rằng dữ liệu truyền qua mạng không bị hỏng. Các phương pháp phổ biến như **CRC (Cyclic Redundancy Check)** được sử dụng để kiểm tra tính toàn vẹn của dữ liệu.
   - Nếu phát hiện lỗi, các frame bị lỗi sẽ bị loại bỏ, và yêu cầu gửi lại có thể được đưa ra (tùy thuộc vào giao thức).

4. **Điều khiển truy cập phương tiện (Media Access Control - MAC)**:
   - Lớp Liên Kết Dữ Liệu kiểm soát việc các thiết bị trong mạng LAN truy cập phương tiện truyền dẫn (như cáp đồng, cáp quang, sóng vô tuyến) để tránh xung đột khi nhiều thiết bị truyền tải đồng thời.
   - Một số giao thức như **CSMA/CD** trong Ethernet hoặc **CSMA/CA** trong Wi-Fi được sử dụng để điều khiển quyền truy cập vào phương tiện.

5. **Quản lý luồng (Flow Control)**:
   - Kiểm soát tốc độ truyền tải dữ liệu giữa các thiết bị để tránh tình trạng tắc nghẽn hoặc mất mát dữ liệu.
   - Điều này đặc biệt quan trọng trong các mạng có băng thông hạn chế.

### **Cấu Trúc Frame trong Lớp Liên Kết Dữ Liệu**

Một **frame** trong Lớp Liên Kết Dữ Liệu có thể có các thành phần sau:

1. **Địa chỉ MAC nguồn**: Địa chỉ MAC của thiết bị gửi.
2. **Địa chỉ MAC đích**: Địa chỉ MAC của thiết bị nhận.
3. **Dữ liệu**: Phần dữ liệu từ các tầng trên (thường là dữ liệu đã được đóng gói từ Tầng Mạng).
4. **Thông tin kiểm tra lỗi (CRC)**: Được sử dụng để phát hiện lỗi trong quá trình truyền dữ liệu.
5. **Đoạn điều khiển (Control)**: Thông tin hỗ trợ quá trình truyền tải như xác định loại giao thức của tầng trên (IP, ARP, v.v.).

### **Các Giao Thức trong Lớp Liên Kết Dữ Liệu (Link Layer)**

1. **Ethernet**:
   - **Ethernet** là một giao thức phổ biến trong mạng LAN. Nó sử dụng **địa chỉ MAC** để xác định các thiết bị trong mạng và kiểm soát truy cập phương tiện với giao thức **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection).
   - Ethernet hoạt động chủ yếu trên môi trường có dây, nhưng cũng có phiên bản không dây (Wi-Fi).

2. **Wi-Fi (IEEE 802.11)**:
   - **Wi-Fi** sử dụng giao thức **IEEE 802.11** để truyền tải dữ liệu không dây qua sóng radio.
   - Wi-Fi sử dụng **CSMA/CA** (Carrier Sense Multiple Access with Collision Avoidance) để tránh xung đột khi nhiều thiết bị cùng truyền dữ liệu.

3. **PPP (Point-to-Point Protocol)**:
   - **PPP** là một giao thức điều khiển liên kết được sử dụng trong các kết nối điểm-điểm, như kết nối dial-up hoặc kết nối VPN.
   - PPP cung cấp các cơ chế như xác thực, nén dữ liệu và mã hóa để đảm bảo tính bảo mật và hiệu quả trong kết nối điểm-điểm.

4. **ARP (Address Resolution Protocol)**:
   - **ARP** được sử dụng để ánh xạ địa chỉ IP sang địa chỉ MAC trong mạng LAN. Khi một thiết bị biết địa chỉ IP của một thiết bị khác nhưng không biết địa chỉ MAC, nó sẽ gửi một yêu cầu ARP để tìm địa chỉ MAC tương ứng.

5. **HDLC (High-Level Data Link Control)**:
   - **HDLC** là giao thức điều khiển liên kết dữ liệu được sử dụng trong nhiều loại mạng (LAN, WAN, kết nối điểm-điểm). Nó cung cấp cơ chế kiểm tra lỗi và kiểm soát luồng.

### **Quá Trình Hoạt Động của Lớp Liên Kết Dữ Liệu**

1. **Tạo frame**:
   - Khi dữ liệu từ **Tầng Mạng** được gửi xuống **Lớp Liên Kết Dữ Liệu**, lớp này sẽ đóng gói dữ liệu vào frame, thêm địa chỉ MAC và thông tin kiểm tra lỗi vào frame.

2. **Truyền frame qua phương tiện truyền dẫn**:
   - Các frame được truyền qua phương tiện truyền dẫn vật lý (như cáp Ethernet, sóng Wi-Fi).

3. **Kiểm tra lỗi**:
   - Khi một thiết bị nhận được frame, nó sẽ kiểm tra dữ liệu trong frame bằng cách sử dụng CRC để đảm bảo tính toàn vẹn của dữ liệu. Nếu dữ liệu bị lỗi, frame sẽ bị loại bỏ.

4. **Xử lý và chuyển tiếp**:
   - Nếu frame không có lỗi, dữ liệu sẽ được gửi lên Tầng Mạng để tiếp tục xử lý.

5. **Điều khiển truy cập phương tiện**:
   - Nếu có nhiều thiết bị cùng muốn truyền dữ liệu, Lớp Liên Kết Dữ Liệu sử dụng các cơ chế như **CSMA/CD** (Ethernet) hoặc **CSMA/CA** (Wi-Fi) để tránh xung đột và điều khiển quyền truy cập vào phương tiện truyền dẫn.

### **Tóm Tắt Lớp Liên Kết Dữ Liệu (Link Layer)** trong TCP/IP:

| **Chức Năng Chính**                    | **Giao Thức Chính**                         | **Đặc Điểm**                                             | **Ứng Dụng**                              |
|----------------------------------------|--------------------------------------------|---------------------------------------------------------|------------------------------------------|
| **Đóng gói dữ liệu thành frame**      | Ethernet, PPP, HDLC, ARP                   | Đóng gói dữ liệu từ Tầng Mạng thành các frame, thêm địa chỉ MAC, kiểm tra lỗi. | Mạng LAN (Ethernet, Wi-Fi), VPN, kết nối dial-up. |
| **Địa chỉ MAC**                        | Ethernet, Wi-Fi, ARP                       | Dùng địa chỉ MAC để xác định thiết bị trong mạng.      | Mạng LAN, Wi-Fi, ARP trong mạng nội bộ. |
| **Kiểm tra lỗi**                       | Ethernet (CRC), PPP, HDLC                 | Kiểm tra lỗi trong quá trình truyền tải dữ liệu.       | Ethernet, PPP.                          |
| **Điều khiển truy cập phương tiện**    | CSMA/CD (Ethernet), CSMA/CA (Wi-Fi)        | Điều khiển cách thiết bị truy cập phương tiện truyền dẫn. | Ethernet, Wi-Fi.                        |
| **Kiểm soát luồng**                    | PPP, HDLC                                  | Điều chỉnh tốc độ truyền tải giữa các thiết bị.        | Kết nối điểm-điểm (VPN, dial-up).       |

Lớp Liên Kết Dữ Liệu trong TCP/IP là một lớp quan trọng để đảm bảo rằng dữ liệu được truyền chính xác giữa các thiết bị trong mạng. Nó không chỉ liên quan đến việc truyền tải dữ liệu, mà còn chịu trách nhiệm về các cơ chế kiểm tra lỗi, kiểm soát luồng, và điều khiển truy cập vào phương tiện truyền dẫn.
