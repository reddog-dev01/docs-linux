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

----------------------

### **Bonding**

-  quá trình kết hợp nhiều kết nối mạng (hoặc cổng mạng) để tạo thành một kết nối duy nhất với băng thông cao hơn hoặc độ tin cậy cao hơn. Việc kết hợp này giúp tăng tốc độ truyền tải dữ liệu, cải thiện độ sẵn sàng (availability), và cung cấp khả năng dự phòng (redundancy) trong trường hợp một kết nối gặp sự cố.

**Các loại Bonding trong mạng**

**1. Link Aggregation (Liên kết các liên kết)**

IEEE 802.3ad (LACP - Link Aggregation Control Protocol) là giao thức phổ biến nhất để kết hợp nhiều liên kết vật lý vào một liên kết duy nhất. Điều này giúp tăng băng thông và tạo độ tin cậy cao hơn cho mạng.
LACP tự động phát hiện các cổng có thể gộp lại, và tối ưu hóa việc phân bổ tải và tăng băng thông.

**2. Ethernet Bonding (Liên kết Ethernet)**

Đây là việc kết hợp các cổng Ethernet của switch hoặc máy chủ để tăng băng thông hoặc độ tin cậy. Các phương pháp bonding này giúp cải thiện hiệu suất mạng và đảm bảo truyền tải dữ liệu mượt mà.
Bonding Ethernet thường được cấu hình thông qua các hệ điều hành như Linux, với các công cụ như ifenslave hoặc các trình điều khiển hệ thống mạng.

**3. Software-based Bonding (Bonding dựa trên phần mềm)**

Bonding có thể được thực hiện thông qua phần mềm trên máy chủ hoặc thiết bị mạng mà không cần phần cứng đặc biệt.
Phần mềm giúp kết hợp các kết nối mạng vật lý lại với nhau và tạo ra các kết nối mạng logic. Đây là một giải pháp linh hoạt và tiết kiệm chi phí, đặc biệt hữu ích trong các hệ thống Linux.

------------

**Lợi ích và ứng dụng của Bonding**

**Bonding trong mạng** là kỹ thuật kết hợp nhiều kết nối mạng vật lý thành một kết nối duy nhất để cải thiện hiệu suất và độ tin cậy của mạng. Điều này mang lại nhiều lợi ích và ứng dụng trong các môi trường mạng khác nhau. Dưới đây là **lợi ích** và **ứng dụng** của bonding trong mạng.

**Lợi ích của Bonding trong Mạng**

1. **Tăng băng thông (Bandwidth Aggregation)**:
   - **Bonding** cho phép kết hợp nhiều kết nối mạng vật lý lại với nhau, từ đó tăng tổng băng thông mà không cần phải nâng cấp phần cứng hoặc thay đổi cơ sở hạ tầng mạng.
   - Ví dụ: Nếu bạn có hai kết nối Ethernet với tốc độ 1 Gbps mỗi kết nối, việc bonding chúng lại có thể tạo ra một kết nối 2 Gbps.

2. **Cải thiện tính sẵn sàng (High Availability)**:
   - Một trong những lợi ích lớn nhất của bonding là khả năng dự phòng. Nếu một kết nối vật lý gặp sự cố, các kết nối còn lại sẽ tự động tiếp quản, đảm bảo mạng luôn hoạt động mà không bị gián đoạn.
   - Điều này rất quan trọng trong các môi trường yêu cầu tính sẵn sàng cao, như trong các **data center** hoặc **hệ thống quan trọng**.

3. **Cân bằng tải (Load Balancing)**:
   - Bonding giúp phân phối lưu lượng dữ liệu đều trên các kết nối vật lý, tránh tình trạng một kết nối bị quá tải trong khi các kết nối khác ít sử dụng.
   - Các chế độ bonding như **Round-robin** và **Adaptive Load Balancing** giúp cân bằng tải theo cách động và tối ưu hóa băng thông.

4. **Giảm độ trễ (Latency Reduction)**:
   - Việc phân phối lưu lượng qua nhiều kết nối giúp giảm độ trễ trong mạng, nhất là khi có nhiều thiết bị hoặc máy chủ cần truy cập dữ liệu cùng lúc.
   - Cân bằng tải và phân phối dữ liệu qua các cổng khác nhau giúp tăng tốc độ và giảm độ trễ.

5. **Tăng cường độ tin cậy và hiệu suất**:
   - Các hệ thống **Bonding** có thể giúp cải thiện độ tin cậy của mạng bằng cách giảm thiểu khả năng gián đoạn mạng, đồng thời tăng hiệu suất bằng cách tận dụng tất cả các kết nối vật lý có sẵn.

6. **Dễ dàng mở rộng (Scalability)**:
   - Bonding cho phép dễ dàng mở rộng mạng mà không cần thay đổi cấu trúc mạng hiện tại. Bạn chỉ cần thêm các kết nối vật lý và cấu hình bonding để tăng băng thông và hiệu suất.
   - Điều này đặc biệt hữu ích trong các môi trường mạng lớn, nơi nhu cầu về băng thông có thể thay đổi theo thời gian.

**Ứng dụng của Bonding trong Mạng**

1. **Mạng doanh nghiệp (Enterprise Networks)**:
   - Các doanh nghiệp lớn sử dụng bonding để kết nối các máy chủ, switch và thiết bị mạng lại với nhau, tối ưu hóa băng thông và giảm thiểu sự cố mạng. Bonding giúp tạo một mạng nội bộ ổn định và hiệu quả.
   - Ví dụ: Một doanh nghiệp có thể sử dụng bonding để kết nối các máy chủ web, cơ sở dữ liệu và các thiết bị mạng khác nhau, giúp cải thiện tốc độ truy cập và giảm thời gian chết.

2. **Data Centers (Trung tâm dữ liệu)**:
   - Trong các trung tâm dữ liệu, bonding là một yếu tố quan trọng để đảm bảo khả năng cung cấp băng thông cao và tính sẵn sàng cho các dịch vụ điện toán đám mây, lưu trữ và truyền tải dữ liệu.
   - Các **server farms** thường sử dụng bonding để kết hợp nhiều kết nối Ethernet, giúp xử lý lượng lớn dữ liệu một cách hiệu quả.

3. **Cung cấp Dịch vụ Internet (ISP - Internet Service Providers)**:
   - Các nhà cung cấp dịch vụ Internet (ISP) sử dụng bonding để kết hợp nhiều kết nối Internet, cung cấp cho người dùng băng thông rộng và tính sẵn sàng cao.
   - Điều này giúp ISP cung cấp dịch vụ ổn định, đảm bảo khách hàng có thể sử dụng Internet một cách liên tục, ngay cả khi một kết nối bị lỗi.

4. **Các Mạng Local Area Network (LAN)**:
   - **Bonding** trong LAN giúp các công ty và tổ chức kết nối các máy tính, thiết bị văn phòng và máy chủ với nhau, từ đó tăng cường hiệu suất và khả năng kết nối mạng.
   - Trong các môi trường LAN với nhiều thiết bị, việc sử dụng bonding giúp tối ưu hóa việc chia sẻ tài nguyên và giảm thiểu tắc nghẽn mạng.

5. **Mạng không dây (Wireless Networks)**:
   - Trong các mạng không dây, bonding có thể được sử dụng để kết hợp các kênh truyền dẫn không dây, giúp tăng băng thông và giảm độ trễ.
   - Ví dụ, trong các mạng Wi-Fi hoặc mạng 4G/5G, bonding các kênh sóng giúp tăng tốc độ và cải thiện chất lượng kết nối.

6. **Mạng lưu trữ (Storage Area Networks - SAN)**:
   - Trong các **Storage Area Networks (SAN)**, bonding giúp kết nối nhiều thiết bị lưu trữ và máy chủ lại với nhau, tạo thành một hệ thống lưu trữ ổn định và hiệu quả.
   - Việc sử dụng bonding trong SAN giúp giảm thiểu sự gián đoạn dịch vụ và cải thiện hiệu suất khi truyền tải dữ liệu lớn.

7. **Mạng ảo (Virtual Networks)**:
   - Trong các **mạng ảo** (Virtual Networks), bonding giúp cải thiện băng thông và độ tin cậy của các kết nối giữa các máy chủ ảo và hệ thống lưu trữ, đảm bảo các dịch vụ ảo hóa hoạt động mượt mà.

8. **Mạng trong môi trường sản xuất (Manufacturing Networks)**:
   - Các hệ thống tự động hóa và kiểm soát trong các môi trường sản xuất cần một mạng ổn định và có khả năng mở rộng. Bonding giúp đảm bảo việc kết nối liên tục giữa các máy móc, thiết bị và máy chủ trong các dây chuyền sản xuất.

-----

**Các chế độ Mode**

Trong **network bonding**, các **chế độ (modes)** xác định cách các kết nối mạng vật lý sẽ được sử dụng để kết hợp thành một kết nối duy nhất. Mỗi chế độ có cách thức hoạt động khác nhau và được áp dụng tùy theo nhu cầu mạng cụ thể như cân bằng tải, dự phòng, hay tăng băng thông. Dưới đây là các chế độ phổ biến của bonding trong mạng và cách sử dụng chúng.

1. **Mode 0 - Round-robin (Chế độ vòng tròn)**

   - **Cách hoạt động**: Trong chế độ này, dữ liệu được gửi lần lượt qua các cổng mạng theo một vòng tròn. Ví dụ, nếu có 3 cổng mạng, gói dữ liệu đầu tiên sẽ qua cổng 1, gói thứ hai qua cổng 2, gói thứ ba qua cổng 3, và sau đó tiếp tục quay lại cổng 1.
   
   - **Ứng dụng**: 
     - Thích hợp khi bạn muốn tận dụng tất cả các kết nối mạng đồng thời để tăng băng thông.
     - Phù hợp với các môi trường có nhiều thiết bị và yêu cầu băng thông cao, chẳng hạn như **mạng doanh nghiệp**, **data center**, hay **video streaming**.

   - **Lưu ý**:
     - Không phù hợp trong trường hợp các kết nối có tốc độ khác nhau hoặc khi các cổng mạng bị nghẽn, vì nó có thể tạo ra tình trạng **tắc nghẽn (congestion)**.

2. **Mode 1 - Active-backup (Chế độ chủ động-phục hồi)**

   - **Cách hoạt động**: Chế độ này chỉ có một cổng mạng hoạt động tại một thời điểm (cổng chủ động), còn các cổng khác sẽ trong trạng thái chờ đợi (dự phòng). Khi cổng chủ động gặp sự cố, một cổng dự phòng sẽ tự động thay thế và trở thành cổng chủ động.
   
   - **Ứng dụng**: 
     - Dành cho các môi trường mạng yêu cầu **tính sẵn sàng cao** và **dự phòng** như các **server farms**, **data center**.
     - Phù hợp trong các mạng nhỏ và trung bình, nơi không cần tăng băng thông mà chỉ cần đảm bảo kết nối liên tục.

   - **Lưu ý**:
     - Mặc dù chế độ này cải thiện tính sẵn sàng, nhưng nó không giúp tăng băng thông vì chỉ có một cổng mạng hoạt động tại một thời điểm.

3. **Mode 2 - XOR (Exclusive OR)**

   - **Cách hoạt động**: Trong chế độ XOR, mỗi gói dữ liệu được gửi qua cổng mà địa chỉ MAC nguồn và đích áp dụng phép toán XOR. Cách này giúp các gói được phân phối đều giữa các cổng mạng mà không gây tắc nghẽn.
   
   - **Ứng dụng**: 
     - Thích hợp cho các mạng có **lưu lượng dữ liệu không đồng đều**, như mạng của các **doanh nghiệp** lớn hoặc các **data center**.
     - Phù hợp với môi trường cần cân bằng tải nhưng không muốn phụ thuộc vào các giao thức như LACP.

   - **Lưu ý**:
     - Phân phối không hoàn toàn đồng đều, có thể gây ra tắc nghẽn nếu các kết nối không đều.

4. **Mode 4 - LACP (Link Aggregation Control Protocol)**

   - **Cách hoạt động**: **LACP** (IEEE 802.3ad) là một giao thức được sử dụng để tự động phát hiện và cấu hình các kết nối gộp. Khi một thiết bị mạng (như switch hoặc máy chủ) hỗ trợ LACP, nó sẽ tự động tạo các liên kết logic (aggregation) giữa các cổng mạng vật lý.
   
   - **Ứng dụng**: 
     - Dùng khi bạn muốn kết hợp nhiều liên kết vật lý thành một kết nối logic với các thiết bị mạng hỗ trợ LACP, chẳng hạn như trong các **data center** hoặc môi trường **mạng doanh nghiệp** có thiết bị mạng hiện đại hỗ trợ LACP.
     - Phù hợp với các **ISP** cung cấp dịch vụ với nhiều đường truyền, hoặc các **mạng LAN lớn**.

   - **Lưu ý**:
     - Cần có sự hỗ trợ từ cả hai đầu của liên kết (ví dụ, máy chủ và switch).
     - Đây là chế độ lý tưởng cho việc kết hợp băng thông mà không phải lo lắng về việc phân phối tải thủ công.

5. **Mode 6 - Balance-alb (Adaptive Load Balancing)**

   - **Cách hoạt động**: **Balance-alb** là một chế độ cân bằng tải động, không yêu cầu hỗ trợ từ switch. Nó không chỉ phân phối tải trên các kết nối mạng mà còn điều chỉnh theo trạng thái của các cổng mạng, giúp sử dụng băng thông hiệu quả hơn.
   
   - **Ứng dụng**: 
     - Phù hợp với các mạng có yêu cầu linh hoạt, như **mạng doanh nghiệp**, các **server farm** hoặc **mạng đám mây**.
     - Thích hợp cho môi trường không muốn phụ thuộc vào cấu hình đặc biệt từ switch hoặc không có tính năng LACP.

   - **Lưu ý**:
     - Chế độ này cần một số tính năng đặc biệt ở phần mềm hoặc phần cứng để hoạt động hiệu quả.

6. **Mode 3 – Broadcast**

   - **Cách hoạt động**: Mỗi gói dữ liệu sẽ được gửi qua tất cả các cổng mạng. Mỗi cổng mạng nhận được một bản sao của gói dữ liệu và gửi nó đến thiết bị đích.
   
   - **Ứng dụng**: 
     - Phù hợp trong những trường hợp mà bạn muốn đảm bảo mọi thiết bị nhận được dữ liệu đồng thời. Tuy nhiên, chế độ này ít được sử dụng vì có thể gây ra **tắc nghẽn** trong mạng.

   - **Lưu ý**:
     - Cần phải sử dụng cẩn thận vì có thể gây lãng phí băng thông khi gửi dữ liệu đến tất cả các cổng mạng, kể cả khi một số cổng không cần thiết.

------------

### **Test Bonding**

### **Cấu hình Bonding trên Ubuntu sử dụng Netplan**

Netplan thay thế cách cấu hình mạng trước đây bằng các tệp YAML, rất dễ sử dụng và linh hoạt. Để cấu hình bonding trong Ubuntu từ 18.04 trở lên, bạn làm theo các bước sau:

**Bước 1: Cài đặt các gói cần thiết**
Đầu tiên, bạn cần đảm bảo rằng gói **ifenslave** đã được cài đặt, vì nó giúp quản lý các liên kết bonding. Cài đặt gói này bằng lệnh sau:
```bash
sudo apt update
sudo apt install ifenslave
```

**Bước 2: Tạo cấu hình Netplan cho Bonding**

Giả sử bạn có hai giao diện mạng vật lý `eth0` và `eth1` và muốn tạo một bond với chúng.

1. **Chỉnh sửa tệp Netplan**: Tệp cấu hình Netplan thường nằm trong thư mục `/etc/netplan/`. Bạn cần chỉnh sửa hoặc tạo một tệp mới trong đó.

Mở tệp Netplan hiện tại (hoặc tạo tệp mới nếu không có):

```bash
sudo nano /etc/netplan/01-netcfg.yaml
```

2. **Cấu hình bonding trong tệp YAML**:

   Ví dụ cấu hình với **bond0** sử dụng chế độ **active-backup** (`bond-mode 1`):

   ```yaml
   network:
     version: 2
     renderer: networkd
     bonds:
       bond0:
         interfaces:
           - eth0
           - eth1
         parameters:
           mode: active-backup
           mii-monitor-interval: 100
           primary: eth0
         dhcp4: true
     ethernets:
       eth0:
         dhcp4: no
       eth1:
         dhcp4: no
   ```

   **Giải thích các trường:**
   - `bond0`: Tên của giao diện bonding.
   - `interfaces`: Liệt kê các giao diện vật lý tham gia bonding (ở đây là `eth0` và `eth1`).
   - `mode: active-backup`: Chế độ bonding, ở đây là **active-backup** (cổng chính và cổng sao lưu).
   - `mii-monitor-interval`: Kiểm tra tình trạng của các cổng mạng vật lý sau mỗi 100ms.
   - `primary: eth0`: Chỉ định `eth0` là cổng chính.
   - `dhcp4: true`: Cấu hình **DHCP** để tự động nhận địa chỉ IP cho bond0.
   - `dhcp4: no`: Tắt DHCP cho các giao diện vật lý `eth0` và `eth1` vì chúng là các slave của bond0.


**Bước 3: Áp dụng cấu hình**

Sau khi chỉnh sửa tệp cấu hình, bạn cần áp dụng thay đổi:

```bash
sudo netplan apply
```

**Bước 4: Kiểm tra trạng thái của bonding**

Sau khi áp dụng cấu hình, bạn có thể kiểm tra trạng thái của liên kết bonding:

1. **Kiểm tra trạng thái bonding**:

   Sử dụng lệnh sau để xem thông tin về **bond0**:

   ```bash
   cat /proc/net/bonding/bond0
   ```

   Bạn sẽ thấy thông tin chi tiết về trạng thái của các cổng vật lý, chế độ bonding, v.v.

2. **Kiểm tra các giao diện mạng**:

   Kiểm tra các giao diện mạng trên hệ thống bằng cách sử dụng:

   ```bash
   ifconfig
   ```

   Bạn sẽ thấy giao diện `bond0` trong danh sách các giao diện mạng.

**Bước 5: Thêm các chế độ khác (nếu cần)**

Đây là một số chế độ bonding mà bạn có thể cấu hình trong Netplan:

- **Chế độ 0 - Round-robin** (Cân bằng tải):
  ```yaml
  mode: balance-rr
  ```

- **Chế độ 1 - Active-backup** (Dự phòng):
  ```yaml
  mode: active-backup
  ```

- **Chế độ 4 - LACP (Link Aggregation Control Protocol)**:
  ```yaml
  mode: 802.3ad
  ```

- **Chế độ 6 - Adaptive Load Balancing** (Balance-ALB):
  ```yaml
  mode: balance-alb
  ```

