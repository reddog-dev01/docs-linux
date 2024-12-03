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

- Không quan tâm đến dữ liệu mà chỉ tập trung vào các phương tiện vật lý và cách thức chúng truyền tín hiệu.

**Lý do cần**: Vì nó cung cấp các phương tiện để truyền tải dữ liệu giữa các thiết bị mạng, đảm bảo dữ liệu được truyền từ nguồn đến đích đúng và hiệu quả. Không có tầng vật lý các tầng trên không thể giao tiếp hoặc trao đổi dữ liệu.

- Chuyển đổi tín hiệu số (0 và 1) từ các tầng trên thành tín hiệu vật lý ( tín hiệu điện, sóng ánh sáng, sóng vô tuyến) để truyền tải qua các phương tiện vật lý (cáp quang, sóng vô tuyến, cáp đồng trục...). Quy định tốc độ truyền tải dữ liệu và băng thông của mạng đảm bảo dữ liệu được truyền đi đúng tốc độ và không bị mất.

**Tầng 2 - Data Link Layer ( Tầng liên kết dữ liệu)**

- Đảm bảo việc truyền tải dữ liệu chính xác và không bị lỗi giữa các thiết bị trong cùng 1 mạng hoặc trên 1 liên kết mạng vật lý. Làm việc với tầng vật lý để đảm bảo rằng dữ liệu được truyền 1 cách an toàn hiệu quả.

**Lý do cần**

- Tầng 2 đảm bảo dữ liệu được gửi đi từ 1 thiết bị đến thiết bị khác không bị lỗi. Nếu có lỗi xảy ra trong quá trình truyền tải nó sẽ phát hiện và sửa lỗi.
- Kiểm soát tốc độ dữ liệu được truyền, tránh tình trạng tắc nghẽn hoặc mất mát dữ liệu.
- Dữ liệu từ tầng 3 được đóng gói thành các frames để có thể được truyền tải qua môi trường vật lý.

**Chức năng của Data Link**

- Data Link nhận dữ liệu từ Network đóng gói thành frames (gồm cả MAC) trong quá trình truyền tải nếu phát hiện lỗi dữ liệu sẽ được sửa hoặc yêu cầu gửi lại. Kiểm soát tốc độ, quản lý truy cập kênh truyền tải để tánh xung đột khi nhiều thiết bị cùng gửi dữ liệu.

**Tầng 3 - Network Layer**

- Định tuyến và điều phối dữ liệu giữa các thiết bị trên các mạng khác nhau.

Network Layer sử dụng các thuật toán định tuyến (routing) để xác định đường đi tốt nhất cho các packets giữa các mạng (sử dụng các thiết bị định tuyến router, switch). Chịu trách nhiệm cấp phát và sử dụng các địa chỉ logic để nhận dạng các thiết bị trong mạng (phổ biến nhất là IP). Nếu packets quá lớn để truyền qua mạng nó sẽ phân mảnh chúng thành các phần nhỏ hơn để có thể gửi qua mạng, khi đến đích, các mảnh gói này sẽ được tái hợp lại. 

**Tầng 4 - Transport Layer (Tầng vận chuyển)**

- Quản lý và điêu phối việc truyền tải dữ liệu giữa các thiết bị đầu cuối (end-to-end). Đảm bảo dữ liệu được truyền tải từ ứng dụng ở thiết bị nguồn đến ứng dụng ở thiết bị đích một cách chính xác, an toàn và hiệu quả.

**Chức năng của Transport layer**

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

- Quản lý và duy trì các phiên làm việc (sessions) giữa các ứng dụng đang giao tiếp trên các thiết bị khác nhau. Xác định cách giao tiếp, duy trì kết nối quản lý phiên làm việc giữa 2 ứng dụng (gồm khởi tạo, đồng bộ hóa và kết thúc các phiên giao tiếp)

**Chức năng của Session Layer**

- Thiết lập, duy trì và kết thúc phiên làm việc: Session Layer thiết lập 1 phiên làm việc giữa 2 ứng dụng. Sau khi hoàn thành giao tiếp, nó sẽ kết thúc phiên đó và giải phóng tài nguyên.
- Quản lý đối thoại (Dialog Control): Kiểm soát kiểu đối thoại giữa các ứng dụng, half-duplex (giao tiếp chỉ có thể diễn ra theo 1 chiều tại 1 thời điểm) và full-duplex (giao tiếp có thể diễn ra 2 chiều đồng thời). VD khi trong 1 cuộc gọi video session layer kiểm soát việc truyền tải âm thanh và hình ảnh đồng thời giữa 2 bên.
- Đồng bộ hóa dữ liệu: Cung cấp các cơ chế để đồng bộ hóa dữ liệu giữa các ứng dụng, đảm bảo rằng các gói dữ liệu được truyền và nhận đúng thời gian. VD khi tải video từ ỉnternet session layer đảm bảo dữ liệu được đồng bộ hóa để video có thể phát liền mạch mà không bị gián đoạn.
- Khôi phục giao tiếp: Nếu có gián đoạn trong giao tiếp, session có thể quản lý việc khôi phục lại kết nối mà không làm mất dữ liệu.

**Tầng 6 - Presentation Layer (Tầng trình bày)**

- Chịu trách nhiệm định dạng, mã hóa, giải mã, nén dữ liệu giữa các ứng dụng. Đảm bảo rằng dữ liệu có thể được hiểu đúng giữa các hệ thống khác nhau, ngay cả khi giữa chúng sử dụng các định dạng hoặc phương thức mã hóa khác nhau. Hoạt động như cầu nối giữa tầng 7 và tầng 5.

**Chức năng chính của Presentation Layer**

- Chuyển đổi định dạng: Khi hai hệ thống sử dụng các định dạng khác nhau để truyền tải dữ liệu, Presentation thực hiện chuyển đổi giữa các định dạng sao cho ứng dụng nhận có thể hiểu được.
- Mã hóa và giải mã: Presentation sẽ mã hóa dữ liệu trước khi gửi đi và giải mã dữ liệu khi nhận được.
- Nén và giải nén: Nén dữ liệu để giảm băng thông khi truyền tải qua mạng và giải nén dữ liệu khi nhận
- Đảm bảo tính tương thích: Presentation đảm bảo rằng các hệ thống sử dụng các ngôn ngữ hoặc định dạng khác nhau vẫn có thể giao tiếp với nhau mà không gặp lỗi.

**Tầng 7 - Application Layer ( Tầng ứng dụng)**

 - Cung cấp các dịch vụ và giao thức cho ứng dụng người dùng cuối. Đây là nơi mà các giao tiếp mạng giữa các ứng dụng và hệ thống diễn ra.

**Chức năng của Application Layer**

- Giao tiếp giữa các ứng dụng: Cho phép các ứng dụng trên các thiết bị khác nhau giao tiếp với nhau thông qua giao thức mạng.
- Quản lý dịch vụ: Cung cấp các dịch vụ như email, truyền tệp, trình duyệt web, và các ứng dụng mạng khác.
- Đảm bảo tính tương thích và định dạng dữ liệu: Chuyển đổi dữ liệu giữa các ứng dụng và hệ thống khác nhau.
- Chạy các ứng dụng người dùng cuối: Gồm các ứng dụng như web browser, email client, FTP client.


### **TCP/IP (Transmission Control Protocol/Internet Protocol)**

**1. TCP/IP là gì** 

- là một bộ giao thức mạng được sử dụng để truyền tải dữ liệu qua các mạng máy tính. TCP/IP là một giao thức liên kết hai tầng, bao gồm tầng TCP và tầng IP, mỗi tầng thực hiện các chức năng riêng biệt nhưng hỗ trợ lẫn nhau để đảm bảo việc truyền tải dữ liệu hiệu quả.

**2. IP (Internet Protocol)**

- Mỗi thiết bị trong mạng được cấp 1 địa chỉ IP để có thể giao tiếp với nhau, giúp định tuyến dữ liệu từ máy này sang máy khác. IP quyết định cách thức chuyển tiếp các gói dữ liệu (chia nhỏ thành các gói tin) qua mạng đến đúng đích (định tuyến), làm việc với router để xác định tuyến đường tốt nhất để gói dữ liệu đi từ nguồn đến đích.
- Hoạt động ở Network Layer trong mô hình OSI

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

**Tầng 3 - Transport Layer (Tầng vận chuyển)**

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

**Tầng 2 - Internet Layer (Tầng Mạng)**

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

**Tầng 1 - Link Layer (Tầng vật lý)**

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


### **UDP(User Datagram Protocol)**

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

### **TCP (Transmission Control Protocol)

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

### **8. Đặc điểm nổi bật của IPv6**

1. **Không gian địa chỉ lớn**: IPv6 có không gian địa chỉ rất lớn với **128 bit**, điều này giúp giải quyết vấn đề thiếu hụt địa chỉ mà IPv4 gặp phải.

2. **Không cần NAT**: IPv6 không yêu cầu sử dụng **NAT (Network Address Translation)** vì có đủ không gian địa chỉ cho mỗi thiết bị có thể có một địa chỉ IP công cộng riêng biệt.

3. **Tự động cấu hình (SLAAC)**: IPv6 cho phép các thiết bị tự động cấu hình địa chỉ mà không cần sử dụng **DHCP**.

4. **Bảo mật**: IPv6 hỗ trợ **IPsec** (Internet Protocol Security) mặc định, giúp bảo mật kết nối trong suốt quá trình truyền tải dữ liệu.

### **9. Tóm tắt cấu trúc của IPv6**

- **Địa chỉ IPv6 có 128 bit**, chia thành 8 nhóm, mỗi nhóm 16 bit.
- Địa chỉ được biểu diễn dưới dạng **chữ số hex**, với các nhóm ngăn cách bằng dấu `:`.
- **Phần mạng** (Network Prefix) chiếm 64 bit đầu tiên, phần còn lại là **Mã nhận diện giao diện**.
- Các loại địa chỉ IPv6 gồm **Unicast**, **Multicast**, và **Anycast**.
- IPv6 hỗ trợ **rút gọn địa chỉ**, giúp viết địa chỉ ngắn gọn và dễ sử dụng.
