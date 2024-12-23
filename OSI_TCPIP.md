### **OSI**

### **1. MÔ HÌNH OSI**

-  OSI không chỉ định giao thức, mà chỉ định nhiệm vụ của giao thức
![image](https://github.com/user-attachments/assets/509547d5-a818-4218-80f2-b9d710677832)

#### **1.1 Các giao thức trong mô hình OSI**

Tầng Vật lý (Physical Layer):

- Chịu trách nhiệm truyền và nhận các tín hiệu thô qua môi trường vật lý.
- Đảm bảo kết nối vật lý giữa các thiết bị cũng như việc mã hóa dữ liệu thành tín hiệu.

Tầng Liên kết dữ liệu (Data Link Layer):

- Đảm bảo truyền dữ liệu an toàn và tin cậy giữa các thiết bị trên một mạng.
- Khung dữ liệu, kiểm soát lỗi, kiểm soát truy cập môi trường.

Tầng Mạng (Network Layer):

- Xác định đường đi tốt nhất cho dữ liệu thông qua mạng.
- Sử dụng địa chỉ mạng (như IP) để xác định nguồn và điểm đến của gói dữ liệu.

Tầng Vận chuyển (Transport Layer):

- Đảm bảo việc truyền dữ liệu tin cậy từ điểm này tới điểm khác.
- Kiểm soát lỗi, kiểm soát luồng và đảm bảo tính toàn vẹn của gói tin.

Tầng Phiên (Session Layer):

- Quản lý phiên làm việc giữa các ứng dụng trên các thiết bị kết nối mạng.
- Đặt lên và duy trì, quản lý và kết thúc các phiên.

Tầng Trình diễn (Presentation Layer):

- Đảm bảo thông tin mà ứng dụng tại một hệ thống được đọc được bởi ứng dụng tại hệ thống khác.
- Xử lý dữ liệu (ví dụ: mã hóa, nén và chuyển đổi dữ liệu).

Tầng Ứng dụng (Application Layer):

- Cung cấp giao diện cho các ứng dụng để tương tác với hệ thống mạng.
- Đảm bảo các ứng dụng có thể truy cập vào mạng và thực hiện các chức năng mạng


**Quá trình dữ liệu từ máy A đến máy B qua các tầng trong mô hình OSI:**

1. **Máy A (Tầng 7 - Application Layer)**
- **Ứng dụng**: Máy A (ví dụ: một trình duyệt web hoặc ứng dụng email) tạo ra dữ liệu người dùng, ví dụ như một yêu cầu HTTP hoặc một email.
  - Ví dụ: Người dùng máy A gửi một yêu cầu HTTP để truy cập một trang web (request).
- **Dữ liệu tại Tầng 7**: Đây là dữ liệu gốc, ví dụ: **HTTP request**.

2. **Máy A (Tầng 6 - Presentation Layer)**
- **Xử lý dữ liệu**: Tầng 6 sẽ xử lý dữ liệu nếu cần thiết. Tầng này có thể thực hiện:
  - Chuyển đổi định dạng (ví dụ: từ ASCII sang Unicode).
  - Mã hóa (nếu ứng dụng yêu cầu bảo mật, như mã hóa SSL).
  - Nén dữ liệu (nếu cần tiết kiệm băng thông).
  - Ví dụ: Nếu dữ liệu cần mã hóa hoặc nén, thì ở Tầng 6 dữ liệu sẽ được xử lý.

- **Dữ liệu tại Tầng 6**: Sau khi xử lý, dữ liệu có thể đã được mã hóa hoặc nén, nhưng vẫn là một yêu cầu HTTP hoặc email.

3. **Máy A (Tầng 5 - Session Layer)**
- **Quản lý kết nối**: Tầng 5 đảm bảo rằng kết nối giữa máy A và máy B được duy trì trong suốt quá trình trao đổi dữ liệu. Tầng này quản lý các phiên làm việc giữa các ứng dụng.
  - Ví dụ: Nếu máy A và máy B đang thực hiện giao tiếp qua HTTP, Tầng 5 sẽ duy trì kết nối trong suốt thời gian yêu cầu HTTP và phản hồi HTTP.

- **Dữ liệu tại Tầng 5**: Dữ liệu không thay đổi, chỉ được gắn thêm thông tin về phiên làm việc.

4. **Máy A (Tầng 4 - Transport Layer)**
- **Chia nhỏ dữ liệu**: Tầng 4 (TCP hoặc UDP) nhận dữ liệu từ Tầng 5 và chia nó thành các **segments**.
  - Tầng 4 thêm vào các thông tin điều khiển như cổng nguồn và cổng đích (ví dụ: cổng 80 cho HTTP).
  - Tầng 4 sử dụng giao thức TCP để kiểm tra lỗi, kiểm soát luồng, và đảm bảo dữ liệu được truyền đúng thứ tự (đối với TCP). Nếu là UDP, việc kiểm soát lỗi và đảm bảo thứ tự không được thực hiện.

- **Dữ liệu tại Tầng 4**: Sau khi chia nhỏ, dữ liệu được chuyển thành **segments** (ví dụ: TCP segment) với các thông tin như cổng và kiểm soát lỗi.

5. **Máy A (Tầng 3 - Network Layer)**
- **Định tuyến và đóng gói**: Tầng 3 nhận các **segments** từ Tầng 4 và **đóng gói** chúng thành **packets**. 
  - Tầng 3 thêm các thông tin định tuyến vào **header** của **packet**, bao gồm địa chỉ IP nguồn và đích, TTL (Time-to-Live), và loại giao thức (TCP/UDP).
  - Tầng 3 sử dụng địa chỉ IP để định tuyến packet qua mạng đến máy B.

- **Dữ liệu tại Tầng 3**: Sau khi đóng gói, dữ liệu trở thành **packets**, có chứa địa chỉ IP của máy A và máy B, và thông tin định tuyến.

6. **Máy A (Tầng 2 - Data Link Layer)**
- **Đóng gói thành frames**: Tầng 2 nhận các **packets** từ Tầng 3 và **đóng gói** chúng thành **frames**.
  - Tầng 2 thêm thông tin như **địa chỉ MAC** nguồn và đích, kiểm tra lỗi (CRC) vào **frame**.
  - Dữ liệu có thể được truyền qua các mạng LAN hoặc qua các thiết bị chuyển mạch (switch).

- **Dữ liệu tại Tầng 2**: Sau khi đóng gói, dữ liệu trở thành **frames**, với thông tin về địa chỉ MAC và các thông tin kiểm tra lỗi.

7. **Máy A (Tầng 1 - Physical Layer)**
- **Chuyển thành tín hiệu vật lý**: Tầng 1 chịu trách nhiệm chuyển **frames** thành các tín hiệu vật lý (bit) để truyền qua môi trường vật lý (dây cáp, sóng vô tuyến, v.v.).
  - Ví dụ: Tầng 1 có thể biến **frames** thành tín hiệu điện (qua cáp Ethernet) hoặc sóng vô tuyến (qua Wi-Fi).
  
- **Dữ liệu tại Tầng 1**: Tín hiệu vật lý được truyền qua môi trường vật lý (ví dụ: cáp mạng, sóng vô tuyến, v.v.).


**Khi dữ liệu đến Máy B**:

1. **Máy B (Tầng 1 - Physical Layer)**: 
   - Tín hiệu vật lý từ môi trường vật lý được nhận và chuyển thành **frames** tại Tầng 2.

2. **Máy B (Tầng 2 - Data Link Layer)**:
   - Tầng 2 giải mã **frames** và chuyển dữ liệu sang Tầng 3 dưới dạng **packets**.

3. **Máy B (Tầng 3 - Network Layer)**:
   - Tầng 3 nhận các **packets**, giải mã và xác định địa chỉ IP đích. Sau đó, dữ liệu được chuyển xuống Tầng 4 dưới dạng **segments**.

4. **Máy B (Tầng 4 - Transport Layer)**:
   - Tầng 4 nhận các **segments**, kiểm tra lỗi và sắp xếp chúng (nếu cần). Sau đó, dữ liệu được gửi lên Tầng 5 dưới dạng dữ liệu gốc.

5. **Máy B (Tầng 5 - Session Layer)**:
   - Tầng 5 xử lý thông tin phiên làm việc và giữ kết nối giữa các ứng dụng.

6. **Máy B (Tầng 6 - Presentation Layer)**:
   - Tầng 6 có thể chuyển đổi định dạng dữ liệu nếu cần (mã hóa/giải mã, nén/dãn nén).

7. **Máy B (Tầng 7 - Application Layer)**:
   - Dữ liệu cuối cùng được trình bày cho ứng dụng trên máy B (ví dụ: trang web được tải trong trình duyệt hoặc email được nhận trong ứng dụng email).


#### **1.2 Vai trò và chức năng 7 tầng OSI**

##### **Tầng 1 - Physical layer (Tầng vật lý)**

**Lớp Vật lý (Physical Layer)** trong mô hình OSI là lớp **thấp nhất**, chịu trách nhiệm truyền tải tín hiệu vật lý qua phương tiện truyền dẫn (cáp, sóng radio, v.v.). Lớp này không xử lý dữ liệu dưới dạng gói, mà chỉ quan tâm đến cách truyền và nhận tín hiệu giữa các thiết bị.


**Chức năng chính của Lớp Vật lý**
1. **Chuyển đổi dữ liệu thành tín hiệu vật lý**:
   - Biến tín hiệu số (bit 0 và 1) thành tín hiệu điện, ánh sáng, hoặc sóng radio để truyền qua cáp hoặc môi trường không dây.

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


**Ví dụ cụ thể trong Lớp Vật lý**
- **Cáp Ethernet (RJ45):**
  - Chuyển đổi tín hiệu điện qua dây cáp đồng.
  - Tốc độ truyền có thể là 10 Mbps, 100 Mbps, 1 Gbps...
- **Cáp quang (Fiber Optics):**
  - Truyền tín hiệu ánh sáng qua sợi quang học, tốc độ cao hơn (10 Gbps, 100 Gbps...).
- **Wi-Fi:**
  - Sử dụng sóng radio để truyền tín hiệu qua không khí, thường dùng tần số 2.4 GHz hoặc 5 GHz.

**Các thiết bị liên quan đến Lớp Vật lý**

**Cáp mạng**:
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
3. **Bluetooth**:
   - Truyền tín hiệu không dây trong khoảng cách ngắn.

--------------------------


##### **Tầng 2 - Data Link Layer ( Tầng liên kết dữ liệu)**

**Lớp Liên kết Dữ liệu (Data Link Layer)** trong mô hình OSI là lớp thứ hai, đóng vai trò quan trọng trong việc xử lý và đóng gói dữ liệu để truyền qua phương tiện vật lý. Nó đảm bảo rằng dữ liệu có thể được truyền một cách an toàn và hiệu quả giữa các thiết bị trong một mạng cục bộ hoặc qua môi trường truyền dẫn.

**Chức năng chính của Lớp Liên kết Dữ liệu**
1. **Đóng khung (Framing)**:
   - Chia dữ liệu từ lớp tầng 3 thành các khung dữ liệu nhỏ hơn.
   - Mỗi khung bao gồm trường header, data, trailer để định dạng và kiểm soát lỗi.

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

**Quy trình hoạt động**

**Quy trình hoạt động của Tầng 2 - Lớp Liên kết Dữ liệu (Data Link Layer)** trong mô hình OSI chủ yếu liên quan đến việc cung cấp phương thức đáng tin cậy để truyền tải dữ liệu giữa các thiết bị trong một mạng cục bộ (LAN) hoặc giữa các thiết bị trên cùng một liên kết vật lý. Lớp liên kết dữ liệu có nhiệm vụ đảm bảo rằng dữ liệu được truyền đi không bị lỗi và có thể được nhận đúng cách, ngoài ra, nó cũng xử lý các vấn đề như **địa chỉ vật lý**, **quản lý truy cập phương tiện** và **phát hiện lỗi**.

Các bước trong quy trình hoạt động của **Tầng Liên kết Dữ liệu (Data Link Layer)**:


1. **Chia nhỏ dữ liệu từ Tầng Mạng thành các khung (Frames)**

- **Tầng Liên kết Dữ liệu** nhận dữ liệu từ Tầng Mạng (Layer 3), mà thường là các gói (packets). Tầng này sẽ đóng gói các gói thành các đơn vị nhỏ hơn gọi là **khung** (frames).
  
  - **Khung (Frame)** là một đơn vị dữ liệu mà Tầng Liên kết Dữ liệu sử dụng để truyền tải qua mạng. Nó bao gồm các thành phần:
    - **Địa chỉ MAC nguồn và đích** (Source MAC Address, Destination MAC Address)
    - **Dữ liệu của gói (Payload)**: Dữ liệu gói mà nó nhận từ Tầng Mạng
    - **Kiểm tra lỗi** (Error Checking): Thường là **CRC** (Cyclic Redundancy Check) để phát hiện lỗi trong quá trình truyền.

2. **Địa chỉ MAC (Media Access Control)**

- **Tầng Liên kết Dữ liệu** chịu trách nhiệm xác định **địa chỉ vật lý MAC** của thiết bị đích. Địa chỉ MAC (hay còn gọi là địa chỉ Ethernet) là một địa chỉ duy nhất được gán cho mỗi thiết bị trong mạng. Đây là thông tin quan trọng để đảm bảo rằng dữ liệu được truyền đến đúng thiết bị đích trong mạng.

  - **Địa chỉ MAC nguồn** và **địa chỉ MAC đích** được thêm vào phần đầu của khung dữ liệu để định danh thiết bị nguồn và đích.
  - Các địa chỉ này là cố định và được gán khi thiết bị được sản xuất, khác với địa chỉ IP, địa chỉ MAC không thay đổi trong quá trình hoạt động của thiết bị.

3. **Kiểm tra lỗi và phát hiện lỗi**

- **Tầng Liên kết Dữ liệu** thực hiện kiểm tra lỗi trong quá trình truyền tải bằng cách sử dụng **Cyclic Redundancy Check (CRC)** hoặc **Check-sum**. Đây là một giá trị được tính toán từ dữ liệu và gửi kèm theo khung để kiểm tra tính toàn vẹn của dữ liệu khi đến đích.

  - Khi thiết bị nhận được khung, nó tính toán lại CRC từ dữ liệu nhận được và so sánh với giá trị CRC đã gửi. Nếu có sự khác biệt, thiết bị sẽ biết rằng dữ liệu bị lỗi và có thể yêu cầu gửi lại.

4. **Quản lý truy cập phương tiện (Media Access Control)**

- Tầng Liên kết Dữ liệu cũng có trách nhiệm điều phối việc **truy cập vào phương tiện truyền dẫn** khi nhiều thiết bị cùng chia sẻ một kênh truyền dẫn, ví dụ như trong mạng LAN Ethernet.

  - Một số giao thức được sử dụng để quản lý truy cập phương tiện, trong đó **CSMA/CD (Carrier Sense Multiple Access with Collision Detection)** là một giao thức phổ biến trong mạng Ethernet.
  
  - **CSMA/CD** hoạt động như sau:
    - **Carrier Sense**: Trước khi thiết bị bắt đầu truyền, nó lắng nghe kênh để kiểm tra xem có thiết bị nào khác đang truyền không.
    - **Multiple Access**: Tất cả các thiết bị đều có quyền truy cập vào kênh truyền dẫn.
    - **Collision Detection**: Nếu hai thiết bị truyền cùng lúc và xảy ra va chạm (collision), chúng sẽ dừng lại và gửi tín hiệu báo hiệu để yêu cầu truyền lại sau một khoảng thời gian ngẫu nhiên.

5. **Xử lý sự cố (Error Handling)**

- **Phát hiện lỗi**: Tầng Liên kết Dữ liệu phát hiện lỗi thông qua việc sử dụng các phương pháp như **CRC**, nhưng việc **sửa lỗi** không phải là trách nhiệm của lớp này. Nếu lỗi được phát hiện trong khung dữ liệu, lớp Liên kết Dữ liệu sẽ yêu cầu gửi lại dữ liệu, tuy nhiên, việc sửa lỗi thực sự được thực hiện ở các tầng cao hơn (như Tầng Giao Vận).

- **Điều chỉnh dòng dữ liệu**: Để tránh quá tải và đảm bảo dữ liệu không bị mất hoặc hỏng, lớp Liên kết Dữ liệu có thể điều chỉnh dòng dữ liệu và đảm bảo sự đồng bộ giữa các thiết bị trong mạng.

6. **Chuyển tiếp và truyền khung**

- **Truyền và nhận khung**: Sau khi khung được đóng gói và kiểm tra, nó sẽ được truyền từ một thiết bị tới thiết bị khác trong mạng. Thiết bị nhận sẽ giải mã khung và chuyển tiếp dữ liệu lên các tầng cao hơn của mô hình OSI, bắt đầu từ **Tầng Mạng**.

- Các giao thức ở Tầng Liên kết Dữ liệu (như **Ethernet**, **PPP**, **HDLC**) định nghĩa cách thức truyền tải khung và quy định các quy tắc liên quan đến việc gửi, nhận, phát hiện và xử lý lỗi.

7. **Điều khiển luồng (Flow Control)**

- **Điều khiển luồng** là cơ chế để kiểm soát lượng dữ liệu được truyền đi giữa các thiết bị. Trong trường hợp các thiết bị truyền tải dữ liệu quá nhanh và thiết bị nhận không thể xử lý kịp, Tầng Liên kết Dữ liệu sẽ giúp điều chỉnh tốc độ truyền để tránh mất mát dữ liệu.

Tóm lại quy trình hoạt động của **Tầng Liên kết Dữ liệu (Data Link Layer)**:

1. Nhận dữ liệu từ Tầng Mạng và đóng gói thành các khung.
2. Thêm địa chỉ MAC nguồn và đích vào khung.
3. Kiểm tra tính toàn vẹn của dữ liệu (sử dụng CRC hoặc các phương pháp khác).
4. Quản lý việc truy cập phương tiện truyền dẫn (như CSMA/CD).
5. Truyền khung dữ liệu qua phương tiện truyền dẫn và phát hiện lỗi.
6. Điều khiển luồng và xử lý các sự cố về dữ liệu.
7. Chuyển tiếp dữ liệu lên các tầng cao hơn khi khung dữ liệu được nhận.


**Các Giao thức và Tiêu chuẩn của Lớp Liên kết Dữ liệu**


3. **PPP (Point-to-Point Protocol)**:
   - Cho phép truyền thông qua đường dây điện thoại hoặc liên kết dữ liệu nối tiếp, thường được sử dụng trong kết nối internet qua điện thoại.

4. **ARP (Address Resolution Protocol)**:
 -  **ARP (Address Resolution Protocol)** là một giao thức thuộc **Tầng 2 (Data Link Layer)** trong mô hình OSI, mặc dù nó liên quan đến việc ánh xạ địa chỉ **IP** (Tầng 3 - Network Layer) sang địa chỉ **MAC** (Media Access Control) ở Tầng 2.

**Chức năng của ARP trong Data Link Layer:**
- **ARP** được sử dụng để **chuyển đổi địa chỉ IP** (mà các giao thức ở Tầng 3 như IPv4 sử dụng) thành địa chỉ **MAC** (mà Tầng 2, hay Data Link Layer, sử dụng để giao tiếp trong mạng vật lý).
- Khi một thiết bị mạng muốn gửi dữ liệu đến một thiết bị khác trong cùng một mạng cục bộ, nó cần biết địa chỉ MAC của thiết bị đích. Tuy nhiên, nếu chỉ có địa chỉ IP của thiết bị đích, thì ARP sẽ giúp xác định địa chỉ MAC tương ứng.

**Quá trình hoạt động của ARP:**

**Thiết bị A (có địa chỉ IP) muốn gửi gói dữ liệu đến Thiết bị B (có địa chỉ IP) trong cùng mạng LAN**:
   - Thiết bị A có địa chỉ IP của thiết bị B nhưng không biết địa chỉ MAC của nó.
   - Thiết bị A sẽ gửi một **ARP request** (Yêu cầu ARP) vào mạng LAN để tìm địa chỉ MAC của thiết bị B.

**ARP Request**:
   - **ARP Request** là một gói tin broadcast được gửi từ thiết bị A đến tất cả các thiết bị trong mạng LAN, yêu cầu **"Ai có địa chỉ IP này?"**.
   - Cấu trúc của ARP Request:
     - **Sender MAC address**: Địa chỉ MAC của thiết bị gửi (A).
     - **Sender IP address**: Địa chỉ IP của thiết bị gửi (A).
     - **Target MAC address**: Để trống (do chưa biết).
     - **Target IP address**: Địa chỉ IP của thiết bị đích (B).

**ARP Reply**:
   - Thiết bị B nhận được ARP Request và **phản hồi bằng một ARP Reply**, trong đó bao gồm **địa chỉ MAC** của thiết bị B.
   - Cấu trúc của ARP Reply:
     - **Sender MAC address**: Địa chỉ MAC của thiết bị B.
     - **Sender IP address**: Địa chỉ IP của thiết bị B.
     - **Target MAC address**: Địa chỉ MAC của thiết bị A.
     - **Target IP address**: Địa chỉ IP của thiết bị A.

**Lưu trữ trong ARP Cache**:
   - Sau khi nhận được ARP Reply, thiết bị A lưu địa chỉ MAC của thiết bị B vào **ARP cache** của nó, để lần sau không cần phải gửi yêu cầu ARP nữa khi gửi dữ liệu tới thiết bị B.

**Ví dụ:**
Giả sử:
- **Thiết bị A** có địa chỉ IP `192.168.1.10` và **địa chỉ MAC** `00:14:22:01:23:45`.
- **Thiết bị B** có địa chỉ IP `192.168.1.20` và **địa chỉ MAC** `00:14:22:67:89:01`.

Khi **Thiết bị A** muốn gửi dữ liệu tới **Thiết bị B**:
- Thiết bị A biết địa chỉ IP của thiết bị B là `192.168.1.20`, nhưng không biết địa chỉ MAC của thiết bị B.
- Thiết bị A gửi một **ARP request** tới tất cả các thiết bị trong mạng LAN với yêu cầu tìm kiếm **MAC address** tương ứng với IP `192.168.1.20`.
- **Thiết bị B** nhận được ARP request và gửi lại một **ARP reply**, cung cấp địa chỉ MAC của nó (`00:14:22:67:89:01`).
- Thiết bị A lưu địa chỉ MAC của thiết bị B trong **ARP cache** và tiếp tục gửi dữ liệu tới thiết bị B qua địa chỉ MAC đó.


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

##### **Tầng 3 - Network Layer**

**Lớp Mạng (Network Layer) trong Mô hình OSI**

Lớp Mạng là lớp thứ ba trong mô hình OSI, có vai trò quan trọng trong việc định tuyến gói tin qua mạng, điều phối dữ liệu giữa các mạng khác nhau, và đảm bảo rằng dữ liệu được gửi đến đúng đích. Lớp này xử lý các vấn đề liên quan đến định tuyến gói dữ liệu từ nguồn đến đích, kể cả khi các thiết bị nguồn và đích nằm trên các mạng khác nhau.

**Chức năng chính của Lớp Mạng**

- Nói chung là đóng gói, xử lý, định tuyến dữ liệu

1. **Định tuyến (Routing):**
   - Xác định đường đi tối ưu cho gói tin từ nguồn đến đích.
   - Sử dụng các bảng định tuyến và thuật toán định tuyến để đưa ra quyết định về đường đi cho mỗi gói tin.

2. **Phân đoạn và Tái lắp ráp (Fragmentation and Reassembly):**
   - Chia gói tin lớn (packets) thành các phân đoạn nhỏ hơn phù hợp với kích thước tối đa mà mạng có thể xử lý (MTU) và tái lắp ráp chúng ở đầu cuối nhận.

3. **Địa chỉ hóa logic (Logical Addressing):**
   - Sử dụng địa chỉ IP để xác định địa chỉ nguồn và đích cho mỗi gói tin.
   - Địa chỉ IP cho phép định tuyến qua các mạng phức tạp và đa dạng.

4. **Xử lý các gói dữ liệu:**
   - Xử lý các gói dữ liệu bao gồm các header với thông tin về định tuyến và điều khiển.

5. **Kiểm soát lỗi:**
   - Phát hiện và xử lý lỗi trong các gói dữ liệu như lỗi định tuyến hoặc địa chỉ không hợp lệ.

**Quy trình hoạt động**


1. **Nhận Dữ Liệu từ Tầng Liên Kết Dữ Liệu**:  
   - Tầng Mạng nhận khung (frame) từ Tầng Liên Kết Dữ Liệu, trong đó có dữ liệu gói (packet) được Tầng Mạng xử lý tiếp.
   
2. **Thêm Địa Chỉ IP (Logical Addressing)**:  
   - Tầng Mạng thêm **địa chỉ IP nguồn** và **địa chỉ IP đích** vào gói dữ liệu. Địa chỉ IP của thiết bị nguồn và thiết bị đích sẽ được đặt vào phần Header của gói dữ liệu (Packet).
   - Tầng này có thể xử lý các giao thức khác nhau như IPv4 và IPv6.

3. **Xử Lý Định Tuyến (Routing)**:  
   - Tầng Mạng sử dụng các thông tin về địa chỉ IP và **bảng định tuyến** (routing table) để xác định đường đi tốt nhất cho gói dữ liệu từ nguồn đến đích. 
   - Nếu gói dữ liệu cần đi qua nhiều mạng, Tầng Mạng sẽ gửi gói đến router phù hợp (thường là router gần nhất), sau đó router tiếp theo sẽ tiếp tục xử lý.

4. **Phân Mảnh Gói Dữ Liệu (Fragmentation)**:  
   - Nếu kích thước của gói dữ liệu lớn hơn MTU (Maximum Transmission Unit) của một mạng, Tầng Mạng sẽ **phân mảnh** gói thành các phần nhỏ hơn để có thể truyền tải qua mạng đó. 
   - Mỗi mảnh sẽ có thông tin về thứ tự để có thể được ghép lại ở phía nhận. Các phần nhỏ này sẽ được ghép lại ở đích sau khi truyền xong.
6. **Xử Lý Địa Chỉ Đích và Đưa Dữ Liệu Đến Router Tiếp Theo**
   - Tầng Mạng sẽ sử dụng địa chỉ IP đích để xác định router tiếp theo mà gói dữ liệu cần phải đi qua.   
   - Nếu đích nằm trong cùng một mạng, gói sẽ được gửi trực tiếp đến đích.   
   - Nếu đích nằm ngoài mạng hiện tại, gói sẽ được gửi đến router để tiếp tục quá trình định tuyến.

7. **Truyền Dữ Liệu qua Mạng (Forwarding)**:  
   - Sau khi gói dữ liệu được xử lý (định tuyến, phân mảnh nếu cần), Tầng Mạng gửi gói dữ liệu xuống Tầng Liên Kết Dữ Liệu của thiết bị tiếp theo (router hoặc thiết bị đích) để tiếp tục quá trình truyền tải.
   - Mỗi thiết bị trên đường đi sẽ xử lý gói dữ liệu, kiểm tra địa chỉ và chuyển tiếp nó đến thiết bị tiếp theo.

8. **Khi Đến Đích Cuối Cùng**:  
   - Khi gói dữ liệu đến đích cuối cùng, Tầng Mạng sẽ giao gói cho Tầng Liên Kết Dữ Liệu của thiết bị đích. Sau đó, dữ liệu sẽ được chuyển tiếp lên Tầng Vận Chuyển (Transport Layer) để tiếp tục xử lý theo giao thức ứng dụng (ví dụ TCP, UDP).


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

##### **Tầng 4 - Transport Layer (Tầng vận chuyển)**

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


1. **Nhận Dữ Liệu Từ Tầng Mạng**
- **Tầng Vận Chuyển** nhận dữ liệu từ **Tầng Mạng (Network Layer)** dưới dạng các gói (packets). Tầng này không chỉ xử lý dữ liệu mà còn đảm bảo dữ liệu được gửi đến đúng ứng dụng và duy trì các tính năng quan trọng như kiểm soát lỗi, kiểm soát luồng và phân đoạn.

2. **Phân Đoạn và Đóng Gói Dữ Liệu (Segmentation and Reassembly)**
- Tầng Vận Chuyển chia nhỏ dữ liệu lớn từ ứng dụng thành các **đoạn (segments)** nếu cần thiết để dễ dàng truyền tải qua mạng.
  - **Phân đoạn**: Dữ liệu từ ứng dụng được chia thành các đoạn nhỏ.
  - **Đóng gói**: Mỗi đoạn sẽ có thông tin như **địa chỉ cổng (port address)** của ứng dụng đích, giúp dữ liệu đến đúng ứng dụng ở phía nhận.

3. **Định Danh Ứng Dụng Bằng Cổng (Port Addressing)**
- Tầng Vận Chuyển sử dụng **cổng mạng** (port) để xác định ứng dụng nào trên thiết bị đích sẽ nhận dữ liệu.
  - Ví dụ: **Cổng 80** dành cho HTTP, **Cổng 443** dành cho HTTPS.
  - Mỗi đoạn dữ liệu sẽ được đánh dấu với số cổng nguồn và cổng đích để giúp định hướng dữ liệu đúng ứng dụng tại thiết bị đích.

4. **Cung Cấp Kết Nối Tin Cậy (Reliable Connection)**
- Tầng Vận Chuyển có thể sử dụng giao thức như **TCP** (Transmission Control Protocol) để tạo một kết nối đáng tin cậy giữa hai thiết bị, đảm bảo rằng dữ liệu được truyền không bị mất và đúng thứ tự.
  - **TCP** thực hiện:
    - **Thiết lập kết nối**: Cả hai bên sẽ "bắt tay" (handshake) để thiết lập kết nối (3-way handshake).
    - **Kiểm tra lỗi**: Mỗi đoạn dữ liệu sẽ có một **mã kiểm tra (checksum)** để phát hiện lỗi trong quá trình truyền.
    - **Đảm bảo truyền tải đúng thứ tự**: TCP sẽ đảm bảo rằng các đoạn dữ liệu đến đúng thứ tự, không bị mất mát.
    - **Xác nhận và yêu cầu lại**: Người nhận sẽ gửi tín hiệu xác nhận (ACK) để thông báo việc nhận dữ liệu thành công. Nếu không nhận được xác nhận, dữ liệu sẽ được gửi lại.

5. **Quản Lý Lưu Lượng (Flow Control)**
- Tầng Vận Chuyển sử dụng cơ chế **kiểm soát lưu lượng** để đảm bảo rằng thiết bị nhận không bị quá tải với quá nhiều dữ liệu.
  - **Windowing**: Ví dụ, TCP sử dụng **windowing** để giới hạn số lượng đoạn dữ liệu có thể được gửi đi trước khi nhận được xác nhận từ phía người nhận. Điều này giúp điều chỉnh tốc độ truyền để tránh tình trạng tràn băng thông.

6. **Điều Kiện Lỗi và Khôi Phục (Error Handling and Recovery)**
- Nếu có lỗi trong quá trình truyền tải, Tầng Vận Chuyển sẽ đảm bảo khôi phục dữ liệu thông qua:
  - **Phát hiện lỗi**: Sử dụng **checksum** để phát hiện lỗi trong các đoạn dữ liệu.
  - **Tái truyền**: Nếu có lỗi, dữ liệu sẽ được yêu cầu gửi lại (nếu sử dụng TCP).
  
7. **Đóng Kết Nối (Connection Termination)**
- Khi dữ liệu đã được truyền xong, Tầng Vận Chuyển sẽ thực hiện **đóng kết nối** giữa hai thiết bị.
  - Với TCP, việc đóng kết nối diễn ra qua một quá trình gọi là **4-way handshake**, đảm bảo rằng cả hai bên đều đã nhận và xử lý hết dữ liệu.

8. **Truyền Dữ Liệu Đến Tầng Ứng Dụng**
- Sau khi dữ liệu được phân đoạn, kiểm tra lỗi và đảm bảo tính toàn vẹn, Tầng Vận Chuyển sẽ chuyển các đoạn dữ liệu tới **Tầng Ứng Dụng** của thiết bị nhận.
  - Tầng Ứng Dụng sẽ nhận và sử dụng dữ liệu này cho các mục đích như trình duyệt web, gửi email, hay các ứng dụng khác.

Tóm lại, quy trình hoạt động của **Tầng Vận Chuyển (Transport Layer)** bao gồm:

1. Nhận dữ liệu từ Tầng Mạng và phân đoạn dữ liệu thành các đoạn nhỏ (segments).
2. Đảm bảo truyền tải tin cậy với các cơ chế như **3-way handshake** (cho TCP), **kiểm soát lỗi** và **tái truyền** khi cần thiết.
3. Quản lý lưu lượng để tránh quá tải và đảm bảo hiệu quả truyền tải.
4. Đóng kết nối khi dữ liệu đã được truyền xong.
5. Chuyển tiếp dữ liệu đã xử lý đến Tầng Ứng Dụng để sử dụng.


##### **Tầng 5 - Session Layer (Tầng phiên)**

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

##### **Tầng 6 - Presentation Layer (Tầng trình bày)**

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

##### **Tầng 7 - Application Layer ( Tầng ứng dụng)**

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

-------------------------------------------------------------------

### **Quá trình nhận dữ liệu từ các tầng thấp (Decapsulation)**  

**1. Tầng 1: Vật lý (Physical Layer)**  
- **Dữ liệu nhận được**: Tín hiệu vật lý (sóng điện, ánh sáng, sóng vô tuyến).  
- **Hoạt động**: 
  - Tín hiệu vật lý được chuyển đổi thành chuỗi bit (0 và 1).  
  - Chuỗi bit này được chuyển lên tầng 2 để xử lý.  

**2. Tầng 2: Liên kết dữ liệu (Data Link Layer)**  
- **Dữ liệu nhận được**: Chuỗi bit từ tầng Vật lý.  
- **Hoạt động**:  
  1. **Tổ chức lại các bit thành khung dữ liệu (frame)**:  
     - Dựa trên cấu trúc frame để xác định ranh giới giữa các khung.
  2. **Kiểm tra lỗi (Error Detection)**:  
     - Sử dụng thông tin từ **trailer** (thường là CRC - Cyclic Redundancy Check) để kiểm tra tính toàn vẹn của dữ liệu.  
     - Nếu phát hiện lỗi, khung sẽ bị loại bỏ hoặc yêu cầu gửi lại (tùy giao thức).  
  3. **Phân tích Header của khung**:  
     - Đọc địa chỉ MAC nguồn và MAC đích.  
     - Kiểm tra địa chỉ MAC đích để xác định khung này có phải dành cho thiết bị nhận hay không.  
  4. **Loại bỏ Header và Trailer của tầng 2**:  
     - Chỉ giữ lại **payload** (gói tin) và chuyển lên tầng 3.  

**3. Tầng 3: Mạng (Network Layer)**  
- **Dữ liệu nhận được**: Gói tin (packet) từ tầng Liên kết dữ liệu.  
- **Hoạt động**:  
  1. **Phân tích Header của gói tin**:  
     - Đọc địa chỉ IP nguồn và đích.  
     - Kiểm tra địa chỉ IP đích để xác định gói tin này có thuộc về thiết bị nhận hay không.  
  2. **Định tuyến nội bộ (Local Routing)**:  
     - Nếu gói tin thuộc về thiết bị nhận, dữ liệu được xử lý tiếp.  
     - Nếu không, gói tin sẽ bị bỏ qua hoặc chuyển tiếp (nếu là router).  
  3. **Loại bỏ Header của tầng 3**:  
     - Chuyển payload (phân đoạn) lên tầng 4.  

**4. Tầng 4: Giao vận (Transport Layer)**  
- **Dữ liệu nhận được**: Phân đoạn (segment) từ tầng Mạng.  
- **Hoạt động**:  
  1. **Phân tích Header của phân đoạn**:  
     - Đọc số cổng (Port Number) để xác định ứng dụng nhận dữ liệu (ví dụ: HTTP, FTP).  
  2. **Tái tạo dữ liệu**:  
     - Nếu dữ liệu bị chia thành nhiều phân đoạn, tầng này sẽ tái tạo lại dữ liệu theo thứ tự đúng (dựa vào thông tin trong header, như số thứ tự).  
  3. **Loại bỏ Header của tầng 4**:  
     - Chuyển dữ liệu thô lên tầng 5.  

**5-7. Tầng Phiên, Trình bày, Ứng dụng (Session, Presentation, Application Layers)**  
- **Dữ liệu nhận được**: Dữ liệu thô từ tầng Giao vận.  
- **Hoạt động**:  
  1. **Tầng Phiên (Session Layer)**:  
     - Quản lý phiên giao tiếp giữa các ứng dụng (nếu cần).  
  2. **Tầng Trình bày (Presentation Layer)**:  
     - Giải mã, giải nén, hoặc chuyển đổi dữ liệu về định dạng mà ứng dụng có thể hiểu được.  
  3. **Tầng Ứng dụng (Application Layer)**:  
     - Dữ liệu được chuyển đến ứng dụng cuối (ví dụ: trình duyệt hiển thị trang web, ứng dụng email tải tin nhắn).  

**Tóm tắt Quá trình Decapsulation**  

1. **Tầng 1**: Chuyển tín hiệu vật lý thành bit.  
2. **Tầng 2**: Tổ chức bit thành khung, kiểm tra lỗi, phân tích địa chỉ MAC.  
3. **Tầng 3**: Kiểm tra địa chỉ IP, định tuyến, loại bỏ header IP.  
4. **Tầng 4**: Xác định ứng dụng đích qua số cổng, tái tạo dữ liệu từ các phân đoạn.  
5. **Tầng 5-7**: Giải mã và chuyển dữ liệu đến ứng dụng cuối.  

**Minh họa trực quan**
- **Dữ liệu gốc (Data)** → **Phân đoạn (Segment)** → **Gói tin (Packet)** → **Khung (Frame)** → **Tín hiệu vật lý (Bits)** (Khi gửi đi).  
- **Tín hiệu vật lý (Bits)** → **Khung (Frame)** → **Gói tin (Packet)** → **Phân đoạn (Segment)** → **Dữ liệu gốc (Data)** (Khi nhận về).  


----------------------------------------------------------------------
-------------------------------------------------------------------


### **TCP/IP (Transmission Control Protocol/Internet Protocol)**

#### **1. TCP/IP là gì** 

- là một bộ giao thức mạng được sử dụng để truyền tải dữ liệu qua các mạng máy tính. TCP/IP là một giao thức liên kết hai tầng, bao gồm tầng TCP và tầng IP, mỗi tầng thực hiện các chức năng riêng biệt nhưng hỗ trợ lẫn nhau để đảm bảo việc truyền tải dữ liệu hiệu quả.

#### **2. IP (Internet Protocol)**

**Định danh thiết bị**
- Mỗi thiết bị trong mạng được cấp 1 địa chỉ IP để định danh thiết bị và để chúng có thể giao tiếp với nhau. Giống như mỗi nhà có 1 địa chỉ riêng để nhận thư, mỗi thiết bị trên mạng cần một địa chỉ IP để nhận và gửi dữ liệu.

**Định tuyến dữ liệu (Routing)**
- Quá trình tìm đường đi tối ưu để các gói tin di chuyển từ thiết bị nguồn đến thiết bị đích qua mạng.
- Nếu gói tin quá lớn để truyền qua 1 mạng, nó sẽ được phân mảnh thành các gói nhỏ (chứa địa chỉ IP nguồn, đích), mỗi mảnh sẽ có 1 header (tiêu đề) chứa thông tin vị trí. Mỗi mạng có giới hạn kích thước gói tin mà nó có thể truyền (gọi là MTU - Maximum Transmission Unit). Gói tin được gửi từ thiết bị nguồn => Đi qua Router (thiết bị trung gian trên mạng internet): Router đọc địa chỉ IP đích và định tuyến gói tin đến mạng tiếp theo. Khi đến đích, thiết bị đích sẽ dùng thông tin trong tiêu đề để ghép các mảnh lại đúng thứ tự, tạo thành gói tin ban đầu.
- **Vấn đề phát sinh:**
Nếu một mảnh bị mất trong quá trình truyền, thiết bị đích không thể lắp ráp gói tin đầy đủ. Khi đó, giao thức cao hơn (như TCP) sẽ yêu cầu gửi lại gói tin.

- Hoạt động ở Network Layer trong mô hình OSI và ở Internet Layer của TCP/IP

#### **3. TCP (Transmission Control Protocol)**

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

#### **4. Các tầng trong mô hình TCP/IP**

#### **Tầng 4 - Application Layer (Tầng ứng dụng)**

##### **Tầng Ứng dụng (Application Layer) trong Mô hình TCP/IP**

Trong mô hình TCP/IP, tầng Ứng dụng là tầng cao nhất và có vai trò cực kỳ quan trọng trong việc cung cấp giao diện cho các ứng dụng để truy cập vào các dịch vụ mạng. Tầng này không chỉ đảm nhận trách nhiệm cung cấp các dịch vụ cho các ứng dụng mà còn giúp đơn giản hóa quá trình trao đổi thông tin giữa người dùng và mạng.

##### **Chức năng chính của Tầng Ứng dụng**
Chức năng chính của **Application Layer** trong mô hình **TCP/IP** là cung cấp các dịch vụ mạng trực tiếp cho các ứng dụng người dùng và quản lý giao tiếp giữa các ứng dụng trên các hệ thống khác nhau. Đây là lớp cao nhất trong mô hình TCP/IP và có các chức năng quan trọng sau:

1. **Cung cấp dịch vụ mạng cho ứng dụng người dùng**
   - Application Layer cung cấp các giao thức và API (Application Programming Interface) cho các ứng dụng để sử dụng các dịch vụ mạng. Các ứng dụng này có thể bao gồm trình duyệt web, phần mềm email, phần mềm FTP, phần mềm chat, v.v.
   - Ví dụ:
     - **HTTP/HTTPS** cho trình duyệt web.
     - **FTP** cho truyền tệp.
     - **SMTP, POP3, IMAP** cho giao tiếp qua email.

2. **Định nghĩa giao thức ứng dụng**
   - Lớp này xác định các giao thức mà các ứng dụng sẽ sử dụng để giao tiếp qua mạng. Mỗi giao thức có các quy tắc riêng để định dạng, truyền tải và xử lý dữ liệu.
   - Các giao thức phổ biến trong Application Layer bao gồm:
     - **HTTP/HTTPS**: Giao thức truyền tải siêu văn bản cho các trang web.
     - **FTP**: Giao thức truyền tải tệp giữa các máy tính.
     - **DNS**: Giao thức phân giải tên miền thành địa chỉ IP.
     - **SMTP/IMAP/POP3**: Giao thức gửi và nhận email.
     - **Telnet/SSH**: Giao thức truy cập từ xa vào các hệ thống máy tính.

3. **Quản lý giao tiếp giữa các ứng dụng**
   - Application Layer điều phối và quản lý giao tiếp giữa các ứng dụng trên các hệ thống mạng khác nhau. Dữ liệu được gửi từ một ứng dụng trên máy tính nguồn, được đóng gói theo giao thức ứng dụng (ví dụ HTTP hoặc FTP), và sau đó truyền đến ứng dụng tương ứng trên máy tính đích.

4. **Xử lý và định dạng dữ liệu ứng dụng**
   - Lớp ứng dụng cũng có thể xử lý và định dạng dữ liệu trước khi gửi hoặc sau khi nhận, tùy thuộc vào giao thức sử dụng. Ví dụ:
     - **HTTP** sẽ định dạng các yêu cầu và phản hồi dưới dạng các HTTP request và response, bao gồm các header, body, và mã trạng thái.
     - **SMTP** sẽ định dạng email theo một cấu trúc đặc biệt để có thể gửi qua mạng.

5. **Cung cấp dịch vụ bảo mật và mã hóa**
   - Một số giao thức ứng dụng trong lớp này có chức năng bảo mật, mã hóa dữ liệu để đảm bảo an toàn trong quá trình truyền tải thông tin. Ví dụ, **HTTPS** sử dụng SSL/TLS để mã hóa dữ liệu giữa trình duyệt và máy chủ.
   
6. **Chuyển dữ liệu giữa lớp ứng dụng và lớp Transport**
   - Lớp ứng dụng sẽ đóng gói và chuyển dữ liệu đến lớp Transport (TCP hoặc UDP) để xử lý việc truyền tải và quản lý kết nối. Ngược lại, dữ liệu nhận từ lớp Transport sẽ được truyền lại cho lớp ứng dụng để xử lý.
   
7. **Quản lý kết nối và ngắt kết nối**
   - Lớp ứng dụng tham gia vào quá trình thiết lập kết nối và ngắt kết nối giữa các hệ thống khi cần thiết. Tuy nhiên, việc duy trì kết nối và đảm bảo sự tin cậy trong việc truyền tải dữ liệu chủ yếu là công việc của lớp Transport (ví dụ TCP).

8. **Cung cấp khả năng tương tác giữa các ứng dụng khác nhau**
   - Lớp ứng dụng cho phép các ứng dụng khác nhau (dù được phát triển bằng các ngôn ngữ khác nhau hoặc trên các nền tảng khác nhau) có thể giao tiếp với nhau qua mạng mà không cần quan tâm đến chi tiết của các lớp thấp hơn trong mô hình TCP/IP.

Tóm tắt các chức năng chính của **Application Layer**:

1. Cung cấp giao thức mạng cho ứng dụng người dùng.
2. Định dạng và xử lý dữ liệu ứng dụng.
3. Quản lý giao tiếp giữa các ứng dụng trên các hệ thống khác nhau.
4. Hỗ trợ bảo mật và mã hóa thông tin.
5. Quản lý kết nối và ngắt kết nối.
6. Cung cấp giao thức và API cho các dịch vụ mạng.

##### **Quy trình hoạt động**

1. **Khởi tạo kết nối (Connection Initiation)**
   - Khi một ứng dụng muốn gửi dữ liệu, lớp ứng dụng sẽ yêu cầu lớp truyền tải (Transport Layer) thiết lập kết nối tới máy tính đích. Ví dụ, trong trường hợp của giao thức TCP, lớp Ứng dụng có thể yêu cầu lớp Transport để thực hiện quá trình "three-way handshake" để thiết lập kết nối TCP.

2. **Đóng gói dữ liệu (Data Packaging)**
   - Dữ liệu từ ứng dụng được đóng gói thành các đơn vị có cấu trúc theo yêu cầu của giao thức trong lớp ứng dụng, ví dụ HTTP, FTP, hoặc SMTP.
   - Dữ liệu này sau đó được chuyển giao cho lớp Transport để đóng gói thành các segment TCP hoặc UDP. Ví dụ, nếu ứng dụng sử dụng HTTP, nó sẽ tạo ra các yêu cầu HTTP, có thể là một dòng lệnh GET hoặc POST.

3. **Xử lý giao thức ứng dụng (Application Protocol Processing)**
   - Lớp ứng dụng chịu trách nhiệm xử lý các giao thức cụ thể như HTTP, FTP, DNS, SMTP, v.v.
   - **HTTP**: Chuyển giao các yêu cầu từ trình duyệt (client) đến máy chủ web và trả về dữ liệu dưới dạng HTML, CSS, JavaScript.
   - **FTP**: Cung cấp các chức năng truyền tệp giữa các hệ thống.
   - **DNS**: Chuyển đổi tên miền (domain name) thành địa chỉ IP.

4. **Chuyển dữ liệu đến lớp Transport (Data Transfer to Transport Layer)**
   - Sau khi xử lý xong dữ liệu, lớp ứng dụng sẽ chuyển tiếp dữ liệu này đến lớp Transport. Tại đây, lớp Transport sẽ xác định xem giao thức nào sẽ được sử dụng (TCP hoặc UDP), chia dữ liệu thành các segment (TCP) hoặc datagram (UDP), và cung cấp thông tin quản lý kết nối (đối với TCP).

5. **Quản lý dữ liệu từ lớp Transport (Receive Data from Transport Layer)**
   - Khi lớp Transport nhận được dữ liệu từ lớp Mạng, nó sẽ gửi dữ liệu này đến lớp Ứng dụng.
   - Lớp ứng dụng sẽ nhận dữ liệu, giải mã nó theo giao thức thích hợp (ví dụ: giải mã HTTP response, kiểm tra mã trạng thái của HTTP, v.v.), và sau đó gửi dữ liệu cho ứng dụng sử dụng.

6. **Đóng kết nối (Connection Termination)**
   - Khi ứng dụng không còn cần kết nối nữa, lớp ứng dụng sẽ yêu cầu lớp Transport đóng kết nối, thực hiện các thao tác cần thiết để ngắt kết nối.

**Tóm tắt quy trình:**
 
1. **Ứng dụng yêu cầu dịch vụ**: Người dùng hoặc ứng dụng yêu cầu một dịch vụ mạng.
2. **Đóng gói dữ liệu theo giao thức ứng dụng**: Dữ liệu từ ứng dụng được đóng gói theo đúng giao thức ứng dụng (HTTP, FTP, v.v.).
3. **Chuyển giao cho lớp Transport**: Dữ liệu được chuyển tới lớp Transport (TCP hoặc UDP) để tiếp tục xử lý.
4. **Kết nối và truyền tải dữ liệu**: Dữ liệu được chuyển tiếp qua các lớp thấp hơn (Lớp Mạng, Lớp Liên kết Dữ liệu, v.v.) và đến máy đích.
5. **Nhận dữ liệu và phản hồi**: Dữ liệu nhận từ máy đích được giải mã và trả về cho ứng dụng.
6. **Kết thúc kết nối**: Sau khi hoàn thành, kết nối sẽ được đóng lại.



#####**Giao thức phổ biến của Tầng Ứng dụng**

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


------------------------------

#### **Tầng 3 - Transport Layer (Tầng vận chuyển)**

**Tầng Giao vận (Transport Layer) trong Mô hình TCP/IP**

Tầng Giao vận, hay còn gọi là Transport Layer, là lớp thứ tư trong mô hình TCP/IP, có nhiệm vụ quan trọng trong việc đảm bảo dữ liệu được truyền đi một cách tin cậy giữa các ứng dụng trên các thiết bị mạng. Tầng này cung cấp các dịch vụ kết nối từ điểm đến điểm, điều khiển lỗi, và quản lý luồng dữ liệu để giảm thiểu tình trạng mất mát và đảm bảo tính toàn vẹn của dữ liệu.

##### **Chức năng chính của Tầng Giao vận**

1. **Cung cấp giao thức truyền tải đáng tin cậy**
   - **Transport Layer** chịu trách nhiệm bảo đảm rằng dữ liệu được truyền từ ứng dụng này đến ứng dụng khác một cách chính xác và đáng tin cậy. Điều này bao gồm việc kiểm tra lỗi, xác nhận và đảm bảo các gói tin không bị mất.
   - Giao thức **TCP (Transmission Control Protocol)** là giao thức chính cung cấp tính năng này, đảm bảo rằng dữ liệu được gửi đến đúng thứ tự và không bị mất.
   
2. **Phân chia và tái hợp dữ liệu**
   - Lớp Transport chịu trách nhiệm phân chia dữ liệu từ **Application Layer** thành các đơn vị nhỏ gọi là **segments** (đối với TCP) hoặc **datagrams** (đối với UDP). Các segment này sẽ được chuyển đến lớp **Network Layer**.
   - Khi các segment được nhận từ lớp **Network Layer** ở máy đích, lớp **Transport Layer** sẽ tái hợp chúng lại thành dữ liệu gốc trước khi chuyển đến lớp **Application Layer**.

3. **Quản lý kết nối và thiết lập (Connection Management)**
   - **Transport Layer** quản lý việc thiết lập và ngắt kết nối giữa các ứng dụng trên các máy khác nhau. Nó đảm bảo rằng khi cần thiết, kết nối được thiết lập (ví dụ, qua TCP's three-way handshake) và khi không còn cần thiết nữa, kết nối sẽ được đóng lại.
   - Với **TCP**, khi thiết lập kết nối, lớp này sử dụng quy trình **three-way handshake** để đảm bảo rằng cả hai bên sẵn sàng cho việc truyền tải dữ liệu. Khi hoàn thành, kết nối có thể được đóng qua **four-way handshake**.

4. **Điều khiển lưu lượng (Flow Control)**
   - Lớp **Transport Layer** cung cấp cơ chế điều khiển lưu lượng để tránh tình trạng tắc nghẽn mạng. Điều này có nghĩa là lớp này có thể điều chỉnh tốc độ gửi dữ liệu giữa hai bên để tránh làm nghẽn hệ thống.
   - **TCP** sử dụng cơ chế **windowing** (cửa sổ điều khiển) để quản lý tốc độ truyền tải dữ liệu, cho phép người gửi điều chỉnh số lượng dữ liệu có thể gửi đi trước khi nhận được xác nhận từ người nhận.

5. **Điều khiển lỗi (Error Control)**
   - **Transport Layer** cung cấp cơ chế kiểm tra lỗi để đảm bảo rằng dữ liệu được truyền đi không bị sai sót. Điều này bao gồm việc sử dụng các mã kiểm tra (checksum) để kiểm tra sự toàn vẹn của dữ liệu.
   - Nếu một segment bị mất hoặc lỗi trong quá trình truyền tải, **TCP** sẽ yêu cầu gửi lại dữ liệu đó. Điều này không áp dụng cho **UDP**, vì UDP là một giao thức không tin cậy (connectionless) và không yêu cầu việc kiểm tra lỗi.

6. **Định danh ứng dụng qua cổng (Port Identification)**
   - Lớp Transport sử dụng cổng (ports) để phân biệt các ứng dụng khác nhau đang chạy trên một hệ thống. Mỗi ứng dụng sử dụng một **port number** cụ thể để giao tiếp với các ứng dụng trên các hệ thống khác. Ví dụ:
     - **Port 80** cho HTTP.
     - **Port 443** cho HTTPS.
     - **Port 25** cho SMTP.
   - Các port này giúp lớp Transport xác định và chuyển giao dữ liệu đúng đến ứng dụng nhận.

7. **Giao thức có kết nối và không có kết nối**
   - **Transport Layer** cung cấp cả giao thức có kết nối (connection-oriented) và không có kết nối (connectionless).
     - **TCP** là giao thức có kết nối, nghĩa là nó thiết lập và duy trì một kết nối giữa các hệ thống trước khi truyền tải dữ liệu.
     - **UDP (User Datagram Protocol)** là giao thức không có kết nối, nghĩa là nó gửi dữ liệu mà không thiết lập kết nối, phù hợp cho các ứng dụng cần tốc độ cao mà không yêu cầu độ tin cậy tuyệt đối (ví dụ, video streaming, game trực tuyến).

8. **Quản lý phân phối dữ liệu (Multiplexing)**
   - Transport Layer thực hiện **multiplexing**, cho phép nhiều ứng dụng trên cùng một hệ thống có thể sử dụng mạng đồng thời. Nó phân phối các segment (hoặc datagrams) đến đúng ứng dụng bằng cách sử dụng cổng mạng (port numbers).

Tóm tắt các chức năng chính của **Transport Layer**:

1. **Cung cấp dịch vụ truyền tải tin cậy** (cho TCP) hoặc không tin cậy (cho UDP).
2. **Phân chia và tái hợp dữ liệu** giữa lớp ứng dụng và lớp mạng.
3. **Quản lý kết nối** giữa các ứng dụng, thiết lập và ngắt kết nối.
4. **Điều khiển lưu lượng** để tránh tắc nghẽn.
5. **Điều khiển lỗi** để đảm bảo tính toàn vẹn của dữ liệu.
6. **Định danh ứng dụng qua cổng** để phân biệt các ứng dụng khác nhau.
7. **Hỗ trợ giao thức có kết nối (TCP) và không có kết nối (UDP)**.
8. **Multiplexing** để nhiều ứng dụng có thể chia sẻ mạng cùng một lúc.


##### **Quy trình hoạt động**


1. **Nhận dữ liệu từ lớp ứng dụng (Application Layer)**
   - Khi một ứng dụng (ví dụ: trình duyệt web, phần mềm email) muốn gửi dữ liệu, dữ liệu này sẽ được truyền từ lớp **Application Layer** đến lớp **Transport Layer**.
   - Dữ liệu có thể là bất kỳ loại thông tin nào cần truyền tải, như một yêu cầu HTTP, email, tệp tin FTP, v.v.

2. **Đóng gói dữ liệu vào các đơn vị truyền tải**
   - **Transport Layer** sẽ đóng gói dữ liệu nhận được từ **Application Layer** thành các **segments** (hoặc **datagrams** nếu sử dụng UDP).
     - **TCP** sẽ thêm các thông tin điều khiển như số hiệu seq (sequence number), ack (acknowledgment number), checksum, cổng nguồn và cổng đích, cửa sổ (window size) vào header của segment.
     - **UDP** sẽ thêm các thông tin như cổng nguồn và cổng đích, chiều dài của datagram, và checksum vào header của datagram.

3. **Chọn giao thức truyền tải (TCP hoặc UDP)**
   - Lớp Transport sẽ quyết định sử dụng **TCP (Transmission Control Protocol)** hoặc **UDP (User Datagram Protocol)** dựa trên yêu cầu của ứng dụng:
     - **TCP** là giao thức có kết nối, cung cấp các tính năng bảo mật, kiểm tra lỗi, điều khiển lưu lượng và đảm bảo dữ liệu được truyền chính xác.
     - **UDP** là giao thức không có kết nối, nhanh hơn nhưng không đảm bảo tính toàn vẹn hoặc thứ tự của dữ liệu.

4. **Chuyển dữ liệu xuống lớp mạng (Network Layer)**
   - Sau khi dữ liệu đã được đóng gói vào các segment (hoặc datagrams), lớp **Transport Layer** sẽ chuyển các đơn vị này xuống lớp **Network Layer** (IP layer) để xử lý việc định tuyến và chuyển tiếp qua mạng.
   - Lớp **Network Layer** sẽ đóng gói dữ liệu thành các **packets** và xác định đường đi của dữ liệu đến máy đích.

5. **Thiết lập kết nối (cho TCP)**
   - Nếu giao thức TCP được chọn, trước khi truyền dữ liệu, lớp **Transport Layer** sẽ thiết lập một kết nối giữa hai hệ thống thông qua quá trình **three-way handshake**:
     1. **SYN**: Máy gửi gửi một gói tin SYN để yêu cầu thiết lập kết nối.
     2. **SYN-ACK**: Máy nhận trả lời với một gói tin SYN-ACK, xác nhận rằng kết nối có thể thiết lập.
     3. **ACK**: Máy gửi cuối cùng gửi một gói tin ACK để hoàn tất quá trình thiết lập kết nối.
   - Sau khi kết nối được thiết lập, dữ liệu có thể bắt đầu được truyền.

6. **Truyền dữ liệu (Data Transfer)**
   - **TCP**: Khi kết nối đã được thiết lập, dữ liệu sẽ được chia thành các segment nhỏ hơn và truyền qua mạng. Mỗi segment sẽ có số hiệu chuỗi (sequence number) để đảm bảo các segment được ghép lại đúng thứ tự khi đến đích.
   - **UDP**: Dữ liệu sẽ được gửi đi ngay lập tức mà không cần xác nhận, giúp tiết kiệm thời gian truyền tải nhưng không có đảm bảo về thứ tự hoặc độ tin cậy.

7. **Điều khiển lưu lượng (Flow Control)**
   - **TCP** sử dụng cơ chế **windowing** để điều khiển lưu lượng, điều này cho phép người gửi chỉ có thể gửi một số lượng dữ liệu xác định mà không cần chờ phản hồi từ người nhận.
     - **TCP** điều chỉnh kích thước cửa sổ (window size) dựa trên khả năng xử lý của máy nhận và tránh tình trạng nghẽn mạng.
     - Nếu quá nhiều dữ liệu được gửi mà không có phản hồi, sẽ dẫn đến tình trạng quá tải.

8. **Điều khiển lỗi và xác nhận (Error Control and Acknowledgment)**
   - **TCP** sử dụng **checksum** để kiểm tra lỗi trong quá trình truyền tải dữ liệu. Nếu một segment bị lỗi (dữ liệu bị thay đổi hoặc mất), máy nhận sẽ gửi yêu cầu gửi lại (retransmission).
   - Mỗi khi một segment được nhận thành công, máy nhận sẽ gửi lại một gói tin **ACK** (Acknowledge), xác nhận rằng dữ liệu đã được nhận đúng.
   - Nếu gói tin không được xác nhận trong một khoảng thời gian, máy gửi sẽ gửi lại gói tin đó.

9. **Ngắt kết nối (Connection Termination)**
   - Khi quá trình truyền tải dữ liệu hoàn tất, lớp **Transport Layer** sẽ thực hiện quá trình ngắt kết nối:
     - **TCP** sử dụng quy trình **four-way handshake** để ngắt kết nối:
       1. Máy gửi gửi một gói tin **FIN** yêu cầu đóng kết nối.
       2. Máy nhận xác nhận với một gói tin **ACK**.
       3. Máy nhận gửi một gói tin **FIN** cho biết nó cũng muốn ngắt kết nối.
       4. Máy gửi cuối cùng gửi lại một gói tin **ACK** để xác nhận quá trình ngắt kết nối.
   - Sau khi kết nối bị ngắt, không có dữ liệu nào sẽ được truyền.

10. **Truyền dữ liệu đến lớp ứng dụng đích**
   - Sau khi dữ liệu đã được truyền qua mạng và đến hệ thống đích, lớp **Transport Layer** trên máy đích sẽ xử lý và chuyển dữ liệu đến lớp **Application Layer** tương ứng.
   - Dữ liệu này sẽ được tái hợp lại từ các segment (cho TCP) hoặc datagrams (cho UDP) và chuyển giao cho ứng dụng nhận.


##### **Giao thức phổ biến của Tầng Giao vận**
1. **TCP (Transmission Control Protocol):**
   - Giao thức định hướng kết nối, cung cấp dịch vụ truyền dữ liệu đáng tin cậy. TCP đảm bảo rằng mọi gói tin đều được gửi tới điểm đích một cách chính xác và theo đúng thứ tự.

2. **UDP (User Datagram Protocol):**
   - Giao thức không định hướng kết nối, cung cấp một dịch vụ truyền dữ liệu nhanh nhưng không đáng tin cậy. UDP phù hợp với các ứng dụng đòi hỏi tốc độ cao và có thể chấp nhận một số mất mát dữ liệu, như trò chơi trực tuyến hoặc truyền phát video.

**Vai trò và Tác động của Tầng Giao vận**
- **Đảm bảo tính đáng tin cậy:** TCP và các giao thức khác tại tầng này đảm bảo dữ liệu được gửi một cách đáng tin cậy, ngay cả trong điều kiện mạng không ổn định.
- **Hỗ trợ đa dạng các ứng dụng:** Từ duyệt web, gửi email, chơi game đến truyền phát video, tầng Giao vận cung cấp các giao thức hỗ trợ cho nhiều loại hình ứng dụng trên Internet.


--------------------------------------------------------


#### **Tầng 2 - Internet Layer (Tầng Mạng)**

**Tầng Internet (Internet Layer) trong Mô hình TCP/IP**

Tầng Internet, còn được gọi là Network Layer trong một số tài liệu, là lớp thứ ba trong mô hình TCP/IP. Nó chịu trách nhiệm chính trong việc định tuyến gói tin qua các mạng khác nhau để đảm bảo chúng đến được đích cuối cùng. Lớp này giúp xác định lộ trình tốt nhất cho dữ liệu di chuyển qua mạng Internet phức tạp.

##### **Chức năng chính của Tầng Internet**


1. **Định tuyến (Routing)**
   - **Internet Layer** chịu trách nhiệm chọn đường đi thích hợp cho dữ liệu để có thể di chuyển từ máy tính này đến máy tính khác qua các mạng khác nhau. 
   - Các **router** (bộ định tuyến) sử dụng các bảng định tuyến để quyết định hướng đi của các gói tin dựa trên địa chỉ IP đích.
   - **Internet Protocol (IP)** là giao thức chính trong lớp này, giúp định tuyến các gói tin từ nguồn đến đích qua các mạng khác nhau, bất kể mạng vật lý của chúng.

2. **Địa chỉ IP (IP Addressing)**
   - **Internet Layer** sử dụng **địa chỉ IP** để xác định các thiết bị trên mạng. Địa chỉ IP là một địa chỉ duy nhất được cấp cho mỗi thiết bị kết nối với Internet hoặc mạng nội bộ.
     - **IPv4** sử dụng địa chỉ 32 bit (ví dụ: `192.168.1.1`).
     - **IPv6** sử dụng địa chỉ 128 bit (ví dụ: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`).
   - Địa chỉ IP được sử dụng để phân biệt các thiết bị và định tuyến các gói tin đến đúng nơi cần đến.

3. **Đóng gói và phân mảnh dữ liệu (Packetizing and Fragmentation)**
   - **Internet Layer** đóng gói dữ liệu nhận được từ lớp **Transport Layer** thành các **gói tin (packets)**, bao gồm thông tin về nguồn và đích (địa chỉ IP), cùng với dữ liệu thực tế.
   - Nếu kích thước của một gói tin quá lớn để truyền qua mạng, lớp Internet sẽ **phân mảnh** gói tin thành các phần nhỏ hơn và gửi từng phần qua mạng. Mỗi phần sẽ có thông tin phân mảnh để giúp máy đích ghép lại dữ liệu chính xác.
   
4. **Xử lý lỗi (Error Handling)**
   - Mặc dù **Internet Layer** không kiểm tra tính toàn vẹn dữ liệu như lớp **Transport Layer** (với các giao thức như TCP), nhưng IP vẫn sử dụng **checksum** để đảm bảo tính toàn vẹn của tiêu đề gói tin trong quá trình truyền tải.
   - Nếu phát hiện lỗi trong tiêu đề của gói tin (như lỗi trong địa chỉ IP hoặc các thông tin điều khiển khác), gói tin sẽ bị loại bỏ và yêu cầu gửi lại sẽ không được thực hiện.

5. **Chuyển tiếp gói tin (Packet Forwarding)**
   - **Router** tại **Internet Layer** sẽ chuyển tiếp các gói tin đến máy đích qua các mạng trung gian. Quy trình này dựa trên địa chỉ IP đích và bảng định tuyến, giúp các gói tin đi qua nhiều router và các mạng khác nhau cho đến khi chúng đến đích cuối cùng.
   - Quá trình chuyển tiếp gói tin này diễn ra nhanh chóng và hiệu quả, giúp dữ liệu được truyền tải qua mạng Internet.

6. **Quản lý các giao thức mạng (Protocol Handling)**
   - **Internet Layer** cũng hỗ trợ các giao thức mạng khác như **ICMP (Internet Control Message Protocol)** và **ARP (Address Resolution Protocol)**:
     - **ICMP** là giao thức kiểm tra trạng thái mạng và giúp gửi các thông báo lỗi, chẳng hạn như thông báo khi một máy không thể truy cập được (ping và các thông báo lỗi).
     - **ARP** là giao thức giúp ánh xạ địa chỉ IP thành địa chỉ MAC (địa chỉ phần cứng) trong một mạng LAN nội bộ.

7. **Hỗ trợ cho việc kết nối mạng giữa các mạng (Internetworking)**
   - **Internet Layer** cho phép kết nối các mạng với nhau, tạo thành một mạng rộng lớn như **Internet**. Điều này là nhờ vào việc sử dụng giao thức **IP**, cho phép các thiết bị trong các mạng khác nhau có thể giao tiếp với nhau.
   - Lớp này hoạt động như một cầu nối giữa các mạng LAN, MAN (Metropolitan Area Network) và WAN (Wide Area Network).


##### **Quy trình hoạt động**


1. **Nhận dữ liệu từ Transport Layer**
   - Khi **Transport Layer** (như TCP hoặc UDP) chuẩn bị dữ liệu để gửi, lớp này đóng gói dữ liệu thành các đơn vị gọi là **segments** (với TCP) hoặc **datagrams** (với UDP).
   - Dữ liệu này sau đó được chuyển đến lớp **Internet Layer** để tiếp tục xử lý và truyền tải qua mạng.

2. **Đóng gói dữ liệu thành gói tin (Packet)**
   - **Internet Layer** sẽ đóng gói dữ liệu từ lớp trên thành các **gói tin (packets)**, trong đó mỗi gói tin sẽ có:
     - **Tiêu đề (Header)**: Bao gồm các thông tin quan trọng như địa chỉ IP nguồn và đích, thông tin phân mảnh (nếu cần), và thông tin điều khiển.
     - **Dữ liệu (Payload)**: Là phần dữ liệu được truyền từ lớp trên (Transport Layer).
   - **Địa chỉ IP**: Mỗi gói tin sẽ được gắn địa chỉ IP của máy gửi và máy nhận để có thể định tuyến gói tin qua các mạng.

3. **Định tuyến gói tin (Routing)**
   - Sau khi gói tin được đóng gói với địa chỉ IP, lớp **Internet Layer** sẽ quyết định đường đi của gói tin thông qua quá trình **định tuyến**. Quá trình này bao gồm việc lựa chọn các router trung gian và các mạng phù hợp để gói tin có thể tới đích.
   - **Router** sẽ kiểm tra địa chỉ IP đích trong mỗi gói tin và sử dụng **bảng định tuyến** (routing table) để quyết định gói tin sẽ đi đâu tiếp theo.
     - Các router giữa các mạng sẽ chuyển tiếp gói tin cho đến khi nó đến mạng đích.

4. **Phân mảnh gói tin (Fragmentation)**
   - Nếu gói tin quá lớn để truyền qua một mạng cụ thể, lớp **Internet Layer** sẽ thực hiện **phân mảnh** gói tin thành các phần nhỏ hơn để chúng có thể được truyền qua các mạng có kích thước MTU (Maximum Transmission Unit) nhỏ hơn.
   - Mỗi mảnh sẽ có một **header riêng** chứa thông tin về gói tin gốc, giúp các mảnh này có thể được ghép lại đúng thứ tự khi đến đích.

5. **Chuyển tiếp gói tin (Packet Forwarding)**
   - Sau khi định tuyến, các **router** sẽ **chuyển tiếp** các gói tin qua các mạng trung gian cho đến khi gói tin đến được mạng đích.
   - Quá trình này được gọi là **chuyển tiếp (forwarding)**, và các router sử dụng địa chỉ IP đích để xác định đường đi tiếp theo của gói tin.

6. **Kiểm tra lỗi (Error Checking)**
   - **Checksum** là một phần của tiêu đề gói tin để kiểm tra tính toàn vẹn của dữ liệu trong quá trình truyền tải.
   - **Internet Layer** không có cơ chế sửa lỗi (như TCP có retransmission), nhưng nếu có lỗi trong tiêu đề gói tin (do nhiễu hoặc mất gói), gói tin sẽ bị loại bỏ và không được chuyển tiếp.

7. **Nhận và xử lý gói tin tại đích**
   - Khi gói tin đến được hệ thống đích (máy nhận), lớp **Internet Layer** trên máy đích sẽ kiểm tra tiêu đề gói tin để xác định xem nó có đích đến là máy của mình không.
   - Nếu đúng, gói tin sẽ được chuyển lên **Transport Layer** để xử lý (ví dụ, chuyển đến TCP hoặc UDP, tùy vào giao thức đã chọn).
   - Nếu địa chỉ IP đích không khớp, gói tin sẽ bị loại bỏ.

8. **Ghép các mảnh lại (Reassembly)**
   - Nếu gói tin đã bị phân mảnh trước khi truyền, khi đến máy đích, lớp **Internet Layer** sẽ thực hiện **ghép các mảnh lại** thành gói tin hoàn chỉnh.
   - Sau khi các mảnh được ghép lại, gói tin sẽ được chuyển lên lớp **Transport Layer** để tiếp tục xử lý.

9. **Truyền tải lên lớp Application Layer**
   - Sau khi gói tin đã được xử lý xong ở lớp **Internet Layer** (bao gồm ghép các mảnh, kiểm tra lỗi, và xác nhận đích), dữ liệu sẽ được chuyển đến lớp **Transport Layer** hoặc **Application Layer** tùy vào quá trình xử lý.
   - Lớp **Transport Layer** sẽ xác định liệu dữ liệu có cần phải được xác nhận (cho TCP) hay không và tiếp tục chuyển dữ liệu lên lớp **Application Layer** nơi ứng dụng thực sự sử dụng.



##### **Giao thức phổ biến của Tầng Internet**
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


------------------------------

#### **Tầng 1 - Link Layer (Tầng vật lý)**

**Tầng Liên kết (Link Layer) trong Mô hình TCP/IP**

Tầng Liên kết, còn được gọi là Link Layer hoặc Network Interface Layer trong mô hình TCP/IP, là lớp thấp nhất và đóng vai trò cơ bản trong việc truyền thông dữ liệu trực tiếp giữa các thiết bị trên một mạng cục bộ. Lớp này xử lý các chi tiết về phần cứng và truyền thông vật lý, từ việc đóng gói dữ liệu vào các khung (frames) cho đến việc xử lý truyền nhận tín hiệu.

#### **Chức năng chính của Tầng Liên kết**


1. **Đóng gói dữ liệu thành khung (Frame)**
   - **Link Layer** đóng gói dữ liệu từ **Internet Layer** (gói tin IP) thành các **khung (frame)**. Khung bao gồm một tiêu đề và phần dữ liệu (payload). 
   - Tiêu đề khung chứa thông tin cần thiết để định vị địa chỉ của các thiết bị trong mạng vật lý, như địa chỉ MAC của máy gửi và máy nhận.
   
2. **Địa chỉ hóa thiết bị (MAC Addressing)**
   - **Link Layer** sử dụng **địa chỉ MAC (Media Access Control)** để xác định và định vị các thiết bị trong mạng vật lý. Mỗi thiết bị trên mạng (như máy tính, router, switch) đều có một địa chỉ MAC duy nhất gắn liền với phần cứng của nó.
   - Địa chỉ MAC giúp các thiết bị trong một mạng LAN (Local Area Network) nhận diện và giao tiếp với nhau.

3. **Quản lý truy cập vào môi trường truyền tải (Media Access Control)**
   - **Link Layer** quản lý cách thức các thiết bị trên cùng một mạng có thể truy cập vào môi trường truyền tải vật lý (ví dụ, cáp đồng trục, cáp quang, sóng radio trong Wi-Fi).
   - Các giao thức như **Ethernet** và **Wi-Fi** quyết định cách thức chia sẻ môi trường truyền tải này giữa các thiết bị, nhằm tránh xung đột dữ liệu (collision).
     - Ví dụ: Giao thức **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) trong Ethernet giúp các thiết bị tránh việc truyền dữ liệu đồng thời trên cùng một kênh.

4. **Chuyển tiếp khung (Frame Forwarding)**
   - **Link Layer** chuyển tiếp các khung dữ liệu từ một thiết bị này đến thiết bị khác trong mạng nội bộ hoặc giữa các mạng vật lý. Khi một khung được nhận, nó sẽ được kiểm tra và chuyển tiếp nếu cần thiết đến đúng địa chỉ MAC đích.

5. **Kiểm tra lỗi và phát hiện lỗi (Error Detection)**
   - **Link Layer** sử dụng **checksum** hoặc **CRC (Cyclic Redundancy Check)** để kiểm tra tính toàn vẹn của dữ liệu trong khung. Nếu có lỗi trong quá trình truyền (do nhiễu, lỗi vật lý, v.v.), khung có thể bị loại bỏ hoặc yêu cầu gửi lại.
   - Các phương pháp này giúp đảm bảo rằng dữ liệu truyền qua các mạng vật lý không bị lỗi hoặc thay đổi.

6. **Chuyển mạch (Switching)**
   - **Link Layer** trong các thiết bị như **switches** có thể thực hiện chức năng chuyển mạch, giúp các gói dữ liệu được gửi từ thiết bị nguồn đến thiết bị đích trong cùng một mạng LAN.
   - Các switch sử dụng **địa chỉ MAC** để định tuyến các khung tới đúng cổng của thiết bị đích.

7. **Tạo giao tiếp trong mạng nội bộ (Local Area Network - LAN)**
   - **Link Layer** là lớp kết nối trực tiếp các thiết bị trong mạng LAN, cho phép các thiết bị như máy tính, máy in, hoặc các router giao tiếp với nhau thông qua các phương tiện vật lý (cáp mạng, sóng Wi-Fi, v.v.).


#### **Quy trình hoạt động**


1. **Nhận dữ liệu từ lớp Internet Layer**
   - **Link Layer** nhận dữ liệu từ **Internet Layer** (lớp trước đó trong mô hình TCP/IP). Dữ liệu này đến dưới dạng **gói tin (packet)** có chứa các thông tin như địa chỉ IP nguồn và đích.
   - Mỗi gói tin IP từ lớp Internet Layer sẽ được **Link Layer** đóng gói lại thành một **khung (frame)**. Khung này có thêm các thông tin cần thiết để truyền tải qua môi trường vật lý, chẳng hạn như địa chỉ MAC của thiết bị nguồn và đích.

2. **Đóng gói dữ liệu thành khung (Frame)**
   - **Link Layer** đóng gói dữ liệu từ lớp Internet Layer vào một khung (frame). Khung bao gồm hai phần chính:
     - **Tiêu đề khung (Frame Header)**: Chứa các thông tin cần thiết cho việc truyền tải trong mạng vật lý, bao gồm:
       - Địa chỉ **MAC nguồn**: Địa chỉ MAC của thiết bị gửi.
       - Địa chỉ **MAC đích**: Địa chỉ MAC của thiết bị nhận.
       - Các thông tin điều khiển, như loại khung (trong trường hợp Ethernet, loại này có thể là "EtherType").
     - **Dữ liệu (Payload)**: Là dữ liệu thực tế từ lớp trên (dữ liệu gói tin của lớp Internet Layer).
     - **Cuối khung (Frame Trailer)**: Chứa thông tin kiểm tra lỗi (thường là **CRC** hoặc **checksum**) để đảm bảo tính toàn vẹn của dữ liệu trong khung.

3. **Quản lý truy cập vào môi trường truyền tải (Media Access Control)**
   - **Link Layer** xác định cách thức thiết bị có thể truy cập vào môi trường truyền tải vật lý mà không gây xung đột (collision) khi nhiều thiết bị cùng truyền tải dữ liệu. Đây là bước quan trọng trong việc duy trì hiệu quả trong mạng.
   - **Giao thức MAC** (Media Access Control) quyết định cách thức truy cập vào mạng vật lý. Ví dụ:
     - **Ethernet** sử dụng **CSMA/CD** (Carrier Sense Multiple Access with Collision Detection) để kiểm tra xem kênh truyền có bận không trước khi truyền.
     - **Wi-Fi** sử dụng **CSMA/CA** (Collision Avoidance) để tránh xung đột trong môi trường không dây.
   
4. **Chuyển tiếp khung (Frame Forwarding)**
   - Sau khi khung được đóng gói, **Link Layer** sẽ gửi khung tới thiết bị đích qua các phương tiện vật lý, như cáp mạng, sóng Wi-Fi, v.v.
   - **Switches** hoặc các thiết bị tương tự sẽ chuyển tiếp các khung trong mạng LAN dựa trên địa chỉ **MAC đích**. Nếu thiết bị đích nằm trong cùng một mạng LAN, khung sẽ được chuyển trực tiếp đến thiết bị đó.
   
5. **Kiểm tra lỗi (Error Checking)**
   - **Link Layer** sử dụng các phương pháp kiểm tra lỗi để xác định xem dữ liệu trong khung có bị lỗi trong quá trình truyền không. Phương pháp phổ biến là **CRC** (Cyclic Redundancy Check), một kỹ thuật phát hiện lỗi mạnh mẽ.
   - Sau khi nhận khung, thiết bị đích sẽ kiểm tra giá trị CRC hoặc checksum trong phần trailer của khung. Nếu có lỗi, khung sẽ bị loại bỏ và yêu cầu truyền lại có thể được đưa ra (tùy thuộc vào giao thức).

6. **Chuyển tiếp qua các thiết bị chuyển mạch (Switching)**
   - Trong mạng LAN, các **switch** (bộ chuyển mạch) đóng vai trò quan trọng trong việc chuyển tiếp các khung giữa các thiết bị. Switch sử dụng **địa chỉ MAC** trong tiêu đề khung để xác định thiết bị đích và gửi khung đến cổng tương ứng.
   - **Switches** xây dựng một bảng ánh xạ các địa chỉ MAC tới các cổng tương ứng. Khi nhận khung, switch tra bảng để xác định cổng ra cho khung.

7. **Đến đích - Giải mã và gửi lên lớp trên**
   - Khi khung đến thiết bị đích, **Link Layer** trên thiết bị này sẽ kiểm tra xem địa chỉ **MAC đích** có khớp với địa chỉ MAC của nó không.
     - Nếu có, khung sẽ được **giải mã** và **chuyển lên lớp Internet Layer** để xử lý tiếp.
     - Nếu không khớp, khung sẽ bị loại bỏ, vì đây là khung không dành cho thiết bị đó.

8. **Phát hiện và xử lý phân mảnh (Fragmentation and Reassembly)**
   - **Link Layer** có thể thực hiện phân mảnh dữ liệu trong trường hợp môi trường vật lý yêu cầu kích thước gói tin nhỏ hơn (ví dụ, MTU - Maximum Transmission Unit).
   - **Link Layer** sẽ chia nhỏ các khung khi cần thiết (ở các giao thức như Ethernet hoặc PPP) và gửi chúng một cách độc lập. Sau đó, khi các mảnh đến đích, chúng sẽ được **ghép lại** thành một khung hoàn chỉnh.



#### **Giao thức phổ biến của Tầng Liên kết**
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

------------------------------------------------

### **Phân biệt ý nghĩa, mối tương quan OSI và TCP/IP



------------------------

### **UDP(User Datagram Protocol)**


UDP (User Datagram Protocol). Đây là giao thức không kết nối, nghĩa là nó không thiết lập một kết nối ổn định trước khi truyền dữ liệu, các gói datagram được gửi đi độc lập vì vậy có thể dẫn đến việc mất mát hoặc sai lệch thứ tự các gói. Do tính chất nhanh và hiệu quả của nó, UDP thường được sử dụng trong các ứng dụng đòi hỏi truyền dữ liệu thời gian thực như video, âm thanh trong cuộc gọi VoIP, trò chơi trực tuyến và nhiều hệ thống phát sóng trực tiếp. hoạt động ở tầng Giao vận (Transport Layer).

#### **Chức năng chính của UDP**


1. **Truyền tải dữ liệu nhanh chóng (Unreliable Transmission)**
   - UDP cung cấp cơ chế truyền tải dữ liệu nhanh mà không cần phải thiết lập kết nối trước giữa các hệ thống. Điều này làm giảm độ trễ và tiết kiệm tài nguyên, nhưng đồng thời cũng bỏ qua các kiểm tra độ tin cậy.
   - Giao thức này không thực hiện các cơ chế như xác nhận (ACK), kiểm tra lỗi, hay truyền lại dữ liệu bị mất, nên nó thích hợp cho các ứng dụng yêu cầu truyền tải dữ liệu với tốc độ cao mà không quá quan trọng về độ tin cậy.

2. **Không có kết nối (Connectionless)**
   - **UDP** là giao thức **không kết nối**. Điều này có nghĩa là không cần phải thiết lập kết nối giữa máy gửi và máy nhận trước khi truyền dữ liệu.
   - Mỗi gói dữ liệu (datagram) được gửi một cách độc lập mà không có bất kỳ thông tin nào về các gói trước hoặc sau đó. Điều này làm cho UDP nhẹ và nhanh chóng, nhưng cũng có thể dẫn đến việc mất mát hoặc sai lệch thứ tự của các gói.

3. **Truyền tải dữ liệu trong các đơn vị gọi là datagram**
   - Dữ liệu trong UDP được chia thành các đơn vị gọi là **datagram**, mỗi datagram chứa một **header** và **payload** (dữ liệu thực tế).
   - Địa chỉ của datagram bao gồm địa chỉ IP của nguồn và đích, cùng với thông tin khác để xác định loại giao thức và kiểm tra lỗi.

4. **Tính toán và kiểm tra lỗi (Checksum)**
   - Mặc dù UDP không cung cấp cơ chế sửa lỗi, nó vẫn sử dụng **checksum** để kiểm tra tính toàn vẹn của dữ liệu trong mỗi datagram.
   - **Checksum** giúp phát hiện các lỗi trong quá trình truyền tải dữ liệu (như lỗi bit do nhiễu). Tuy nhiên, UDP không có cơ chế tự động yêu cầu gửi lại dữ liệu nếu phát hiện lỗi (khác với TCP).

5. **Quản lý địa chỉ và cổng (Port Management)**
   - UDP sử dụng các **cổng** (ports) để phân biệt các ứng dụng khác nhau trên một thiết bị. Mỗi datagram UDP sẽ chứa thông tin về **cổng nguồn** và **cổng đích**.
   - Điều này cho phép nhiều ứng dụng hoặc dịch vụ chạy đồng thời trên một thiết bị mà không bị xung đột với nhau. Ví dụ: cổng 53 cho DNS, cổng 67 cho DHCP, v.v.

6. **Dữ liệu gửi một lần (Single Packet Delivery)**
   - UDP gửi mỗi gói tin (datagram) một lần duy nhất. Nếu gói tin bị mất trong quá trình truyền tải (do lỗi mạng hoặc sự cố), nó sẽ không được tự động gửi lại. Điều này có nghĩa là không có cơ chế đảm bảo rằng mỗi datagram sẽ đến đích, và các gói tin có thể đến theo thứ tự khác nhau hoặc không đến được.

7. **Tiết kiệm tài nguyên (Low Overhead)**
   - UDP có **đầu phí thấp** vì nó không yêu cầu tạo lập kết nối, xác nhận dữ liệu, hay chia nhỏ các gói khi có lỗi. Điều này giúp tiết kiệm tài nguyên hệ thống và làm giảm độ trễ.
   - Header của UDP rất nhỏ, chỉ 8 byte, giúp tiết kiệm băng thông khi truyền tải các gói nhỏ.

8. **Thích hợp cho các ứng dụng yêu cầu tốc độ và độ trễ thấp**
   - UDP thường được sử dụng trong các ứng dụng yêu cầu tốc độ truyền tải nhanh và độ trễ thấp, chẳng hạn như:
     - **Streaming** (video, audio) trực tiếp: Như trong truyền hình trực tuyến hoặc các cuộc gọi VoIP.
     - **Game trực tuyến**: Dữ liệu cần được truyền nhanh mà không cần quá nhiều xác nhận về độ tin cậy.
     - **DNS** (Domain Name System): Câu truy vấn DNS và phản hồi của nó thường sử dụng UDP vì tốc độ quan trọng hơn độ tin cậy trong trường hợp này.
     - **Truyền tải tệp nhỏ** trong các ứng dụng yêu cầu ít thao tác và độ trễ thấp.

9. **Không đảm bảo thứ tự (Out-of-Order Delivery)**
   - UDP không đảm bảo rằng các gói tin sẽ đến theo thứ tự mà chúng được gửi đi. Các datagram có thể đến đích không theo đúng thứ tự gửi (bởi vì mạng có thể thay đổi đường truyền).
   - Đây là lý do tại sao UDP không phù hợp với các ứng dụng cần đảm bảo thứ tự các gói tin, như truyền tệp hoặc các giao thức yêu cầu sự chính xác tuyệt đối.

10. **Tính mở rộng (Scalability)**
   - UDP cho phép mở rộng quy mô rất tốt vì nó có ít cơ chế quản lý kết nối và kiểm tra lỗi hơn, giúp giảm tải cho các máy chủ hoặc các thiết bị mạng.
   - Điều này làm UDP lý tưởng cho các ứng dụng cần phục vụ nhiều người dùng đồng thời, chẳng hạn như trong các dịch vụ trực tuyến hoặc giao thức truyền thông không có yêu cầu độ tin cậy cao.

#### **Giao thức UDP**
- **DNS (Domain Name System):**
   - Sử dụng UDP cho các truy vấn thông tin nhanh chóng về địa chỉ IP từ tên miền.
  
- **DHCP (Dynamic Host Configuration Protocol):**
   - Giao thức cấp phát địa chỉ IP động sử dụng UDP để trao đổi thông tin cấu hình mạng nhanh chóng.
  
- **SNMP (Simple Network Management Protocol):**
   - Dùng UDP để giám sát và quản lý thiết bị mạng với lưu lượng thấp và yêu cầu độ trễ thấp.

- **VoIP (Voice over Internet Protocol) và truyền phát video:**
   - Các ứng dụng cần truyền tải dữ liệu âm thanh và video thời gian thực thường sử dụng UDP để giảm độ trễ.

#### **Cấu trúc của Datagram UDP**
Một datagram UDP gồm các phần chính sau:

1. **Header (phần đầu)**:
   - **Source Port** (Cổng nguồn): Xác định cổng của ứng dụng gửi.
   - **Destination Port** (Cổng đích): Xác định cổng của ứng dụng nhận.
   - **Length**: Độ dài của toàn bộ datagram UDP (header + dữ liệu).
   - **Checksum**: Sử dụng để kiểm tra lỗi trong header và dữ liệu. Tuy nhiên, UDP không yêu cầu thiết bị nhận phải thực hiện kiểm tra lỗi hoặc yêu cầu tái gửi nếu phát hiện lỗi.

2. **Data (dữ liệu)**:
   - Chứa dữ liệu mà ứng dụng gửi đi. Dữ liệu này có thể có bất kỳ kích thước nào và không cần phải được chia thành các gói nhỏ (miễn là không vượt quá kích thước tối đa của giao thức liên kết dưới lớp mạng).

#### **Cơ chế hoạt động của UDP**
Khi một ứng dụng muốn gửi dữ liệu qua UDP, quy trình sẽ diễn ra như sau:

1. **Tạo datagram UDP**:
   - **Ứng dụng gửi dữ liệu** qua UDP bằng cách đóng gói dữ liệu của mình vào datagram UDP. Cổng nguồn và cổng đích được chỉ định trong header của UDP.
   
2. **Gửi dữ liệu đến lớp internet (Internet Layer)**:
   - UDP không kiểm tra hay phân chia dữ liệu thành các gói nhỏ hơn nếu dữ liệu quá lớn. Dữ liệu được truyền từ lớp vận chuyển (UDP) tới lớp internet (Internet Layer), nơi nó sẽ được đóng gói vào **gói IP**.
   - Tại lớp IP, gói dữ liệu sẽ được thêm các thông tin cần thiết (như địa chỉ IP nguồn và đích) và sẽ được gửi qua mạng.

3. **Gửi qua mạng**:
   - Gói dữ liệu sẽ được gửi qua mạng, có thể đi qua nhiều router và mạng con khác nhau. UDP không thực hiện bất kỳ kiểm tra nào để đảm bảo dữ liệu được nhận đúng thứ tự hoặc không bị mất mát.
   
4. **Máy nhận nhận gói UDP**:
   - Khi gói UDP đến máy nhận, lớp internet tại máy nhận sẽ kiểm tra địa chỉ IP và xác định máy đích. Sau đó, lớp vận chuyển (UDP) sẽ nhận gói UDP và chuyển tiếp dữ liệu tới ứng dụng nhận thông qua cổng đích.
   
5. **Xử lý của ứng dụng**:
   - Ứng dụng nhận sẽ đọc dữ liệu từ gói UDP và xử lý. Nếu có lỗi xảy ra trong quá trình truyền (như mất gói, dữ liệu bị hỏng), UDP không tự động yêu cầu gửi lại gói dữ liệu. Tuy nhiên, nếu ứng dụng cần độ tin cậy, nó có thể thực hiện việc kiểm tra lỗi và yêu cầu tái gửi lại dữ liệu.

#### **Ưu điểm và nhược điểm của UDP**

**Ưu điểm**:
- **Tốc độ cao**: UDP không có các cơ chế kiểm tra như TCP, vì vậy có thể truyền tải dữ liệu nhanh chóng với ít độ trễ.
- **Đơn giản**: UDP có cấu trúc header đơn giản hơn và ít overhead so với TCP.
- **Phù hợp cho ứng dụng yêu cầu độ trễ thấp**: UDP thường được sử dụng cho các ứng dụng **real-time** (thời gian thực) như **streaming video**, **voice over IP (VoIP)**, **gaming trực tuyến**, nơi mà việc mất mát một vài gói tin có thể chấp nhận được nhưng độ trễ phải thấp.

**Nhược điểm**:
- **Không tin cậy**: UDP không đảm bảo rằng dữ liệu sẽ đến đích hoặc đến đúng thứ tự. Các lỗi như mất mát gói tin hoặc trùng lặp có thể xảy ra.
- **Không kiểm tra lỗi toàn diện**: Mặc dù có checksum để kiểm tra lỗi cơ bản, UDP không thực hiện bất kỳ việc khôi phục hay yêu cầu tái gửi lại dữ liệu nếu phát hiện lỗi.
- **Không phân mảnh tự động**: Nếu dữ liệu vượt quá kích thước tối đa của gói UDP, nó sẽ bị mất.


**Ví dụ thực tế**

Một ví dụ điển hình về UDP trong ứng dụng thực tế là **streaming video**. Khi xem video trực tuyến, dữ liệu video được chia thành các gói nhỏ và gửi đi qua mạng bằng UDP. Nếu một vài gói tin bị mất trong quá trình truyền, video vẫn có thể tiếp tục phát mà không bị ảnh hưởng quá nhiều. Tuy nhiên, việc có độ trễ thấp và truyền tải nhanh vẫn là yếu tố quan trọng hơn trong trường hợp này.


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
**TCP (Transmission Control Protocol)** là một giao thức truyền tải dữ liệu có kết nối (tức là phải thiết lập 1 kết nối trước khi truyền và duy trì trong suốt quá trình truyền để đảm bảo dữ liệu không bị mất), hoạt động tại tầng vận chuyển (Transport Layer) trong mô hình OSI. TCP đảm bảo rằng các gói dữ liệu được truyền một cách đáng tin cậy và theo thứ tự, bảo vệ tính toàn vẹn của dữ liệu. Khi một kết nối TCP được thiết lập, nó sẽ duy trì sự ổn định và bảo mật trong suốt quá trình truyền tải, sử dụng các cơ chế kiểm tra lỗi và xác nhận dữ liệu.

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

