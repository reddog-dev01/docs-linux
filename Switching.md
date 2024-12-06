### **SWITCHING**

- Switching là quá trình chuyển dữ liệu từ nguồn đến đích qua một mạng viễn thông. Các thiết bị chuyển mạch (switches) trong mạng giám sát và điều hướng lưu lượng trên mạng bằng cách chuyển dữ liệu đến địa chỉ hoặc cổng chính xác.
- Switching diễn ra ở Data Link layer của OSI (sau khi các gói dữ liệu được tạo ra ở Physical Layer

**Các loại Switching**

**Switch là gì?**

Trong mạng máy tính, **switch** (công tắc mạng) là một thiết bị phần cứng dùng để kết nối các thiết bị mạng như máy tính, máy in, server, và các thiết bị khác trong một mạng cục bộ (LAN). Switch giúp các thiết bị chia sẻ tài nguyên mạng mà không làm gián đoạn hoặc gây xung đột dữ liệu giữa chúng.

Switch hoạt động tại **Tầng Liên kết Dữ liệu (Data Link Layer)** trong mô hình OSI và giúp chuyển tiếp các gói dữ liệu (frames) giữa các thiết bị trong cùng một mạng LAN.

**Cách thức hoạt động của Switch:**

- **Kết nối các thiết bị trong mạng:** Switch kết nối nhiều thiết bị trong mạng LAN và giúp các thiết bị này giao tiếp với nhau bằng cách chuyển tiếp gói dữ liệu qua các cổng của nó.
  
- **Địa chỉ MAC:** Khi một thiết bị gửi dữ liệu qua mạng, switch sử dụng **địa chỉ MAC (Media Access Control)** của thiết bị gửi và nhận để xác định đích đến của gói dữ liệu. Mỗi thiết bị trong mạng có một địa chỉ MAC duy nhất.

- **Bảng chuyển mạch:** Switch duy trì một bảng chuyển mạch (hoặc bảng định tuyến) lưu trữ các địa chỉ MAC của các thiết bị kết nối với các cổng của nó. Khi một gói dữ liệu đến, switch kiểm tra địa chỉ MAC đích và gửi gói dữ liệu đến cổng tương ứng mà thiết bị đích kết nối.

- **Forwarding Decision (Quyết định chuyển tiếp):** Khi switch nhận được một gói dữ liệu, nó sẽ tra cứu địa chỉ MAC đích trong bảng chuyển mạch. Nếu tìm thấy, nó chuyển tiếp gói đến cổng thích hợp. Nếu không tìm thấy, nó sẽ "flooding" (phát gói dữ liệu) đến tất cả các cổng trừ cổng nhận gói ban đầu, nhằm tìm ra thiết bị đích.

- **Giảm tắc nghẽn mạng:** Vì switch chỉ gửi dữ liệu đến cổng đích thay vì phát tất cả dữ liệu đến mọi cổng như trong hub, nên nó giúp giảm tắc nghẽn và tăng hiệu quả trong mạng.

**Các loại switch:**

- **Unmanaged Switch (Switch không quản lý):** Đây là loại switch cơ bản, không yêu cầu cấu hình và thường được sử dụng cho các mạng nhỏ hoặc trong các môi trường không yêu cầu quản lý mạng phức tạp.

- **Managed Switch (Switch quản lý):** Loại switch này cung cấp nhiều tính năng như khả năng cấu hình, giám sát và quản lý mạng. Managed switch cho phép người dùng cấu hình VLANs, chất lượng dịch vụ (QoS), bảo mật và khả năng khôi phục lỗi trong mạng.

- **PoE Switch (Switch cấp nguồn qua Ethernet):** Đây là loại switch cung cấp cả dữ liệu và nguồn điện qua cáp Ethernet cho các thiết bị hỗ trợ PoE, như điện thoại VoIP, camera IP, hoặc các thiết bị mạng khác.

**Lợi ích của Switch:**

1. **Tăng băng thông:** Switch giảm tắc nghẽn mạng bằng cách phân phối băng thông mạng giữa các thiết bị trong mạng LAN mà không làm gián đoạn thông tin giữa các thiết bị.
   
2. **An toàn và bảo mật:** Switch chỉ chuyển tiếp gói dữ liệu đến các cổng đích cụ thể, giúp bảo vệ dữ liệu khỏi bị truy cập trái phép từ các thiết bị không liên quan trong mạng.

3. **Tăng khả năng mở rộng mạng:** Khi sử dụng switch, bạn có thể dễ dàng mở rộng mạng LAN bằng cách thêm thiết bị mà không ảnh hưởng đến hoạt động của các thiết bị khác.

4. **Giảm độ trễ:** So với hub (thiết bị trước đây thường dùng để kết nối mạng), switch giảm độ trễ trong truyền tải dữ liệu vì nó không phát gói dữ liệu đến tất cả các thiết bị mà chỉ gửi đến thiết bị đích.

--------------

### **Network Switching (Chuyển Mạch Mạng)**

**Network Switching** là quá trình chuyển các gói dữ liệu từ một thiết bị này sang thiết bị khác trong mạng hoặc giữa các mạng, sử dụng các thiết bị chuyển mạch gọi là **switches**. Mục tiêu của chuyển mạch mạng là đảm bảo dữ liệu được gửi từ nguồn đến đích một cách hiệu quả và chính xác. Trong quá trình này, các gói dữ liệu sẽ được xử lý và chuyển tiếp bởi các thiết bị mạng, thường là các switch hoặc router.

Switches hoạt động chủ yếu tại **Tầng Liên kết Dữ Liệu (Data Link Layer)** của mô hình OSI, nghĩa là các switch xử lý việc truyền tải các khung dữ liệu từ thiết bị này sang thiết bị khác trong cùng một mạng.

**Quá Trình Chuyển Mạch (Process of Switching)**

Quá trình chuyển mạch bao gồm nhiều bước để đảm bảo dữ liệu được chuyển đến đúng đích. Dưới đây là các bước chính trong quá trình chuyển mạch:

#### 1. **Tiếp Nhận Khung Dữ Liệu (Frame Reception)**

Khi một thiết bị trong mạng gửi dữ liệu, nó sẽ được đóng gói trong các khung (frames). Các switch nhận các khung này từ các thiết bị được kết nối với nó. Switch đầu tiên nhận khung dữ liệu từ cổng vào.

#### 2. **Trích Xuất Địa Chỉ MAC (MAC Address Extraction)**

Switch đọc tiêu đề của khung dữ liệu và trích xuất **địa chỉ MAC** đích. Địa chỉ MAC là một địa chỉ duy nhất của mỗi thiết bị trong mạng, giúp switch xác định thiết bị đích mà gói dữ liệu cần gửi đến.

#### 3. **Tra Cứu Bảng Địa Chỉ MAC (MAC Address Table Lookup)**

Switch sử dụng **bảng chuyển mạch (MAC address table)** để tra cứu địa chỉ MAC đích trong bảng này. Bảng chuyển mạch chứa thông tin về các thiết bị được kết nối và cổng của switch mà chúng đang sử dụng. Mỗi mục trong bảng này kết hợp giữa địa chỉ MAC và cổng kết nối.

- Nếu địa chỉ MAC đích được tìm thấy trong bảng, switch sẽ quyết định cổng nào để gửi khung dữ liệu.
- Nếu không tìm thấy địa chỉ trong bảng, switch sẽ "flood" (phát gói) đến tất cả các cổng (trừ cổng nhận gói ban đầu), nhằm tìm thiết bị đích.

#### 4. **Quyết Định Chuyển Tiếp và Cập Nhật Bảng Chuyển Mạch (Forwarding Decision and Table Update)**

- Nếu switch tìm thấy địa chỉ MAC đích trong bảng chuyển mạch, nó sẽ gửi gói dữ liệu đến cổng tương ứng với địa chỉ MAC đó.
- Nếu không tìm thấy địa chỉ, switch sẽ gửi gói dữ liệu tới tất cả các cổng để tìm thiết bị đích và sau đó cập nhật bảng chuyển mạch với các địa chỉ MAC mà nó đã phát gói đến.

#### 5. **Chuyển Gói Dữ Liệu (Frame Forwarding)**

Sau khi quyết định được cổng đích, switch sẽ chuyển gói dữ liệu đến cổng đó, đưa gói dữ liệu đến thiết bị đích trong mạng.



----------------

### **Các loại Switching**

**Circuit Switching**

**Circuit Switching** là một phương pháp chuyển mạch truyền thống trong mạng viễn thông, nơi mà một kết nối vật lý cố định được thiết lập giữa hai điểm cuối trong suốt thời gian của cuộc giao tiếp. Khi một cuộc gọi được thực hiện, một đường dẫn được thiết lập và giữ nguyên cho đến khi cuộc gọi kết thúc, không có thiết bị nào khác có thể sử dụng các tài nguyên đường dẫn đó cho đến khi nó được giải phóng.

**Cách Thức Hoạt Động của Circuit Switching**

1. **Thiết lập Đường Dẫn:**
   - Khi hai điểm muốn giao tiếp, một đường dẫn vật lý được thiết lập thông qua mạng. Quá trình này bao gồm việc định tuyến cuộc gọi qua các trạm chuyển mạch và tạo một kết nối liên tục.

2. **Truyền Dữ liệu:**
   - Sau khi đường dẫn được thiết lập, dữ liệu bắt đầu truyền liên tục giữa người gửi và người nhận. Dữ liệu theo đường dẫn này không bị chia sẻ với các cuộc gọi khác.

3. **Giải Phóng Đường Dẫn:**
   - Cuối cùng, khi cuộc giao tiếp kết thúc, đường dẫn được giải phóng và tài nguyên đó trở lại trạng thái sẵn sàng cho các cuộc giao tiếp tiếp theo.

**Ứng Dụng của Circuit Switching**

- **Mạng Điện Thoại Truyền Thống:**
   - Circuit switching là nền tảng của mạng điện thoại truyền thống, nơi mỗi cuộc gọi cần một đường dẫn cố định để đảm bảo chất lượng và không bị gián đoạn.
  
- **Mạng Dữ Liệu Chuyên Dụng:**
   - Dùng trong các mạng dữ liệu chuyên dụng nơi độ trễ thấp và băng thông đảm bảo là cần thiết, chẳng hạn như trong các ứng dụng tài chính hoặc các ứng dụng quan trọng khác.

**Ưu và Nhược Điểm của Circuit Switching**

- **Ưu điểm:**
   - **Độ Tin Cậy Cao:** Kết nối liên tục đảm bảo độ tin cậy cao và chất lượng ổn định.
   - **Độ Trễ Thấp:** Không có độ trễ do xử lý gói tin, vì vậy rất phù hợp cho các ứng dụng cần độ trễ thấp.
   
- **Nhược điểm:**
   - **Tốn Tài Nguyên:** Tài nguyên đường dẫn bị chiếm dụng suốt thời gian cuộc gọi, ngay cả khi không có dữ liệu truyền qua.
   - **Không Linh Hoạt:** Không hiệu quả khi lưu lượng giao tiếp có tính chất bursty hoặc khi lượng dữ liệu truyền không đều.
   - **Quá Trình Thiết Lập Mất Thời Gian:** Cần thời gian để thiết lập kết nối trước khi có thể bắt đầu truyền dữ liệu.

--------------

### **Packet Switching**

Packet Switching là một kỹ thuật mạng cho phép dữ liệu được chia thành các gói nhỏ, được gửi đi qua mạng một cách độc lập và có thể theo các đường dẫn khác nhau đến đích. Kỹ thuật này là nền tảng của mạng Internet hiện đại và được sử dụng rộng rãi trong các mạng máy tính để truyền dữ liệu.

**Cách Thức Hoạt Động của Packet Switching**
1. **Phân Mảnh Dữ Liệu:**
   - Dữ liệu lớn được chia thành các gói nhỏ hơn. Mỗi gói chứa một phần của dữ liệu gốc cùng với thông tin đầu đề (header) mô tả nguồn, đích, số thứ tự, và thông tin khác cần thiết cho việc truyền tải và tái lắp ráp.

2. **Định Tuyến Độc Lập:**
   - Mỗi gói được gửi độc lập qua mạng và có thể đi qua các tuyến đường khác nhau đến đích, tùy thuộc vào tình trạng mạng tại thời điểm đó.

3. **Tái Lắp Ráp:**
   - Tại điểm đích, các gói được tái lắp ráp theo đúng thứ tự để phục hồi thông tin gốc.

**Ưu Điểm của Packet Switching**
- **Hiệu Quả Cao:**
  - Tối ưu hóa việc sử dụng băng thông; chỉ các gói cần thiết mới được truyền đi, giúp giảm bớt lãng phí tài nguyên.
  
- **Độ Tin Cậy Cao:**
  - Nếu một tuyến đường bị hỏng hoặc quá tải, các gói có thể được chuyển hướng qua các tuyến đường khác, đảm bảo dữ liệu vẫn có thể đến được đích.

- **Linh Hoạt và Mở Rộng:**
  - Dễ dàng mở rộng và thích ứng với sự thay đổi của mạng mà không cần thay đổi cơ sở hạ tầng cơ bản.

---

**Nhược Điểm của Packet Switching**
- **Không Đảm Bảo Thời Gian Thực:**
  - Không phù hợp cho các ứng dụng đòi hỏi thời gian thực như cuộc gọi điện thoại hoặc video conferencing do độ trễ và sự chênh lệch thời gian gửi nhận các gói.

- **Phức Tạp trong Quản Lý:**
  - Việc quản lý và định tuyến các gói tin có thể phức tạp khi mạng lớn và đông đúc, yêu cầu các thuật toán định tuyến phức tạp và cơ sở hạ tầng mạng mạnh mẽ.

- **Cần Cơ Chế Kiểm Soát Lỗi và Luồng:**
  - Cần có cơ chế kiểm soát lỗi và kiểm soát luồng để đảm bảo dữ liệu được truyền một cách chính xác và hiệu quả.

----------------

### **Message Switching**

**Message Switching** là một phương pháp chuyển mạch trong đó toàn bộ một thông điệp (message) được nhận tại mỗi nút chuyển mạch và lưu trữ tạm thời trước khi được chuyển tiếp đến nút tiếp theo trong mạng. Phương pháp này không yêu cầu thiết lập một đường truyền cố định giữa nguồn và đích như trong **circuit switching**, mà thay vào đó, mỗi thông điệp được lưu trữ và chuyển tiếp qua mạng.

**Cách Thức Hoạt Động của Message Switching**
1. **Chuyển Tiếp Lưu Trữ (Store-and-Forward):**
   - Khi một thông điệp đến một nút chuyển mạch (switch), thông điệp sẽ được lưu trữ tạm thời tại đó cho đến khi có sẵn một đường truyền để chuyển tiếp thông điệp đó đến nút tiếp theo.
   - Nút chuyển mạch sẽ kiểm tra các điều kiện về đường truyền và lưu trữ thông điệp cho đến khi có thể gửi tiếp.

2. **Không Cần Kết Nối Cố Định:**
   - Không giống như circuit switching, trong message switching không cần thiết lập một đường truyền cố định giữa các nút trong suốt quá trình truyền tải. Mỗi thông điệp có thể đi qua các tuyến đường khác nhau và không theo một lộ trình cố định.

3. **Chuyển Tiếp Từng Thông Điệp:**
   - Mỗi thông điệp được xử lý một cách độc lập, không chia nhỏ thành các gói như trong **packet switching**. Điều này có thể dẫn đến độ trễ cao hơn, vì phải chờ đợi để lưu trữ và chuyển tiếp toàn bộ thông điệp.

4. **Tái Lắp Ráp (Reassembly):**
   - Không giống như packet switching, không cần tái lắp ráp thông điệp vì toàn bộ thông điệp đã được gửi nguyên vẹn từ nguồn đến đích. Tuy nhiên, nếu có nhiều thông điệp nhỏ được gửi, mỗi thông điệp sẽ được xử lý riêng biệt.

**Ưu Điểm của Message Switching**
- **Không Cần Đường Dẫn Cố Định:**
  - Phương pháp này linh hoạt hơn so với circuit switching vì không yêu cầu thiết lập một đường truyền cố định trong suốt quá trình truyền tải.
  
- **Tiết Kiệm Tài Nguyên Mạng:**
  - Do không cần giữ một kết nối cố định, tài nguyên mạng có thể được sử dụng hiệu quả hơn, đặc biệt trong các tình huống mạng có lưu lượng không đồng đều.

- **Có Thể Chuyển Tiếp Các Thông Điệp Lớn:**
  - Thông điệp có thể được chuyển tiếp dưới dạng nguyên vẹn mà không cần phân mảnh.

**Nhược Điểm của Message Switching**
- **Độ Trễ Cao:**
  - Do thông điệp phải được lưu trữ tại mỗi nút cho đến khi có đủ khả năng để chuyển tiếp, có thể gây ra độ trễ lớn, đặc biệt khi có tắc nghẽn trong mạng.

- **Không Phù Hợp Cho Ứng Dụng Thời Gian Thực:**
  - Vì độ trễ cao và quá trình lưu trữ, message switching không thích hợp cho các ứng dụng yêu cầu thời gian thực như thoại hay video.

- **Khó Kiểm Soát Lưu Lượng:**
  - Việc chuyển tiếp các thông điệp lớn có thể gặp khó khăn trong việc kiểm soát lưu lượng và phân phối tải mạng, đặc biệt khi mạng trở nên quá tải.

**Ứng Dụng và Lịch Sử**
- **Ứng Dụng:** 
  - Message switching đã được sử dụng trong các mạng viễn thông cũ như mạng điện tín (telegraph networks) và một số hệ thống truyền thông dữ liệu sơ khai.
  
- **Lịch Sử:**
  - Tuy nhiên, phương pháp này đã dần bị thay thế bởi **packet switching** vì tính linh hoạt, hiệu quả và khả năng quản lý lưu lượng tốt hơn, đặc biệt là trong môi trường mạng ngày nay.


