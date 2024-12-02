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


--------------
---------------

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

  - 
