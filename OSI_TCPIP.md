### **OSI**

### **1. MÔ HÌNH OSI**

-  OSI không chỉ định giao thức, mà chỉ định nhiệm vụ của giao thức

**1.1 Các giao thức trong mô hình OSI**

**a. Giao thức hướng liên kết (Connection Oriented)**
- Thiết lập 1 kết nối logic trong cùng 1 tầng của 2 thiết bị trước khi truyền dữ liệu.
- Kiểm tra lỗi, phát hiện và gửi lại dữ liệu bị mất.

**b. Giao thức không liên kết (Connectionless Protocol)**
- Dữ liệu được gửi duới dạng packets độc lập.
- Không có đảm bảo dữ liệu sẽ đến đích hoặc gửi theo đúng thứ tự

**1.2 Vai trò và chức năng 7 tầng OSI**

**Tầng 1 - Physical layer (Tầng vật lý)**

**Lớp Vật lý (Physical Layer)** trong mô hình OSI là lớp **thấp nhất**, chịu trách nhiệm truyền tải tín hiệu vật lý qua phương tiện truyền dẫn (cáp, sóng radio, v.v.). Lớp này không xử lý dữ liệu dưới dạng gói, mà chỉ quan tâm đến cách truyền và nhận tín hiệu giữa các thiết bị.


**Chức năng chính của Lớp Vật lý**
1. **Chuyển đổi dữ liệu thành tín hiệu vật lý**:
   - Biến dữ liệu số (bit 0 và 1) thành tín hiệu điện, ánh sáng, hoặc sóng radio để truyền qua cáp hoặc môi trường không dây.

2. **Truyền tín hiệu qua phương tiện truyền dẫn**:
   - Đảm bảo tín hiệu được truyền từ nguồn đến đích qua các phương tiện truyền dẫn:
     - Cáp mạng (Ethernet, quang học, đồng).
     - Sóng không dây (Wi-Fi, Bluetooth, sóng di động).

3. **Đồng bộ hóa tín hiệu**:
   - Đảm bảo rằng thiết bị gửi và nhận hiểu được thời điểm bắt đầu và kết thúc của mỗi bit.

4. **Xác định tốc độ truyền dữ liệu**:
   - Quy định tốc độ truyền tải (tốc độ băng thông) giữa các thiết bị.

5. **Kiểm soát môi trường truyền dẫn**:
   - Xác định các đặc tính vật lý như:
     - Điện áp sử dụng.
     - Tần số sóng.
     - Kiểu đầu nối (RJ45, USB, cổng quang...).

6. **Kiểm soát truy cập môi trường (Media Access Control)**:
   - Giúp các thiết bị chia sẻ một môi trường truyền dẫn vật lý mà không xung đột tín hiệu.

---

**Ví dụ cụ thể trong Lớp Vật lý**
- **Cáp Ethernet (RJ45):**
  - Chuyển đổi tín hiệu điện qua dây cáp đồng.
  - Tốc độ truyền có thể là 10 Mbps, 100 Mbps, 1 Gbps...
- **Cáp quang (Fiber Optics):**
  - Truyền tín hiệu ánh sáng qua sợi quang học, tốc độ cao hơn (10 Gbps, 100 Gbps...).
- **Wi-Fi:**
  - Sử dụng sóng radio để truyền tín hiệu qua không khí, thường dùng tần số 2.4 GHz hoặc 5 GHz.

**Các thiết bị liên quan đến Lớp Vật lý**
1. **Hub**:
   - Thiết bị đơn giản truyền tín hiệu đến tất cả các thiết bị trong mạng mà không xử lý dữ liệu.
2. **Repeater**:
   - Khuếch đại tín hiệu để truyền xa hơn trong mạng.
3. **Modem**:
   - Chuyển đổi tín hiệu số từ máy tính thành tín hiệu analog để truyền qua đường dây điện thoại hoặc cáp.
4. **Cáp mạng**:
   - Các loại cáp truyền dẫn như Ethernet, cáp quang, hoặc cáp đồng trục.

**Đặc điểm của Lớp Vật lý**
- **Không xử lý dữ liệu**:
  - Chỉ quan tâm đến tín hiệu vật lý, không biết nội dung dữ liệu đang truyền.
- **Hoạt động gần phần cứng**:
  - Phần lớn công việc được thực hiện bởi phần cứng như card mạng (NIC), dây cáp, hoặc anten Wi-Fi.
- **Tốc độ truyền**:
  - Phụ thuộc vào công nghệ truyền dẫn (Ethernet, Wi-Fi, cáp quang…).

**Một số tiêu chuẩn và giao thức của Lớp Vật lý**
1. **Ethernet (IEEE 802.3)**:
   - Quy định cách truyền tín hiệu qua cáp đồng hoặc cáp quang.
2. **Wi-Fi (IEEE 802.11)**:
   - Quy định cách truyền tín hiệu không dây qua sóng radio.
3. **Bluetooth**:
   - Truyền tín hiệu không dây trong khoảng cách ngắn.
4. **USB (Universal Serial Bus)**:
   - Truyền dữ liệu giữa các thiết bị thông qua cáp vật lý.

---


**Tầng 2 - Data Link Layer ( Tầng liên kết dữ liệu)**

**Lớp Liên kết Dữ liệu (Data Link Layer)** trong mô hình OSI là lớp thứ hai, đóng vai trò quan trọng trong việc xử lý và đóng gói dữ liệu để truyền qua phương tiện vật lý. Nó đảm bảo rằng dữ liệu có thể được truyền một cách an toàn và hiệu quả giữa các thiết bị trong một mạng cục bộ hoặc qua môi trường truyền dẫn.

**Chức năng chính của Lớp Liên kết Dữ liệu**
1. **Đóng khung (Framing)**:
   - Chia dữ liệu từ lớp Giao vận (Transport Layer) thành các khung dữ liệu nhỏ hơn.
   - Mỗi khung bao gồm trường header và trailer để định dạng và kiểm soát lỗi.

2. **Địa chỉ vật lý (Physical Addressing)**:
   - Sử dụng địa chỉ MAC (Media Access Control) để xác định nguồn và đích của mỗi khung dữ liệu.

3. **Kiểm soát truy cập môi trường (Media Access Control)**:
   - Quản lý việc truy cập vào môi trường truyền dẫn chung, đặc biệt trong mạng có nhiều thiết bị.
   - Giải quyết vấn đề va chạm và phân bổ thời gian truy cập.

4. **Kiểm tra và xử lý lỗi (Error Detection and Handling)**:
   - Phát hiện lỗi xảy ra trong quá trình truyền dữ liệu bằng cách sử dụng các thuật toán như CRC (Cyclic Redundancy Check).
   - Đảm bảo tính toàn vẹn của dữ liệu truyền.

5. **Kiểm soát luồng (Flow Control)**:
   - Điều chỉnh tốc độ truyền dữ liệu giữa người gửi và người nhận để tránh quá tải.

**Các Giao thức và Tiêu chuẩn của Lớp Liên kết Dữ liệu**
1. **Ethernet (IEEE 802.3)**:
   - Là tiêu chuẩn phổ biến nhất cho mạng LAN, sử dụng địa chỉ MAC để xác định các thiết bị và điều khiển việc truy cập môi trường truyền thông.

2. **Wi-Fi (IEEE 802.11)**:
   - Cũng sử dụng địa chỉ MAC, nhưng trong môi trường không dây, cung cấp kết nối linh hoạt và dễ dàng mở rộng.

3. **PPP (Point-to-Point Protocol)**:
   - Cho phép truyền thông qua đường dây điện thoại hoặc liên kết dữ liệu nối tiếp, thường được sử dụng trong kết nối internet qua điện thoại.

4. **ARP (Address Resolution Protocol)**:
   - Giúp dịch địa chỉ IP thành địa chỉ MAC, cần thiết cho việc gửi dữ liệu giữa các thiết bị trong mạng LAN.

5. **HDLC (High-Level Data Link Control)**:
   - Giao thức liên kết dữ liệu chung, cung cấp cơ chế kiểm tra lỗi và điều khiển luồng trong mạng điểm-đến-điểm và điểm-đến-đa điểm.

**Các Thiết bị Hoạt động ở Lớp Liên kết Dữ liệu**
1. **Switch**:
   - Chuyển mạch các khung dữ liệu dựa trên địa chỉ MAC đến cổng đích thích hợp.
   - Giảm bớt lưu lượng mạng bằng cách giới hạn phạm vi truyền dẫn khung dữ liệu đến các thiết bị đích.

2. **Bridge**:
   - Kết nối các mạng LAN hoặc phân đoạn mạng LAN thành nhóm nhỏ, giảm bớt lưu lượng và cải thiện hiệu suất.
   - Hoạt động tại lớp Liên kết Dữ liệu và có khả năng lọc lưu lượng.

**Tác động và Vai trò**
- **Đảm bảo truyền dẫn dữ liệu**: Lớp Liên kết Dữ liệu là lớp quan trọng để bảo đảm dữ liệu được truyền từ người gửi đến người nhận một cách chính xác và an toàn.
- **Cải thiện hiệu suất mạng**: Đóng gói dữ liệu vào các khung và quản lý lưu lượng giúp tối ưu hóa sử dụng môi trường truyền dẫn.

-----------------

**Tầng 3 - Network Layer**

**Lớp Mạng (Network Layer) trong Mô hình OSI**

Lớp Mạng là lớp thứ ba trong mô hình OSI, có vai trò quan trọng trong việc định tuyến gói tin qua mạng, điều phối dữ liệu giữa các mạng khác nhau, và đảm bảo rằng dữ liệu được gửi đến đúng đích. Lớp này xử lý các vấn đề liên quan đến định tuyến gói dữ liệu từ nguồn đến đích, kể cả khi các thiết bị nguồn và đích nằm trên các mạng khác nhau.

**Chức năng chính của Lớp Mạng**
1. **Định tuyến (Routing):**
   - Xác định đường đi tối ưu cho gói tin từ nguồn đến đích.
   - Sử dụng các bảng định tuyến và thuật toán định tuyến để đưa ra quyết định về đường đi cho mỗi gói tin.

2. **Phân đoạn và Tái lắp ráp (Fragmentation and Reassembly):**
   - Chia gói tin lớn thành các phân đoạn nhỏ hơn phù hợp với kích thước tối đa mà mạng có thể xử lý (MTU) và tái lắp ráp chúng ở đầu cuối nhận.

3. **Địa chỉ hóa logic (Logical Addressing):**
   - Sử dụng địa chỉ IP để xác định địa chỉ nguồn và đích cho mỗi gói tin.
   - Địa chỉ IP cho phép định tuyến qua các mạng phức tạp và đa dạng.

4. **Xử lý các gói dữ liệu:**
   - Xử lý các gói dữ liệu bao gồm các header với thông tin về định tuyến và điều khiển.

5. **Kiểm soát lỗi:**
   - Phát hiện và xử lý lỗi trong các gói dữ liệu như lỗi định tuyến hoặc địa chỉ không hợp lệ.

**Giao thức phổ biến của Lớp Mạng**
1. **IP (Internet Protocol):**
   - Phiên bản IPv4 và IPv6 là nền tảng của Internet hiện đại, định tuyến gói dữ liệu trên mạng toàn cầu.

2. **ICMP (Internet Control Message Protocol):**
   - Sử dụng cho việc gửi thông điệp điều khiển và báo cáo lỗi, như thông báo đích không đạt được hoặc việc chuyển hướng định tuyến.

3. **IGMP (Internet Group Management Protocol):**
   - Quản lý thành viên trong các nhóm truyền thông đa điểm (multicast).

4. **OSPF (Open Shortest Path First) và BGP (Border Gateway Protocol):**
   - OSPF là giao thức định tuyến nội vùng sử dụng thuật toán trạng thái liên kết.
   - BGP là giao thức định tuyến giữa các tổ chức khác nhau, quản lý cách các nhà cung cấp dịch vụ Internet trao đổi thông tin định tuyến.

 **Thiết bị hoạt động ở Lớp Mạng**
- **Router:**
   - Thiết bị chính trong lớp Mạng, chịu trách nhiệm định tuyến gói tin giữa các mạng.
   - Cập nhật và duy trì bảng định tuyến, quyết định đường đi cho gói tin dựa trên địa chỉ IP.

- **Layer 3 Switch (Switch đa lớp):**
   - Kết hợp chức năng của switch và router, có thể định tuyến gói tin dựa trên địa chỉ IP ngoài chức năng chuyển mạch thông thường.

**Vai trò và Tác động**
- **Chức năng mở rộng mạng:** Đảm bảo rằng dữ liệu có thể đi qua các mạng lớn và phức tạp trên toàn cầu.
- **Cải thiện hiệu suất:** Tối ưu hóa đường đi của gói tin, giảm thiểu độ trễ và tắc nghẽn mạng.
- **Tăng tính linh hoạt:** Định tuyến dựa trên nhu cầu và tình trạng mạng, cho phép mạng thích ứng với thay đổi.

---------------

**Tầng 4 - Transport Layer (Tầng vận chuyển)**

- Quản lý và điêu phối việc truyền tải dữ liệu giữa các thiết bị đầu cuối (end-to-end). Đảm bảo dữ liệu được truyền tải từ ứng dụng ở thiết bị nguồn đến ứng dụng ở thiết bị đích một cách chính xác, an toàn và hiệu quả.

**Chức năng của Transport layer**
**Tầng Giao vận (Transport Layer) trong Mô hình OSI**

Tầng Giao vận là lớp thứ tư trong mô hình OSI và có vai trò cực kỳ quan trọng trong việc quản lý giao tiếp dữ liệu giữa các ứng dụng trên các thiết bị mạng. Lớp này cung cấp các dịch vụ truyền thông đáng tin cậy, hiệu quả giữa các thiết bị cuối trong một mạng.

**Chức năng chính của Tầng Giao vận**
1. **Đa hóa kết nối (Multiplexing):**
   - Cho phép nhiều ứng dụng trên một thiết bị sử dụng cùng một mạng mà không xảy ra xung đột, thông qua cơ chế gán các cổng khác nhau cho các phiên khác nhau.

2. **Đảm bảo dịch vụ (Service Assurance):**
   - Cung cấp khả năng truyền dữ liệu đáng tin cậy, bao gồm kiểm soát lỗi, kiểm soát luồng và quản lý tắc nghẽn.

3. **Phân đoạn dữ liệu (Segmentation):**
   - Chia dữ liệu lớn thành các phân đoạn nhỏ hơn để dễ dàng truyền tải và quản lý.

4. **Kiểm soát luồng (Flow Control):**
   - Điều chỉnh tốc độ truyền dữ liệu giữa người gửi và người nhận để tránh làm quá tải bộ đệm của người nhận.

5. **Kiểm tra lỗi (Error Checking):**
   - Sử dụng các thuật toán kiểm tra lỗi để đảm bảo dữ liệu được truyền đúng và hoàn chỉnh.

6. **Điều chỉnh tắc nghẽn (Congestion Control):**
   - Giảm tốc độ truyền khi phát hiện mạng bị tắc nghẽn để ngăn chặn mất dữ liệu.

**Giao thức phổ biến của Tầng Giao vận**
1. **TCP (Transmission Control Protocol):**
   - Giao thức kết nối hướng và đáng tin cậy, cung cấp kiểm soát lỗi, kiểm soát luồng và điều chỉnh tắc nghẽn.
   - Đảm bảo rằng mọi gói dữ liệu đều được nhận đúng thứ tự và không bị mất mát.

2. **UDP (User Datagram Protocol):**
   - Giao thức không kết nối và không đáng tin cậy, truyền dữ liệu mà không cần thiết lập kết nối và không cung cấp kiểm soát luồng hay điều chỉnh tắc nghẽn.
   - Thích hợp cho các ứng dụng yêu cầu tốc độ truyền cao và có thể chấp nhận một số mất mát dữ liệu, như truyền video hoặc trò chơi trực tuyến.

3. **SCTP (Stream Control Transmission Protocol):**
   - Giao thức mới hơn, kết hợp các tính năng của TCP và UDP.
   - Hỗ trợ truyền nhiều luồng dữ liệu đồng thời trong một kết nối, giúp cải thiện hiệu suất và độ tin cậy.

**Thiết bị và Công cụ hoạt động ở Tầng Giao vận**
- **Thiết bị**: Chủ yếu là phần mềm được tích hợp trong hệ điều hành hoặc ứng dụng, vì tầng Giao vận không yêu cầu phần cứng cụ thể.
- **Công cụ**: Các thư viện lập trình mạng như Winsock, BSD Sockets cho phép các nhà phát triển truy cập vào chức năng của TCP và UDP trong các ứng dụng của họ.

**Vai trò và Tác động**
- **Đảm bảo tính đáng tin cậy**: TCP và các giao thức khác đảm bảo dữ liệu được gửi một cách đáng tin cậy, đặc biệt là trong môi trường mạng không ổn định.
- **Hỗ trợ các ứng dụng đa dạng**: Từ duyệt web, email đến trò chơi và truyền phát trực tiếp, tầng Giao vận là nền tảng cho hầu hết các loại giao tiếp mạng.

----

- Quản lý kết nối: Thiết lập 1 kết nối giữa các thiết bị đầu cuối. Kết nối có trạng thái (TCP) dữ liệu được truyền sau khi một kết nối ổn định được thiết lập. Kết nối không trạng thái (UDP) dữ liệu được truyền mà không cần thiết lập kết nối.
- Đảm bảo truyền tải đáng tin cậy: quản lý việc truyền tải dữ liệu giữa các thiết bị tránh tắc nghẽn. Kiểm tra và sửa lỗi (checksum). Sắp xếp thứ tự packets.
- Chia dữ liệu thành các segment (đoạn) để truyền qua mạng và sau đó tái hợp lại ở phía người nhận.

**Quá trình hoạt động của Transport Layer**

1. Thiết lập kết nối

- Khi 1 ứng dụng muốn gửi dữ liệu đến 1 ứng dụng khác, Transport layer sẽ thiết lập 1 kết nối giữa chúng (TCP). VD khi ở 1 web trình duyệt sẽ thiết lập 1 kết nối TCP với máy chủ web.

2. Chia dữ liệu thành các segment

- Dữ liệu từ ứng dụng được chia thành các segment nhỏ. Mỗi segment này chứa 1 thông tin điều khiển như số thứ tự của segment, số hiệu kết nối và thông tin kiểm tra lỗi.

3. Truyền tải các segment qua mạng

- Các segment được gửi qua các tầng dưới (Network, Datalink, Phisical) để đến thiết bị đích. VD segment từ trình duyệt sẽ đi qua router, switch để đến máy chủ.

4. Tái hợp và xử lý dữ liệu ở thiết bị nhận

- Khi các segment đến đích Transport Layer của thiết bị nhận  sẽ tái hợp chúng thành dữ liệu đầy đủ và truyền lên tầng trên ( 5 6) để xử lý. VD: khi tải trang web, các segment TCP sẽ được tái hợp lại và trình duyệt sẽ hiển thị trang web

5. Kiểm tra và sửa lỗi

- Nếu segment bị mất hoặc lỗi trong quá trình truyền, Transport layer sẽ yêu cầu gửi lại segment đó.

**Tầng 5 - Session Layer (Tầng phiên)**

**Tầng Phiên (Session Layer) trong Mô hình OSI**

Tầng Phiên, lớp thứ năm trong mô hình OSI, đóng vai trò quan trọng trong việc quản lý và duy trì các phiên làm việc giữa hai thiết bị hoặc ứng dụng qua mạng. Tầng này chủ yếu xử lý việc thiết lập, quản lý và kết thúc các phiên giao tiếp.

**Chức năng chính của Tầng Phiên**
1. **Thiết lập, quản lý và kết thúc phiên làm việc:**
   - Tạo ra các phiên giao tiếp giữa các ứng dụng trên các thiết bị khác nhau.
   - Quản lý và duy trì phiên làm việc, đảm bảo thông tin được truyền tải hiệu quả và đúng thứ tự.

2. **Đồng bộ hóa:**
   - Đảm bảo các giao tiếp diễn ra theo thứ tự và dữ liệu được đồng bộ hóa, giúp phục hồi sau khi có sự cố mạng mà không cần truyền lại toàn bộ thông tin.

3. **Kiểm soát biên (Checkpointing):**
   - Tạo điểm kiểm soát trong dữ liệu được truyền để trong trường hợp lỗi, chỉ cần phục hồi từ điểm kiểm soát cuối cùng chứ không phải bắt đầu lại từ đầu.

4. **Quản lý các giao tiếp đồng thời:**
   - Xử lý nhiều phiên giao tiếp giữa các ứng dụng trên một thiết bị, đảm bảo mỗi ứng dụng nhận được sự chú ý thích hợp và không bị can thiệp lẫn nhau.

**Giao thức phổ biến của Tầng Phiên**
1. **RPC (Remote Procedure Call):**
   - Cho phép một chương trình yêu cầu một dịch vụ từ một chương trình khác nằm trên máy tính khác trong mạng, mà không cần quan tâm đến chi tiết mạng.

2. **SQL (Structured Query Language):**
   - Sử dụng trong các giao tiếp cơ sở dữ liệu, SQL quản lý các phiên giao tiếp giữa ứng dụng và cơ sở dữ liệu.

3. **NFS (Network File System):**
   - Cho phép các hệ thống tập tin trên các máy tính khác nhau chia sẻ thông qua mạng, dùng phiên để quản lý các truy cập tập tin.

4. **NetBIOS (Network Basic Input/Output System):**
   - Cung cấp dịch vụ giao tiếp cho các máy tính trong mạng LAN, bao gồm thiết lập và quản lý phiên.

5. **PPTP (Point-to-Point Tunneling Protocol):**
   - Sử dụng trong các kết nối VPN, quản lý các phiên kết nối từ điểm này đến điểm khác qua mạng IP.

**Thiết bị hoạt động ở Tầng Phiên**
- Không có thiết bị cụ thể nào được thiết kế riêng cho Tầng Phiên. Thay vào đó, các chức năng của tầng này chủ yếu được xử lý bởi phần mềm trên máy chủ và máy trạm, như phần mềm quản lý mạng hoặc các hệ thống quản lý cơ sở dữ liệu.

**Vai trò và Tác động**
- **Quản lý giao tiếp:** Tầng Phiên đóng vai trò cốt lõi trong việc đảm bảo rằng các phiên giao tiếp giữa các ứng dụng được thiết lập, duy trì và kết thúc một cách hiệu quả.
- **Hỗ trợ các ứng dụng phức tạp:** Tầng này cung cấp nền tảng cho các ứng dụng đa yêu cầu, như các dịch vụ tài chính trực tuyến, trò chơi đa người chơi và ứng dụng chia sẻ tài liệu.


--------

- Quản lý và duy trì các phiên làm việc (sessions) giữa các ứng dụng đang giao tiếp trên các thiết bị khác nhau. Xác định cách giao tiếp, duy trì kết nối quản lý phiên làm việc giữa 2 ứng dụng (gồm khởi tạo, đồng bộ hóa và kết thúc các phiên giao tiếp)

**Chức năng của Session Layer**

- Thiết lập, duy trì và kết thúc phiên làm việc: Session Layer thiết lập 1 phiên làm việc giữa 2 ứng dụng. Sau khi hoàn thành giao tiếp, nó sẽ kết thúc phiên đó và giải phóng tài nguyên.
- Quản lý đối thoại (Dialog Control): Kiểm soát kiểu đối thoại giữa các ứng dụng, half-duplex (giao tiếp chỉ có thể diễn ra theo 1 chiều tại 1 thời điểm) và full-duplex (giao tiếp có thể diễn ra 2 chiều đồng thời). VD khi trong 1 cuộc gọi video session layer kiểm soát việc truyền tải âm thanh và hình ảnh đồng thời giữa 2 bên.
- Đồng bộ hóa dữ liệu: Cung cấp các cơ chế để đồng bộ hóa dữ liệu giữa các ứng dụng, đảm bảo rằng các gói dữ liệu được truyền và nhận đúng thời gian. VD khi tải video từ ỉnternet session layer đảm bảo dữ liệu được đồng bộ hóa để video có thể phát liền mạch mà không bị gián đoạn.
- Khôi phục giao tiếp: Nếu có gián đoạn trong giao tiếp, session có thể quản lý việc khôi phục lại kết nối mà không làm mất dữ liệu.

------------------------------------------------------------

**Tầng 6 - Presentation Layer (Tầng trình bày)**

**Tầng Trình bày (Presentation Layer) trong Mô hình OSI**

Tầng Trình bày là lớp thứ sáu trong mô hình OSI, đóng vai trò cầu nối giữa các dữ liệu mà ứng dụng tạo ra và cách dữ liệu đó được chuyển qua mạng. Tầng này chủ yếu xử lý định dạng dữ liệu, mã hóa và chuyển đổi dữ liệu để đảm bảo các ứng dụng trên các hệ thống khác nhau có thể hiểu được dữ liệu cùng một cách.

**Chức năng chính của Tầng Trình bày**
1. **Chuyển đổi dữ liệu:**
   - Đảm bảo dữ liệu được truyền từ một ứng dụng tới một ứng dụng khác có thể được đọc và hiểu một cách chính xác, không phụ thuộc vào kiến trúc nền tảng hệ thống.
   - Chuyển đổi các định dạng mã hóa khác nhau, như ASCII, Unicode, EBCDIC.

2. **Mã hóa dữ liệu:**
   - Bảo mật dữ liệu bằng cách mã hóa trước khi truyền và giải mã tại điểm nhận.
   - Quan trọng đối với việc truyền thông an toàn trên mạng.

3. **Nén dữ liệu:**
   - Giảm băng thông cần thiết cho việc truyền tải dữ liệu.
   - Nén dữ liệu để giảm kích thước gói tin, tăng hiệu quả truyền tải.

**Giao thức và Tiêu chuẩn của Tầng Trình bày**
- **SSL (Secure Sockets Layer) và TLS (Transport Layer Security):**
   - Cung cấp bảo mật cho các giao tiếp mạng bằng cách mã hóa phiên trước khi dữ liệu được truyền đi.
- **MIME (Multipurpose Internet Mail Extensions):**
   - Cho phép truyền các tệp không phải là văn bản qua email, bằng cách mã hóa chúng thành định dạng có thể truyền qua Internet.
- **JPEG, GIF, TIFF (định dạng ảnh):**
   - Quy định cách mã hóa và nén ảnh.
- **MPEG, QuickTime, RealVideo (định dạng video và âm thanh):**
   - Quy định cách nén và truyền dữ liệu âm thanh và video.

**Vai trò và Tác động của Tầng Trình bày**
- **Độc lập với nền tảng:** Đảm bảo rằng dữ liệu từ các ứng dụng được trình bày một cách nhất quán, bất kể nền tảng hệ thống hay kiến trúc của thiết bị.
- **Tăng cường bảo mật:** Mã hóa dữ liệu trước khi chúng được gửi qua mạng giúp bảo vệ chống lại sự nghe trộm và can thiệp dữ liệu.
- **Tối ưu hóa băng thông:** Nén dữ liệu giúp giảm thiểu chi phí băng thông và cải thiện hiệu suất truyền tải.

-----------

- Chịu trách nhiệm định dạng, mã hóa, giải mã, nén dữ liệu giữa các ứng dụng. Đảm bảo rằng dữ liệu có thể được hiểu đúng giữa các hệ thống khác nhau, ngay cả khi giữa chúng sử dụng các định dạng hoặc phương thức mã hóa khác nhau. Hoạt động như cầu nối giữa tầng 7 và tầng 5.

**Chức năng chính của Presentation Layer**

- Chuyển đổi định dạng: Khi hai hệ thống sử dụng các định dạng khác nhau để truyền tải dữ liệu, Presentation thực hiện chuyển đổi giữa các định dạng sao cho ứng dụng nhận có thể hiểu được.
- Mã hóa và giải mã: Presentation sẽ mã hóa dữ liệu trước khi gửi đi và giải mã dữ liệu khi nhận được.
- Nén và giải nén: Nén dữ liệu để giảm băng thông khi truyền tải qua mạng và giải nén dữ liệu khi nhận
- Đảm bảo tính tương thích: Presentation đảm bảo rằng các hệ thống sử dụng các ngôn ngữ hoặc định dạng khác nhau vẫn có thể giao tiếp với nhau mà không gặp lỗi.

------------------------------------------

**Tầng 7 - Application Layer ( Tầng ứng dụng)**

**Tầng Ứng dụng (Application Layer) trong Mô hình OSI**

Tầng Ứng dụng là lớp thứ bảy và cũng là lớp cao nhất trong mô hình OSI. Lớp này cung cấp giao diện cho các ứng dụng để truy cập vào mạng. Nó đóng vai trò trực tiếp trong việc hỗ trợ các dịch vụ mạng cuối cùng cho người dùng.

**Chức năng chính của Tầng Ứng dụng**
1. **Cung cấp giao diện người dùng:**
   - Cho phép người dùng tương tác với các ứng dụng mạng như trình duyệt web, email, và các dịch vụ truyền thông.

2. **Hỗ trợ các ứng dụng mạng:**
   - Tạo điều kiện cho các ứng dụng mạng thực hiện các chức năng cụ thể như truy cập cơ sở dữ liệu, truyền tệp, và truyền thông điện tử.

3. **Xử lý dữ liệu đặc thù ứng dụng:**
   - Định dạng và mã hóa dữ liệu theo cách thức phù hợp với từng ứng dụng cụ thể.

**Giao thức phổ biến của Tầng Ứng dụng**
1. **HTTP (HyperText Transfer Protocol):**
   - Giao thức nền tảng cho web, quản lý truyền thông giữa trình duyệt web và máy chủ web.

2. **FTP (File Transfer Protocol):**
   - Cho phép truyền tệp giữa máy chủ và máy khách.

3. **SMTP (Simple Mail Transfer Protocol):**
   - Dùng để truyền email giữa máy chủ thư điện tử.

4. **DNS (Domain Name System):**
   - Dịch tên miền thành địa chỉ IP, là cơ sở cho mọi hoạt động trên internet.

5. **DHCP (Dynamic Host Configuration Protocol):**
   - Tự động cấp phát địa chỉ IP và thông tin cấu hình khác cho thiết bị trong mạng.

6. **LDAP (Lightweight Directory Access Protocol):**
   - Quản lý và truy cập thông tin phân phối rộng rãi trong một mạng máy tính.

7. **SOAP (Simple Object Access Protocol) và REST (Representational State Transfer):**
   - Cung cấp cơ chế cho các dịch vụ web để giao tiếp với nhau qua mạng.

**Vai trò và Tác động của Tầng Ứng dụng**
- **Tương tác trực tiếp với người dùng cuối:** Là lớp duy nhất trong mô hình OSI mà người dùng cuối tương tác trực tiếp, qua các ứng dụng mạng.
- **Quản lý thông tin ứng dụng:** Đảm bảo thông tin được gửi và nhận một cách chính xác, an toàn và hiệu quả qua các ứng dụng.
- **Độc lập với dữ liệu:** Cho phép các ứng dụng hoạt động mà không cần quan tâm đến chi tiết về cách dữ liệu được truyền qua mạng.

------------

 - Cung cấp các dịch vụ và giao thức cho ứng dụng người dùng cuối. Đây là nơi mà các giao tiếp mạng giữa các ứng dụng và hệ thống diễn ra.

**Chức năng của Application Layer**

- Giao tiếp giữa các ứng dụng: Cho phép các ứng dụng trên các thiết bị khác nhau giao tiếp với nhau thông qua giao thức mạng.
- Quản lý dịch vụ: Cung cấp các dịch vụ như email, truyền tệp, trình duyệt web, và các ứng dụng mạng khác.
- Đảm bảo tính tương thích và định dạng dữ liệu: Chuyển đổi dữ liệu giữa các ứng dụng và hệ thống khác nhau.
- Chạy các ứng dụng người dùng cuối: Gồm các ứng dụng như web browser, email client, FTP client.

-------------------------------------

### **TCP/IP (Transmission Control Protocol/Internet Protocol)**

**1. TCP/IP là gì** 

- là một bộ giao thức mạng được sử dụng để truyền tải dữ liệu qua các mạng máy tính. TCP/IP là một giao thức liên kết hai tầng, bao gồm tầng TCP và tầng IP, mỗi tầng thực hiện các chức năng riêng biệt nhưng hỗ trợ lẫn nhau để đảm bảo việc truyền tải dữ liệu hiệu quả.

**2. IP (Internet Protocol)**

**Định danh thiết bị**
- Mỗi thiết bị trong mạng được cấp 1 địa chỉ IP để định danh thiết bị và để chúng có thể giao tiếp với nhau. Giống như mỗi nhà có 1 địa chỉ riêng để nhận thư, mỗi thiết bị trên mạng cần một địa chỉ IP để nhận và gửi dữ liệu.

**Định tuyến dữ liệu (Routing)**
- Quá trình tìm đường đi tối ưu để các gói tin di chuyển từ thiết bị nguồn đến thiết bị đích qua mạng.
- Nếu gói tin quá lớn để truyền qua 1 mạng, nó sẽ được phân mảnh thành các gói nhỏ (chứa địa chỉ IP nguồn, đích), mỗi mảnh sẽ có 1 header (tiêu đề) chứa thông tin vị trí. Mỗi mạng có giới hạn kích thước gói tin mà nó có thể truyền (gọi là MTU - Maximum Transmission Unit). Gói tin được gửi từ thiết bị nguồn => Đi qua Router (thiết bị trung gian trên mạng internet): Router đọc địa chỉ IP đích và định tuyến gói tin đến mạng tiếp theo. Khi đến đích, thiết bị đích sẽ dùng thông tin trong tiêu đề để ghép các mảnh lại đúng thứ tự, tạo thành gói tin ban đầu.
- **Vấn đề phát sinh:**
Nếu một mảnh bị mất trong quá trình truyền, thiết bị đích không thể lắp ráp gói tin đầy đủ. Khi đó, giao thức cao hơn (như TCP) sẽ yêu cầu gửi lại gói tin.

- Hoạt động ở Network Layer trong mô hình OSI và ở Internet Layer của TCP/IP

**3. TCP (Transmission Control Protocol)**

- Hoạt động ở Transport Layer trong mô hình OSI.

a. Chia nhỏ dữ liệu thành các segment.

- Dữ liệu từ ứng dụng sẽ được chia thành các segment (không phải tất cả đều được chia mà nó chia theo chuẩn segment). Mỗi segment có thêm 1 số thông tin điều khiển như port nguồn, port đích, mã số sequence, mã số acknowledment.

b. Thiết lập kết nối (Three-way Handshake)

- 3 bước trong quá trình thiết lập kết nối giữa hai thiết bị:
    1. SYN (Synchronize): Thiết bị A gửi 1 gói SYN đến thiết bị B, yêu cầu bắt đầu kết nối
    2. SYN-ACK (Synchronize-Acknowledgment): Thiết bị B nhận được yêu cầu và trả lời bằng một gói SYN_ACK
    3. ACK (Acknowledgment): Thiết bị A xác nhận nhận được gói SYN-ACK và gửi lại một gói ACK.
    => Sau khi 3 bước này hoàn tất, kết nối giữa hai thiết bị được thiết lập và truyền dữ liệu có thể bắt đầu.
c. Điều khiển lưu lượng (Flow control)

- TCP sử dụng window size (cho biết số lượng byte dữ liệu mà thiết bị gửi có thể truyền đi mà không cần đợi ACK) để điều khiển lượng dữ liệu được gửi đi tại 1 thời điểm, nhằm tránh tình trạng quá tải băng thông hoặc bộ nhớ của thiết bị nhận.

d. Kiểm tra lỗi (Error checking)

- Mỗi segment TCP đều có checksum để kiểm tra xem dữ liệu có bị lỗi trong quá trình truyền tải hay không. Nếu có lỗi, gói tin sẽ bị bỏ qua và yêu cầu gửi lại.
- Checksum là một giá trị số được tính toán từ dữ liệu của 1 gói tin (gồm phần dữ liệu và header của TCP). Khi tạo gói tin TCP, thiết bị gửi sẽ tính toán 1 giá trị checksum, checksum được gắp vào gói tin và gửi đi. Khi thiết bị nhận sẽ tính toán lại checksum nếu khớp thì là không bị lỗi. Cách tính checksum là tổng các phần của gói tin theo từ đoạn 16bit (cụ thể thì có thể tìm hiểu sau)

e. Đảm bảo thứ tự gói tin (Order preservation)

- Đảm bảo các gói tin đến đúng thứ tự, ngay cả khi chúng đi qua các tuyến đường khác nhau trong mạng. Mỗi gói tin TCP đều có 1 sequence number (số thứ tự) giúp đảm bảo dữ liệu được tái hợp đúng cách ở đích.

f. Khôi phục sau lỗi (Error recovery)

- Nếu 1 gói tin bị mất, bị lỗi hoặc không nhận được xác nhận, TCP sẽ yêu cầu truyền lại gói tin đó

g. Đóng kết nối (Connection termination)

- Khi truyền dữ liệu xong, TCP sẽ đóng kết nối giữa hai thiết bị qua một quy trình gọi là four-way handshake.
    1. FIN: Thiết bị A gửi 1 gói FIN (Finish) để yêu cầu kết thúc kết nối.
    2. ACK: Thiết bị B xác nhận yêu cầu kết thúc bằng cách gửi lại 1 gói ACK.
    3. FIN: Thiết bị B gửi gói FIN của chính nó để yêu cầu kết thúc phía của nó.
    4. ACKL Thiết bị A gửi 1 gói ACK cuối cùng, xác nhận kết nối đã được đóng.

**4. Các tầng trong mô hình TCP/IP**

**Tầng 4 - Application Layer (Tầng ứng dụng)**

**Tầng Ứng dụng (Application Layer) trong Mô hình TCP/IP**

Trong mô hình TCP/IP, tầng Ứng dụng là tầng cao nhất và có vai trò cực kỳ quan trọng trong việc cung cấp giao diện cho các ứng dụng để truy cập vào các dịch vụ mạng. Tầng này không chỉ đảm nhận trách nhiệm cung cấp các dịch vụ cho các ứng dụng mà còn giúp đơn giản hóa quá trình trao đổi thông tin giữa người dùng và mạng.

**Chức năng chính của Tầng Ứng dụng**
1. **Truy cập tài nguyên mạng:**
   - Cho phép người dùng và các ứng dụng truy cập vào tài nguyên mạng, như trang web, email, cơ sở dữ liệu, và file.

2. **Xử lý giao thức đặc thù ứng dụng:**
   - Điều phối và sử dụng các giao thức cụ thể để hỗ trợ các hoạt động như truyền thư điện tử, chuyển file, và xử lý truy vấn từ xa.

3. **Cung cấp các API mạng:**
   - Cung cấp giao diện lập trình ứng dụng (APIs) cho phép phần mềm ứng dụng tương tác trực tiếp với các lớp thấp hơn trong mô hình TCP/IP, qua đó giúp lập trình viên dễ dàng phát triển các ứng dụng mạng.

**Giao thức phổ biến của Tầng Ứng dụng**
1. **HTTP (HyperText Transfer Protocol):**
   - Là giao thức nền tảng cho World Wide Web, quản lý truyền thông giữa trình duyệt web và máy chủ web.

2. **FTP (File Transfer Protocol):**
   - Dùng để chuyển file giữa máy khách và máy chủ trên một mạng máy tính.

3. **SMTP (Simple Mail Transfer Protocol):**
   - Được sử dụng để truyền email giữa các máy chủ thư điện tử.

4. **DNS (Domain Name System):**
   - Chuyển đổi giữa tên miền và địa chỉ IP, cho phép người dùng và ứng dụng truy cập mạng dễ dàng hơn.

5. **DHCP (Dynamic Host Configuration Protocol):**
   - Tự động cấp phát địa chỉ IP và thông tin cấu hình mạng cho máy khách trong một mạng.

6. **POP3/IMAP (Post Office Protocol / Internet Message Access Protocol):**
   - Dùng cho việc truy xuất email từ máy chủ thư, cho phép người dùng đọc thư mà không cần phải online.

**Vai trò và Tác động của Tầng Ứng dụng**
- **Giao tiếp người dùng cuối:** Là tầng mà người dùng tương tác trực tiếp thông qua các ứng dụng, làm điểm truy cập cho các tài nguyên và dịch vụ mạng.
- **Hỗ trợ đa dạng các ứng dụng:** Từ duyệt web, email, truyền file, và truyền thông điện tử, tầng Ứng dụng hỗ trợ một loạt các ứng dụng khác nhau, giúp đáp ứng nhu cầu ngày càng cao của người dùng và doanh nghiệp.

------------

- Các giao thức trong tầng ứng dụng: HTTP, HTTPS, FTP, DNS, SSH, DHCP...

a. Cung cấp các dịch vụ và giao diện cho người dùng hoặc các ứng dụng

  - Chịu trách nhiệm trực tiếp xử lý các yêu cầu và phản hồi của người dùng. VD tải trang web, gửi email, truyền tải dữ liệu.
  - Application Layer định nghĩa các giao thức ứng dụng để các ứng dụng có thể giao tiếp qua mạng.

b. Quản lý các giao thức mạng

  - Chứa các giao thức mạng cần thiết cho việc trao đổi thông tin giữa các thiết bị và ứng dụng trong mạng.
  - Các giao thức này hoạt động như 1 cầu nối giữa các ứng dụng và tầng vận chuyển (TCP/UDP)

c. Chuyển đổi dữ liệu giữa các ứng dụng

  - Chuyển đổi dữ liệu giữa các ứng dụng người dùng và các tầng thấp hơn trong mô hình mạng
  - Application Layer cũng có thể chuyển đổi định dạng dữ liệu, mã hóa, giải mã, nén và giải nén dữ liệu khi cần thiết.

------------------------------

**Tầng 3 - Transport Layer (Tầng vận chuyển)**

**Tầng Giao vận (Transport Layer) trong Mô hình TCP/IP**

Tầng Giao vận, hay còn gọi là Transport Layer, là lớp thứ tư trong mô hình TCP/IP, có nhiệm vụ quan trọng trong việc đảm bảo dữ liệu được truyền đi một cách tin cậy giữa các ứng dụng trên các thiết bị mạng. Tầng này cung cấp các dịch vụ kết nối từ điểm đến điểm, điều khiển lỗi, và quản lý luồng dữ liệu để giảm thiểu tình trạng mất mát và đảm bảo tính toàn vẹn của dữ liệu.

**Chức năng chính của Tầng Giao vận**
1. **Đa hóa kết nối (Multiplexing):**
   - Cho phép nhiều ứng dụng trên một thiết bị sử dụng cùng một kết nối mạng mà không gây xung đột, bằng cách gán các cổng riêng biệt cho từng phiên ứng dụng.

2. **Điều khiển phiên (Session Control):**
   - Quản lý phiên làm việc giữa các ứng dụng, đảm bảo rằng dữ liệu gửi đến là liên tục và đúng thứ tự.

3. **Kiểm soát lỗi (Error Control):**
   - Sử dụng các kỹ thuật như kiểm tra checksum và báo cáo xác nhận để phát hiện và sửa lỗi trong quá trình truyền dữ liệu.

4. **Kiểm soát luồng (Flow Control):**
   - Điều chỉnh tốc độ truyền dữ liệu giữa người gửi và người nhận để tránh làm quá tải bộ đệm của người nhận.

5. **Kiểm soát tắc nghẽn (Congestion Control):**
   - Giảm tốc độ truyền khi mạng bị tắc nghẽn để ngăn chặn mất dữ liệu và cải thiện hiệu suất mạng.

**Giao thức phổ biến của Tầng Giao vận**
1. **TCP (Transmission Control Protocol):**
   - Giao thức định hướng kết nối, cung cấp dịch vụ truyền dữ liệu đáng tin cậy. TCP đảm bảo rằng mọi gói tin đều được gửi tới điểm đích một cách chính xác và theo đúng thứ tự.

2. **UDP (User Datagram Protocol):**
   - Giao thức không định hướng kết nối, cung cấp một dịch vụ truyền dữ liệu nhanh nhưng không đáng tin cậy. UDP phù hợp với các ứng dụng đòi hỏi tốc độ cao và có thể chấp nhận một số mất mát dữ liệu, như trò chơi trực tuyến hoặc truyền phát video.

**Vai trò và Tác động của Tầng Giao vận**
- **Đảm bảo tính đáng tin cậy:** TCP và các giao thức khác tại tầng này đảm bảo dữ liệu được gửi một cách đáng tin cậy, ngay cả trong điều kiện mạng không ổn định.
- **Hỗ trợ đa dạng các ứng dụng:** Từ duyệt web, gửi email, chơi game đến truyền phát video, tầng Giao vận cung cấp các giao thức hỗ trợ cho nhiều loại hình ứng dụng trên Internet.


----------

- Chịu trách nhiệm về việc truyền tải dữ liệu giữa các thiết bị đầu cuối qua mạng.

Chức năng chính của Transport Layer

a. Chia nhỏ và tái hợp dữ liệu

- Tầng vận chuyển chia dữ liệu từ ứng dụng thành các segments được đánh số thứ tự. Các segments này sau đó được truyền qua mạng và sẽ được tái hợp tại thiết bị nhận.

b. Quản lý kết nối

- Quyết định có nên tạo kết nối giữa các thiết bị hay không (VD TCP) và đảm bảo sự ổn định của kết nối trong suốt quá trình truyền tải.
- Các giao thức trong transport layer hỗ trợ 2 phương thức kết nối chính: TCP và UDP

c. Đảm bảo tính toàn vẹn của dữ liệu

- Sử dụng checksum để kiểm tra tính toàn vẹn của dữ liệu

d. Kiểm soát lưu lượng

- Tránh tình trạng tắc nghẽn mạng

e. Quản lý lỗi

- TCP có khả năng phát hiện lỗi và y/c gửi lại dữ liệu nếu phát hiện lỗi
- UDP không có

--------------------------------------------------------


**Tầng 2 - Internet Layer (Tầng Mạng)**

**Tầng Internet (Internet Layer) trong Mô hình TCP/IP**

Tầng Internet, còn được gọi là Network Layer trong một số tài liệu, là lớp thứ ba trong mô hình TCP/IP. Nó chịu trách nhiệm chính trong việc định tuyến gói tin qua các mạng khác nhau để đảm bảo chúng đến được đích cuối cùng. Lớp này giúp xác định lộ trình tốt nhất cho dữ liệu di chuyển qua mạng Internet phức tạp.

**Chức năng chính của Tầng Internet**
1. **Định tuyến (Routing):**
   - Chọn lộ trình tối ưu cho gói tin từ nguồn đến đích, dựa trên thông tin định tuyến có sẵn và thuật toán định tuyến. Gói tin có thể đi qua nhiều mạng khác nhau để đến đích.

2. **Địa chỉ hóa logic:**
   - Sử dụng địa chỉ IP để xác định mỗi thiết bị trên mạng. Địa chỉ này giúp xác định vị trí của nguồn và đích trên mạng rộng lớn.

3. **Phân mảnh và tái lắp ráp gói tin:**
   - Chia nhỏ gói tin lớn thành các phân đoạn nhỏ hơn nếu kích thước gói tin vượt quá Maximum Transmission Unit (MTU) của mạng mà chúng đi qua. Các phân đoạn này được tái lắp ráp khi đến nơi nhận.

4. **Xử lý lỗi và thông điệp điều khiển:**
   - Sử dụng các giao thức như ICMP (Internet Control Message Protocol) để xử lý thông báo lỗi và cung cấp thông tin về tình trạng mạng, như thông báo lỗi truyền tải, thời gian sống của gói tin (TTL) đã hết, và các vấn đề khác.

**Giao thức phổ biến của Tầng Internet**
1. **IP (Internet Protocol):**
   - Là giao thức chính tại tầng này, định dạng gói tin và định tuyến chúng trong mạng.

2. **ICMP (Internet Control Message Protocol):**
   - Được sử dụng để gửi thông điệp lỗi và điều khiển, giúp quản lý và gỡ lỗi trong mạng.

3. **ARP (Address Resolution Protocol):**
   - Dùng để ánh xạ địa chỉ IP với địa chỉ MAC (địa chỉ vật lý), cần thiết cho việc truyền gói tin qua mạng LAN.

4. **RIP (Routing Information Protocol), OSPF (Open Shortest Path First), và BGP (Border Gateway Protocol):**
   - Là các giao thức định tuyến chủ yếu được sử dụng để trao đổi thông tin định tuyến giữa các router.

**Vai trò và Tác động của Tầng Internet**
- **Định tuyến toàn cầu:** Đảm bảo gói tin có thể di chuyển từ bất kỳ nguồn nào đến bất kỳ đích nào trên toàn cầu, qua các mạng khác nhau.
- **Quản lý mạng:** Giám sát và phản hồi các điều kiện mạng, như tắc nghẽn và lỗi kết nối.
- **Độc lập với phần cứng:** Các giao thức hoạt động ở tầng Internet tương thích với nhiều loại phần cứng và mạng, giúp Internet hoạt động liền mạch giữa các môi trường khác nhau.


-------------

 - Cung cấp phương thức định tuyến và chuyển tiếp dữ liệu giữa các thiết bị qua các mạng khác nhau.

Chức năng

a. Định tuyến dữ liệu (Routing)

- Lớp mạng xác định đường đi (route) mà dữ liệu phải đi qua giữa các mạng. Các router trong Internet Layer sẽ quyết định đường đi tốt nhất cho dữ liệu. Đảm bảo dữ liệu có thể vượt qua nhiều mạng khác nhau, từ mạng nội bộ đén mạng công cộng.

b. Addressing

- Sử dụng các địa chỉ IP để xác định và phân biệt các thiết bị trong mạng. Mỗi thiết bị kết nối vào mạng sẽ có 1 địa chỉ IP duy nhất

c. Phân mảnh và tái hợp dữ liệu (Fragmantation and Reassembly)

- Dữ liệu có thể bị phân mảnh tròng quá trình truyền tải qua mạng. Nếu dữ liệu quá lớn để truyền qua 1 mạng với kích thước gói tin tối đa (MTU - Maximum Transmission Unit), lớp mạng sẽ phân dữ liệu thành các gói tin nhỏ hơn
- Các gói tin này sau đó sẽ được tái hợp tại đích để thành dữ liệu đầy đủ.

d. Truyền thông giữa các mạng.

Các giao thức IP, ARP, ICMP, IGMP....

------------------------------

**Tầng 1 - Link Layer (Tầng vật lý)**

**Tầng Liên kết (Link Layer) trong Mô hình TCP/IP**

Tầng Liên kết, còn được gọi là Link Layer hoặc Network Interface Layer trong mô hình TCP/IP, là lớp thấp nhất và đóng vai trò cơ bản trong việc truyền thông dữ liệu trực tiếp giữa các thiết bị trên một mạng cục bộ. Lớp này xử lý các chi tiết về phần cứng và truyền thông vật lý, từ việc đóng gói dữ liệu vào các khung (frames) cho đến việc xử lý truyền nhận tín hiệu.

**Chức năng chính của Tầng Liên kết**
1. **Đóng khung (Framing):**
   - Tầng này đóng gói dữ liệu từ tầng trên (Internet Layer) vào trong các khung, bao gồm cả địa chỉ vật lý và thông tin kiểm tra lỗi, để chuẩn bị truyền qua mạng.

2. **Địa chỉ vật lý (Physical Addressing):**
   - Sử dụng địa chỉ MAC (Media Access Control) để xác định nguồn và đích của các khung dữ liệu trên một mạng cục bộ.

3. **Kiểm soát truy cập môi trường (Media Access Control):**
   - Quản lý việc truy cập vào môi trường truyền dẫn chung, đặc biệt là trong mạng nơi mà nhiều thiết bị cùng chia sẻ một kênh vật lý.

4. **Phát hiện và xử lý lỗi (Error Detection and Handling):**
   - Phát hiện lỗi xảy ra trong quá trình truyền dữ liệu (thường thông qua CRC - Cyclic Redundancy Check) và đôi khi sửa chữa các lỗi đó.

5. **Phản hồi tình trạng (Status Reporting):**
   - Báo cáo trạng thái của kết nối và truyền thông về cho tầng trên, bao gồm cả thông tin về lỗi và các vấn đề khác.

**Giao thức phổ biến của Tầng Liên kết**
- **Ethernet (IEEE 802.3):**
   - Phổ biến nhất cho mạng LAN, quy định cách đóng khung dữ liệu và quản lý truy cập vào môi trường vật lý.
- **Wi-Fi (IEEE 802.11):**
   - Quản lý truy cập không dây và đóng khung dữ liệu trong môi trường không dây.
- **ARP (Address Resolution Protocol):**
   - Dùng để ánh xạ giữa địa chỉ IP và địa chỉ MAC trong một mạng cục bộ.
- **PPP (Point-to-Point Protocol):**
   - Cung cấp đóng khung dữ liệu và kiểm soát kết nối trên các liên kết điểm-đến-điểm, thường được sử dụng trong kết nối Internet qua modem.

**Vai trò và Tác động của Tầng Liên kết**
- **Đảm bảo giao tiếp trên mạng cục bộ:** Là tầng trực tiếp xử lý giao tiếp giữa các thiết bị trong một mạng, đảm bảo rằng dữ liệu được gửi và nhận một cách chính xác.
- **Cung cấp cơ sở cho các lớp cao hơn:** Làm nền tảng cho tầng Internet để thực hiện định tuyến dữ liệu giữa các mạng khác nhau.
- **Độc lập với phương tiện truyền dẫn:** Có thể hoạt động trên nhiều loại phương tiện truyền dẫn khác nhau, từ cáp đồng trục, cáp quang đến không gian không dây.


-----------------------

- Tương đương với Tầng Liên Kết Dữ Liệu (Data Link Layer) trong mô hình OSI.

Chức năng

a. Đóng gói dữ liệu thành frame

- Dữ liệu được truyền từ Network Layer sẽ được đóng gói thành các frame trong Link Layer
- frame chứa nhiều thành phần như địa chỉ MAC nguồn và đích, dữ liệu, thông tin kiểm tra lỗi (CRC)
- frame giúp truyền dữ liệu qua mạng vật lý từ thiết bị này sang thiết bị khác.

b. Địa chỉ MAC

- Link Layer sử dụng địa chỉ MAC để xác định thiết bị trong mạng LAN. Các địa chỉ MAC giúp các thiết bị trong mạng LAN giao tiếp và xác định thiết bị đích khi gửi dữ liệu.

c. Kiểm tra lỗi

- Lớp này cung cấp cơ chế kiểm tra lỗi để đảm bảo rằng dữ liệu truyền qua mạng không bị hỏng. Các phương pháp phổ biến như CRC (Cyclic Redundancy Check) được sử dụng để kiểm tra tính toàn vẹn của dữ liệu.
- Nếu phát hiện lỗi, các frame bị lỗi sẽ bị loại bỏ, và yêu cầu gửi lại có thể được đưa ra (tùy thuộc vào giao thức).

d. Điều khiển truy cập phương tiện (Media Access Control - MAC)

- Lớp Liên Kết Dữ Liệu kiểm soát việc các thiết bị trong mạng LAN truy cập phương tiện truyền dẫn (như cáp đồng, cáp quang, sóng vô tuyến) để tránh xung đột khi nhiều thiết bị truyền tải đồng thời.
- Một số giao thức như CSMA/CD trong Ethernet hoặc CSMA/CA trong Wi-Fi được sử dụng để điều khiển quyền truy cập vào phương tiện.

e. Quản lý luồng (Flow Control)

- Kiểm soát tốc độ truyền tải dữ liệu giữa các thiết bị để tránh tình trạng tắc nghẽn hoặc mất mát dữ liệu.
- Điều này đặc biệt quan trọng trong các mạng có băng thông hạn chế.

Các giao thức....

------------------------

### **UDP(User Datagram Protocol)**


UDP, viết tắt của User Datagram Protocol, là một trong những giao thức cơ bản trong bộ giao thức TCP/IP, hoạt động ở tầng Giao vận (Transport Layer). Đây là giao thức không định hướng kết nối, nghĩa là nó không thiết lập một kết nối ổn định trước khi truyền dữ liệu, và cũng không đảm bảo rằng dữ liệu gửi đi sẽ được nhận chính xác tại điểm đích. Do tính chất nhanh và hiệu quả của nó, UDP thường được sử dụng trong các ứng dụng đòi hỏi truyền dữ liệu thời gian thực như video, âm thanh trong cuộc gọi VoIP, trò chơi trực tuyến và nhiều hệ thống phát sóng trực tiếp.

**Chức năng chính của UDP**
1. **Truyền dữ liệu nhanh và hiệu quả:**
   - UDP bỏ qua các bước thiết lập kết nối, kiểm soát luồng và sửa lỗi, cho phép dữ liệu được truyền nhanh chóng mà không cần chờ đợi xác nhận từ đầu nhận.

2. **Không đảm bảo truyền tin:**
   - Không đảm bảo dữ liệu gửi đi sẽ đến được nơi nhận hay đến trong trạng thái nguyên vẹn. Dữ liệu có thể bị mất hoặc sai lệch mà không được phát hiện hoặc sửa chữa.

3. **Không duy trì trạng thái:**
   - UDP không duy trì trạng thái kết nối giữa các lần trao đổi thông tin, giúp giảm tải cho máy chủ vì không cần theo dõi trạng thái của các kết nối.

4. **Đa hóa:**
   - Sử dụng cổng để phân biệt các ứng dụng khác nhau trên cùng một máy, cho phép nhiều ứng dụng sử dụng UDP cùng một lúc.

**Giao thức và Ứng dụng sử dụng UDP**
- **DNS (Domain Name System):**
   - Sử dụng UDP cho các truy vấn thông tin nhanh chóng về địa chỉ IP từ tên miền.
  
- **DHCP (Dynamic Host Configuration Protocol):**
   - Giao thức cấp phát địa chỉ IP động sử dụng UDP để trao đổi thông tin cấu hình mạng nhanh chóng.
  
- **SNMP (Simple Network Management Protocol):**
   - Dùng UDP để giám sát và quản lý thiết bị mạng với lưu lượng thấp và yêu cầu độ trễ thấp.

- **VoIP (Voice over Internet Protocol) và truyền phát video:**
   - Các ứng dụng cần truyền tải dữ liệu âm thanh và video thời gian thực thường sử dụng UDP để giảm độ trễ.

**Ưu và Nhược điểm của UDP**
- **Ưu điểm:**
   - **Tốc độ cao:** Việc không có cơ chế kiểm soát tạo điều kiện cho truyền tải dữ liệu nhanh chóng.
   - **Đơn giản:** Cấu trúc gọn nhẹ, ít tốn tài nguyên hệ thống.

- **Nhược điểm:**
   - **Không đáng tin cậy:** Không có kiểm soát lỗi, không đảm bảo rằng dữ liệu gửi đi sẽ đến nơi nhận.
   - **Thiếu kiểm soát luồng:** Dữ liệu có thể bị mất nếu phía nhận không kịp xử lý.
  

-----------

- Là giao thức truyền tải dữ liệu không kết nối. Hoạt động ở Transport Layer trong OSI. UDP cho phép truyền tải dữ liệu dưới dạng các gói (datagrams), không yêu cầu kết nối giữa các máy gửi và nhận. Không đảm bảo tính toàn vẹn của dữ liệu, không kiểm tra lỗi và không xác nhận việc nhận gói dữ liệu.

**2. Cơ chế hoạt động của UDP:**  
- **Không kết nối**: UDP không cần thiết lập kết nối trước khi truyền tải dữ liệu. Dữ liệu được gửi ngay lập tức dưới dạng các gói độc lập.
- **Không đảm bảo thứ tự**: Các gói dữ liệu có thể đến theo một thứ tự khác với thứ tự ban đầu mà chúng được gửi đi.
- **Không kiểm tra lỗi**: UDP không thực hiện kiểm tra lỗi hay xác nhận gói dữ liệu. Nếu có mất gói hoặc lỗi trong quá trình truyền tải, UDP không thực hiện các biện pháp để sửa chữa.
- **Gửi gói độc lập**: Mỗi gói dữ liệu là một đơn vị độc lập, không có sự liên kết với các gói khác.
- **Không đảm bảo độ tin cậy**: UDP không cung cấp bất kỳ cơ chế nào để đảm bảo gói dữ liệu được nhận đúng hoặc không bị mất trong quá trình truyền.

**3. Khi nào dùng UDP?**  
- **Ứng dụng yêu cầu tốc độ cao và độ trễ thấp**: UDP là lựa chọn tốt cho các ứng dụng cần truyền tải nhanh chóng mà không quan tâm đến việc kiểm tra lỗi hoặc độ tin cậy của dữ liệu.
- **Ứng dụng có thể chịu được mất gói**: Các ứng dụng không yêu cầu hoàn chỉnh dữ liệu và có thể chịu đựng việc mất mát một số gói dữ liệu.
- **Truyền thông thời gian thực**: Đặc biệt trong các tình huống như cuộc gọi thoại hay video streaming, nơi độ trễ thấp và sự liên tục trong truyền tải dữ liệu quan trọng hơn là đảm bảo rằng tất cả các gói dữ liệu đều đến được.
- **Các ứng dụng phát trực tiếp (streaming)**: Dữ liệu có thể được truyền đi liên tục, và các gói mất mát có thể dễ dàng bỏ qua mà không gây ảnh hưởng lớn đến trải nghiệm người dùng.

**4. Các dịch vụ phổ biến dùng UDP:**
- **Video Streaming**: Các dịch vụ như YouTube, Netflix có thể sử dụng UDP cho việc phát video trực tuyến. Nếu một vài gói bị mất, chúng có thể được bỏ qua mà không làm gián đoạn quá trình phát.
- **Voice over IP (VoIP)**: Các cuộc gọi VoIP như Skype, Zoom sử dụng UDP vì yêu cầu về độ trễ thấp và khả năng truyền tải dữ liệu âm thanh nhanh chóng mà không quan tâm đến việc mất một vài gói.
- **Online Gaming**: Các trò chơi trực tuyến như Fortnite, PUBG sử dụng UDP để giảm độ trễ và đảm bảo việc truyền tải nhanh chóng các lệnh và thông tin trong thời gian thực.
- **DNS (Domain Name System)**: Khi bạn yêu cầu dịch vụ DNS (tra cứu tên miền), giao thức UDP thường được sử dụng để nhanh chóng gửi và nhận yêu cầu tra cứu mà không cần thiết lập kết nối dài hạn.
- **TFTP (Trivial File Transfer Protocol)**: Đây là một giao thức truyền tệp đơn giản, sử dụng UDP để truyền tệp mà không yêu cầu các tính năng như xác nhận hoặc kiểm tra lỗi.

--------------


### **TCP (Transmission Control Protocol)



---------

**1. TCP là gì?**
**TCP (Transmission Control Protocol)** là một giao thức truyền tải dữ liệu có kết nối, hoạt động tại tầng vận chuyển (Transport Layer) trong mô hình OSI. TCP đảm bảo rằng các gói dữ liệu được truyền một cách đáng tin cậy và theo thứ tự, bảo vệ tính toàn vẹn của dữ liệu. Khi một kết nối TCP được thiết lập, nó sẽ duy trì sự ổn định và bảo mật trong suốt quá trình truyền tải, sử dụng các cơ chế kiểm tra lỗi và xác nhận dữ liệu.

**2. Cơ chế hoạt động của TCP**
**a. Kết nối đầy đủ (Three-way Handshake)**
Trước khi truyền dữ liệu, TCP thiết lập một kết nối bằng quá trình gọi là **three-way handshake**. Quá trình này gồm ba bước:
1. **SYN (Synchronize)**: Máy gửi gửi một gói SYN yêu cầu thiết lập kết nối với máy nhận.
2. **SYN-ACK (Synchronize-Acknowledge)**: Máy nhận trả lời với một gói SYN-ACK để xác nhận yêu cầu kết nối.
3. **ACK (Acknowledge)**: Máy gửi gửi một gói ACK xác nhận kết nối đã được thiết lập và quá trình truyền tải có thể bắt đầu.

**b. Truyền tải dữ liệu và bảo mật**
- **Xác nhận (Acknowledgment)**: Mỗi gói dữ liệu khi nhận được sẽ được xác nhận bằng một gói ACK. Máy nhận sẽ gửi lại một gói ACK đến máy gửi để thông báo rằng dữ liệu đã được nhận đúng.
- **Kiểm tra lỗi (Error Checking)**: TCP sử dụng kiểm tra lỗi (checksum) để đảm bảo rằng dữ liệu không bị lỗi trong quá trình truyền. Nếu có lỗi trong gói dữ liệu, TCP sẽ yêu cầu máy gửi gửi lại gói đó.
- **Điều khiển lưu lượng (Flow Control)**: TCP sử dụng một cơ chế điều khiển lưu lượng để điều chỉnh tốc độ truyền tải dữ liệu, đảm bảo máy nhận không bị quá tải.
- **Điều khiển tắc nghẽn (Congestion Control)**: TCP cũng có cơ chế giảm tốc độ truyền tải nếu xảy ra tắc nghẽn mạng, tránh làm mạng bị quá tải.

**c. Truyền tải dữ liệu theo thứ tự**
TCP đảm bảo rằng các gói dữ liệu được tái sắp xếp theo đúng thứ tự mà chúng được gửi đi, ngay cả khi chúng đến nơi không theo thứ tự. Điều này giúp đảm bảo rằng người nhận sẽ nhận dữ liệu theo đúng thứ tự mà máy gửi mong muốn.

**d. Kết thúc kết nối (Four-way Handshake)**
Khi quá trình truyền tải dữ liệu kết thúc, kết nối TCP được đóng lại bằng một quy trình gọi là **four-way handshake**:
1. Máy gửi gửi một gói FIN (Finish) để yêu cầu đóng kết nối.
2. Máy nhận gửi lại một gói ACK xác nhận đã nhận yêu cầu.
3. Máy nhận gửi một gói FIN để kết thúc kết nối.
4. Máy gửi gửi lại một gói ACK để xác nhận kết nối đã đóng hoàn tất.

**3. Khi nào dùng TCP?**
TCP được sử dụng trong các tình huống và ứng dụng cần:
- **Độ tin cậy cao và bảo vệ dữ liệu**: TCP đảm bảo rằng dữ liệu sẽ được truyền đúng đắn, không mất mát và theo thứ tự. Điều này rất quan trọng đối với các ứng dụng như gửi email, tải tệp tin, hoặc các giao dịch tài chính.
- **Truyền tải dữ liệu theo kết nối**: Các ứng dụng yêu cầu một kết nối ổn định trong suốt quá trình truyền tải sẽ sử dụng TCP, vì giao thức này duy trì kết nối trong suốt phiên làm việc.
- **Ứng dụng không thể chịu mất dữ liệu**: Các ứng dụng yêu cầu toàn vẹn dữ liệu và không thể chấp nhận mất mát, ví dụ như giao dịch ngân hàng, các kết nối cơ sở dữ liệu, hoặc truyền tải tệp tin quan trọng.
- **Điều khiển tắc nghẽn và lưu lượng**: Các mạng có mật độ truy cập cao sẽ sử dụng TCP để đảm bảo không bị tắc nghẽn và điều chỉnh lưu lượng truyền tải phù hợp.

**4. Các dịch vụ phổ biến dùng TCP (chi tiết)**

**a. Web Browsing (HTTP/HTTPS)**
- **Cách hoạt động**: Giao thức HTTP (HyperText Transfer Protocol) và HTTPS (HTTP Secure) được sử dụng trong duyệt web. Khi bạn truy cập một trang web, trình duyệt gửi yêu cầu HTTP/HTTPS đến máy chủ và nhận lại nội dung trang web (HTML, hình ảnh, video, v.v.).
- **Lý do dùng TCP**: Web duyệt yêu cầu một kết nối ổn định và đảm bảo rằng tất cả các tài nguyên trên trang web được tải đúng đắn và không bị mất mát. TCP đảm bảo rằng tất cả các gói dữ liệu (trang web, hình ảnh, v.v.) được truyền tải theo thứ tự và đầy đủ.

**b. Email (SMTP, IMAP, POP3)**
- **Cách hoạt động**: Các giao thức gửi và nhận email như **SMTP (Simple Mail Transfer Protocol)**, **IMAP (Internet Message Access Protocol)** và **POP3 (Post Office Protocol)** đều sử dụng TCP để đảm bảo email được gửi và nhận một cách chính xác.
- **Lý do dùng TCP**: Email yêu cầu tính toàn vẹn dữ liệu cao và không thể chấp nhận việc mất mát thư. TCP đảm bảo rằng mọi thông tin gửi đi được bảo vệ và đảm bảo sự ổn định trong quá trình giao tiếp giữa các máy chủ email.

**c. File Transfer (FTP)**
- **Cách hoạt động**: **FTP (File Transfer Protocol)** là giao thức cho phép truyền tệp giữa các máy tính. Nó sử dụng TCP để truyền tải tệp, đảm bảo tính toàn vẹn và chính xác của dữ liệu.
- **Lý do dùng TCP**: Việc truyền tệp cần đảm bảo rằng dữ liệu không bị mất và được truyền đầy đủ, đúng thứ tự. TCP cung cấp các cơ chế kiểm tra lỗi và xác nhận gói dữ liệu đã nhận.

**d. Remote Desktop (RDP)**
- **Cách hoạt động**: **RDP (Remote Desktop Protocol)** cho phép người dùng kết nối từ xa vào máy tính khác và điều khiển nó như thể đang ngồi trước máy. RDP sử dụng TCP để duy trì kết nối ổn định giữa các thiết bị.
- **Lý do dùng TCP**: Để điều khiển máy tính từ xa, yêu cầu phải có một kết nối ổn định và đáng tin cậy, đảm bảo rằng mọi thao tác từ xa được thực hiện chính xác.

**e. Database Connections (SQL)**
- **Cách hoạt động**: Các ứng dụng kết nối với cơ sở dữ liệu, ví dụ như MySQL, SQL Server, Oracle, sử dụng TCP để truy vấn và trả về kết quả từ cơ sở dữ liệu.
- **Lý do dùng TCP**: Các giao dịch cơ sở dữ liệu yêu cầu độ tin cậy cao và không thể chấp nhận mất mát dữ liệu. TCP giúp duy trì một kết nối ổn định và bảo vệ tính toàn vẹn của dữ liệu.

**f. VoIP (Voice over IP)**
- **Cách hoạt động**: **VoIP (Voice over IP)** là công nghệ cho phép gọi thoại qua Internet. Dù UDP thường được sử dụng cho VoIP vì tính hiệu quả và độ trễ thấp, nhưng một số hệ thống VoIP vẫn sử dụng TCP trong các trường hợp yêu cầu độ tin cậy cao và bảo mật.
- **Lý do dùng TCP**: Khi cần bảo mật và ổn định trong quá trình gọi thoại, TCP có thể được sử dụng. Điều này đặc biệt quan trọng trong các ứng dụng VoIP cho các cuộc gọi doanh nghiệp hoặc các giao dịch yêu cầu bảo mật.

**g. SSH (Secure Shell)**
- **Cách hoạt động**: **SSH (Secure Shell)** là một giao thức bảo mật cho phép người dùng kết nối từ xa vào hệ thống máy tính. SSH sử dụng TCP để mã hóa và bảo vệ các kết nối.
- **Lý do dùng TCP**: SSH yêu cầu bảo mật và tính toàn vẹn cao, vì các kết nối này thường liên quan đến quyền truy cập hệ thống và điều khiển máy tính từ xa.

----------------


### **IPv4**

**1. Cấu trúc địa chỉ IPv4**
Địa chỉ **IPv4** (Internet Protocol version 4) là một địa chỉ 32 bit, được biểu diễn dưới dạng 4 phần, mỗi phần là một số nguyên từ 0 đến 255, cách nhau bằng dấu chấm, ví dụ: `192.168.1.1`.

- **Định dạng**: `X.X.X.X`, trong đó mỗi `X` là một số từ 0 đến 255 (biểu diễn trong hệ thập phân), nhưng thực tế mỗi số này đại diện cho một octet (tám bit), vì vậy mỗi phần có giá trị từ `0000 0000` đến `1111 1111` trong hệ nhị phân.
- **Số bit**: IPv4 sử dụng 32 bit (4 x 8 bit), được chia thành 4 phần, mỗi phần là 1 octet (8 bit).

**Ví dụ**: Địa chỉ IPv4 `192.168.1.1` có dạng nhị phân là:
- `192` → `11000000`
- `168` → `10101000`
- `1`   → `00000001`
- `1`   → `00000001`

**2. Phân loại địa chỉ IPv4**
Các địa chỉ IPv4 được phân loại thành các lớp khác nhau dựa trên phạm vi và mục đích sử dụng, bao gồm **Class A**, **Class B**, **Class C**, **Class D**, và **Class E**.

**loopback** 

- được sử dụng để gửi dữ liệu quay lại chính thiết bị mà không phải rời khỏi máy tính đó. 
- **Dải địa chỉ loopback IPv4**: **127.0.0.0/8**
- Điều này có nghĩa là bất kỳ địa chỉ nào trong khoảng từ **127.0.0.0** đến **127.255.255.255** đều là các địa chỉ loopback.
- **Địa chỉ loopback phổ biến nhất**: **127.0.0.1**, thường được gọi là "localhost".
**Tại sao cần địa chỉ loopback?**
- **Kiểm tra kết nối mạng nội bộ**: Địa chỉ loopback giúp kiểm tra kết nối mạng của hệ thống mà không cần phải truy cập mạng thực tế. Ví dụ, bạn có thể kiểm tra xem liệu phần mềm mạng (như một máy chủ web) có hoạt động đúng trên chính máy tính của bạn hay không mà không cần phải kết nối ra ngoài.
- **Chạy ứng dụng mạng**: Các ứng dụng và dịch vụ có thể sử dụng địa chỉ loopback để gửi yêu cầu đến chính mình mà không đi qua mạng vật lý, giúp giảm độ trễ và cải thiện hiệu suất.
- **Hỗ trợ cấu hình và thử nghiệm**: Các kỹ thuật viên hoặc nhà phát triển phần mềm có thể sử dụng địa chỉ loopback để kiểm tra cấu hình mạng và các dịch vụ mà không cần thiết bị mạng bên ngoài.

**Các Đặc Điểm của Địa Chỉ Loopback**
- **Không có kết nối vật lý**: Địa chỉ loopback không yêu cầu kết nối vật lý với mạng bên ngoài; nó chỉ sử dụng **giao thức TCP/IP** để giao tiếp trong hệ thống.
- **Được xử lý trong hệ điều hành**: Địa chỉ loopback được xử lý bởi hệ điều hành và phần mềm mạng trên chính máy tính đó.
- **Không thể được định tuyến ra ngoài**: Các địa chỉ loopback không thể đi ra ngoài máy tính và không thể được sử dụng trên các mạng ngoài. Tất cả các dữ liệu gửi đến các địa chỉ loopback sẽ không rời khỏi hệ thống.

**a. Phân loại theo Class**
Địa chỉ IPv4 được chia thành các lớp (Class) sau đây:

1. **Class A** (`0.0.0.0` - `127.255.255.255`)
   - **Đặc điểm**: Class A có 8 bit đầu tiên dành cho **phần mạng** và 24 bit còn lại dành cho **phần host**. 
   - **Dải địa chỉ**: Địa chỉ từ `0.0.0.0` đến `127.255.255.255`. Trong đó, `127.0.0.0` đến `127.255.255.255` được dành riêng cho **loopback** (quay lại máy tính của mình).
   - **Số mạng**: 128 mạng (2^7) với khoảng 16 triệu host mỗi mạng (2^24 - 2). 0.0.0.0 dành riêng cho mục đích đặc biệt như chỉ ra mạng hiện tại hoặc làm địa chỉ mặc định. 127.0.0.0/8 được dành riêng cho các địa chỉ loopback, không dùng làm địa chỉ mạng thực tế.
    
   - **Ứng dụng**: Lớp A được dùng cho các tổ chức lớn cần nhiều địa chỉ IP cho các thiết bị trong mạng của mình.

2. **Class B** (`128.0.0.0` - `191.255.255.255`)
   - **Đặc điểm**: Class B có 16 bit đầu tiên dành cho **phần mạng** và 16 bit còn lại dành cho **phần host**.
   - **Dải địa chỉ**: Địa chỉ từ `128.0.0.0` đến `191.255.255.255`.
   - **Số mạng**: 16,384 mạng (2^14) với khoảng 65,534 host mỗi mạng (2^16 - 2).
   - **Ứng dụng**: Dành cho các tổ chức vừa và lớn, cần số lượng host vừa phải trong mỗi mạng.

3. **Class C** (`192.0.0.0` - `223.255.255.255`)
   - **Đặc điểm**: Class C có 24 bit đầu tiên dành cho **phần mạng** và 8 bit còn lại dành cho **phần host**.
   - **Dải địa chỉ**: Địa chỉ từ `192.0.0.0` đến `223.255.255.255`.
   - **Số mạng**: 2 triệu mạng (2^21) với khoảng 254 host mỗi mạng (2^8 - 2).
   - **Ứng dụng**: Lớp C được sử dụng cho các mạng nhỏ hơn, như các mạng văn phòng hoặc doanh nghiệp nhỏ.

4. **Class D** (`224.0.0.0` - `239.255.255.255`)
   - **Đặc điểm**: Class D được dùng cho **multicast** (truyền tải thông tin đến nhóm nhiều thiết bị).
   - **Dải địa chỉ**: Địa chỉ từ `224.0.0.0` đến `239.255.255.255`.
   - **Ứng dụng**: Dùng cho các ứng dụng như phát sóng video hoặc thoại qua Internet (VoIP).

5. **Class E** (`240.0.0.0` - `255.255.255.255`)
   - **Đặc điểm**: Class E dành cho các mục đích thử nghiệm và nghiên cứu, không được sử dụng rộng rãi trong mạng công cộng.
   - **Dải địa chỉ**: Địa chỉ từ `240.0.0.0` đến `255.255.255.255`.
   - **Ứng dụng**: Dành cho các nghiên cứu hoặc thử nghiệm của các nhà phát triển mạng.

**b. Địa chỉ công cộng và địa chỉ riêng**
- **Địa chỉ công cộng**: Đây là địa chỉ có thể truy cập trực tiếp từ Internet và được cấp phát bởi các nhà cung cấp dịch vụ mạng (ISP). Những địa chỉ này không bị giới hạn trong mạng nội bộ.
- **Địa chỉ riêng (Private IP)**: Là địa chỉ được sử dụng trong các mạng nội bộ (LAN), không thể truy cập từ Internet. Các địa chỉ riêng thuộc các dải sau:
  - **Class A**: `10.0.0.0` đến `10.255.255.255`
  - **Class B**: `172.16.0.0` đến `172.31.255.255`
  - **Class C**: `192.168.0.0` đến `192.168.255.255`
  
- **Địa chỉ loopback** (`127.0.0.0` đến `127.255.255.255`): Dùng để gửi các gói tin từ máy tính đến chính nó, thường được sử dụng để kiểm tra các kết nối mạng trong máy tính.

**c. Địa chỉ Broadcast**
- **Địa chỉ Broadcast** được dùng để gửi dữ liệu đến tất cả các thiết bị trong một mạng. Địa chỉ broadcast có dạng `X.X.X.255`, trong đó `X.X.X` là địa chỉ mạng. Ví dụ: `192.168.1.255` là broadcast cho mạng `192.168.1.0`.

**d. Địa chỉ Multicast**
- **Multicast** là một phương thức truyền dữ liệu đến một nhóm các thiết bị, không phải tất cả các thiết bị trong mạng. Địa chỉ multicast nằm trong dải từ `224.0.0.0` đến `239.255.255.255`.

**3. Chia địa chỉ IPv4 (Subnetting)**
Quá trình **Subnetting** là việc chia một mạng lớn thành nhiều mạng nhỏ hơn. Điều này giúp tối ưu hóa việc sử dụng địa chỉ IP và tổ chức mạng một cách hợp lý hơn.

**a. Subnet Mask**
- **Subnet Mask** giúp xác định phần mạng và phần host trong một địa chỉ IP. Đây là một giá trị 32-bit, với phần mạng có giá trị 1 và phần host có giá trị 0.
  
**Ví dụ**:
- **IP**: `192.168.1.1`
- **Subnet Mask**: `255.255.255.0` (biểu diễn nhị phân là `11111111.11111111.11111111.00000000`).

Với subnet mask `255.255.255.0`, ta biết rằng 24 bit đầu tiên là phần mạng, còn 8 bit cuối cùng là phần host. Điều này có nghĩa là ta có thể chia mạng `192.168.1.0` thành 256 địa chỉ host (từ `192.168.1.0` đến `192.168.1.255`).

**b. CIDR (Classless Inter-Domain Routing)**
- **CIDR** là phương pháp chia địa chỉ linh hoạt hơn so với phân chia theo lớp (Classful). CIDR sử dụng cú pháp `X.X.X.X/bit` để xác định số bit được sử dụng cho phần mạng. Ví dụ: `192.168.1.0/24` có nghĩa là 24 bit đầu tiên được dùng cho phần mạng và 8 bit còn lại dành cho phần host.
  
**Ví dụ**:
- **Địa chỉ IP**: `192.168.1.0`
- **CIDR**: `/24` (tức là 24 bit đầu tiên là phần mạng).

CIDR cho phép chia địa chỉ mạng thành các subnet nhỏ hơn mà không bị ràng buộc bởi các lớp A, B, C.

### **IPv6**

**1. Tổng Quan về Địa chỉ IPv6**
- **Địa chỉ IPv6 có độ dài 128 bit**, tức là 16 byte. Điều này giúp IPv6 có thể hỗ trợ rất nhiều địa chỉ, gấp nhiều lần IPv4.
- Địa chỉ IPv6 được chia thành **8 nhóm 16 bit**, mỗi nhóm được biểu diễn dưới dạng một **chữ số hex** (hệ thập lục phân), và các nhóm được ngăn cách bởi dấu **cột đôi (:)**.

**2. Cấu trúc Địa chỉ IPv6**
Mỗi địa chỉ IPv6 có dạng:
```
xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx
```
- **Mỗi nhóm 4 chữ số hex** tương đương với **16 bit**.
- **Tổng cộng là 128 bit** (8 nhóm x 16 bit = 128 bit).

**Ví dụ**:
Một địa chỉ IPv6 đầy đủ có thể là:
```
2001:0db8:85a3:0000:0000:8a2e:0370:7334
```
**3. Phân chia các thành phần trong địa chỉ IPv6**

Địa chỉ IPv6 có thể bao gồm các thành phần sau:

1. **Network Prefix** (Tiền tố mạng): Phần đầu của địa chỉ IPv6 dùng để xác định mạng, tương tự như phần mạng trong địa chỉ IPv4. Phần này có thể có độ dài từ 0 đến 128 bit, thông thường là **64 bit** cho phần mạng.
   
2. **Interface Identifier** (Mã nhận diện giao diện): Phần còn lại của địa chỉ IPv6 được dùng để xác định một thiết bị cụ thể trong mạng. Phần này có thể có độ dài từ 0 đến 128 bit, thường là **64 bit**.

**4. Cấu trúc cụ thể trong IPv6**
- **Phần mạng** (Network Prefix): Thường chiếm 64 bit đầu tiên trong địa chỉ IPv6.
- **Phần host** (Interface Identifier): Chiếm 64 bit còn lại.

**Ví dụ**:
Địa chỉ IPv6: `2001:0db8:85a3:0000:0000:8a2e:0370:7334/64`
- **Phần mạng**: `2001:0db8:85a3:0000`
- **Phần host**: `0000:8a2e:0370:7334`
- Đổi hex ra nhị phân: 2001 (hex) = 0010 0000 0000 0001 (bin)
- 
**5. Định dạng và Rút gọn Địa chỉ IPv6**

IPv6 cho phép **rút gọn địa chỉ** để giảm độ dài của địa chỉ, bao gồm các quy tắc sau:

1. **Loại bỏ các nhóm toàn 0**: Bạn có thể loại bỏ các nhóm toàn 0 và thay thế bằng **`::`** (chỉ có thể thay thế một lần trong một địa chỉ).

   Ví dụ: 
   ```
   2001:0db8:0000:0000:0000:0000:0000:0001
   ```
   Có thể rút gọn thành:
   ```
   2001:db8::1
   ```

2. **Loại bỏ các số 0 ở đầu mỗi nhóm**: Các chữ số 0 ở đầu của mỗi nhóm có thể bị loại bỏ.

   Ví dụ:
   ```
   2001:0db8:0a00:0000:0000:0000:0001:0001
   ```
   Có thể rút gọn thành:
   ```
   2001:db8:a00::1:1
   ```

**6. Các Loại Địa chỉ IPv6**

IPv6 hỗ trợ ba loại địa chỉ chính:

1. Unicast (Đơn phát)
Địa chỉ Unicast là địa chỉ duy nhất trong một mạng và dùng để gửi dữ liệu từ một thiết bị này đến một thiết bị khác. Nó là địa chỉ "một với một" (one-to-one), nghĩa là dữ liệu chỉ được gửi đến một thiết bị duy nhất.

Cấu trúc: Địa chỉ Unicast có thể có cấu trúc giống như bất kỳ địa chỉ IPv6 nào, nhưng thường không bắt đầu với FF00::/8 (được dành cho Multicast) hay fe80::/10 (dành cho địa chỉ Link-local).
Ví dụ:
2001:db8::1 là một địa chỉ Unicast, chỉ đến một máy chủ duy nhất.
Địa chỉ này có thể là của một thiết bị trong mạng, chẳng hạn như một máy tính, máy chủ hoặc thiết bị mạng.
Mục đích sử dụng: Địa chỉ Unicast là loại địa chỉ phổ biến nhất trong mạng, dùng trong hầu hết các giao tiếp trực tiếp giữa các thiết bị (ví dụ: từ máy tính này sang máy chủ, từ máy tính này sang máy tính khác).

2. Multicast (Đa phát)
Địa chỉ Multicast là loại địa chỉ dùng để gửi thông tin đến một nhóm thiết bị trong mạng. Thông điệp multicast được gửi đến tất cả các thiết bị trong nhóm được chỉ định, thay vì gửi tới từng thiết bị một như trong trường hợp Unicast. Đây là địa chỉ "một với nhiều" (one-to-many).

Cấu trúc: Địa chỉ Multicast bắt đầu với tiền tố FF00::/8.
Ví dụ, các địa chỉ trong phạm vi FF00::/8 được dành riêng cho Multicast.
Một ví dụ về địa chỉ multicast là ff02::1, địa chỉ này được sử dụng để gửi thông điệp đến tất cả các node trong mạng nội bộ (link-local scope).
Mục đích sử dụng:

FF02::1: Địa chỉ này được sử dụng trong mạng nội bộ (link-local) để gửi dữ liệu đến tất cả các thiết bị trong mạng nội bộ.
FF02::2: Địa chỉ multicast này được gửi đến tất cả các router trong mạng nội bộ.
Ví dụ ứng dụng: Địa chỉ multicast rất hữu ích trong việc phát video trực tuyến, truyền tải dữ liệu nhóm (group communication), hoặc trong các ứng dụng VoIP (Voice over IP) khi nhiều thiết bị cần nhận một luồng dữ liệu đồng thời.
3. Anycast (Bất kỳ phát)
Địa chỉ Anycast là loại địa chỉ được sử dụng để gửi thông tin đến một thiết bị trong nhóm thiết bị có địa chỉ gần nhất. Khi một thông điệp được gửi đến một địa chỉ Anycast, nó sẽ được chuyển đến thiết bị có địa chỉ gần nhất (theo định nghĩa của "gần nhất" trong routing, có thể là gần nhất về mặt địa lý hoặc về mặt cấu trúc mạng).

Cấu trúc: Địa chỉ Anycast có thể giống như một địa chỉ Unicast trong mạng, nhưng với định nghĩa đặc biệt trong bảng định tuyến. Một địa chỉ Anycast có thể trông giống như bất kỳ địa chỉ Unicast nào.

Ví dụ: Một ví dụ điển hình là địa chỉ Anycast trong hệ thống DNS. Khi bạn gửi một yêu cầu DNS tới một địa chỉ Anycast, yêu cầu đó sẽ được chuyển đến máy chủ DNS gần nhất về mặt mạng (tức là máy chủ DNS với độ trễ thấp nhất, có thể là máy chủ gần về mặt địa lý hoặc có bảng định tuyến tối ưu).

Ví dụ: Một dịch vụ DNS có thể được triển khai với địa chỉ Anycast, nơi nhiều máy chủ DNS ở các vị trí khác nhau sử dụng cùng một địa chỉ Anycast. Khi bạn gửi một yêu cầu DNS đến địa chỉ này, thông tin sẽ được chuyển tới máy chủ DNS gần nhất.

Mục đích sử dụng:

Anycast chủ yếu được sử dụng trong các dịch vụ mà bạn muốn chuyển hướng yêu cầu đến thiết bị/điểm truy cập gần nhất.

Ứng dụng phổ biến của Anycast có thể thấy trong các dịch vụ như DNS, CDN (Content Delivery Networks), DDoS mitigation (chống tấn công DDoS), nơi yêu cầu sẽ được chuyển đến điểm gần nhất để giảm độ trễ và cải thiện hiệu suất.

**7. Các Phần trong Địa chỉ IPv6**

1. **Địa chỉ Giao thức Internet (Prefix)**:
   - Phần này xác định mạng con của địa chỉ IPv6, và độ dài thường là **64 bit**.

2. **Mã nhận diện giao diện (Interface Identifier)**:
   - Đây là phần xác định một thiết bị trong mạng con. Thông thường, **64 bit cuối cùng** trong địa chỉ IPv6 sẽ là mã nhận diện giao diện.

3. **Prefix Length**:
   - Đây là độ dài của phần mạng trong địa chỉ IPv6, thường được biểu thị bằng `/n`, ví dụ `/64` trong địa chỉ `2001:db8::/64`, nơi 64 bit đầu tiên là phần mạng.

**8. Đặc điểm nổi bật của IPv6**

1. **Không gian địa chỉ lớn**: IPv6 có không gian địa chỉ rất lớn với **128 bit**, điều này giúp giải quyết vấn đề thiếu hụt địa chỉ mà IPv4 gặp phải.

2. **Không cần NAT**: IPv6 không yêu cầu sử dụng **NAT (Network Address Translation)** vì có đủ không gian địa chỉ cho mỗi thiết bị có thể có một địa chỉ IP công cộng riêng biệt.

3. **Tự động cấu hình (SLAAC)**: IPv6 cho phép các thiết bị tự động cấu hình địa chỉ mà không cần sử dụng **DHCP**.

4. **Bảo mật**: IPv6 hỗ trợ **IPsec** (Internet Protocol Security) mặc định, giúp bảo mật kết nối trong suốt quá trình truyền tải dữ liệu.

