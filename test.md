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

--------------
-------------

### Định tuyến tĩnh (Static Routing)

**Định tuyến tĩnh** là một phương pháp định tuyến trong đó các tuyến đường được cấu hình thủ công và không thay đổi trừ khi người quản trị mạng thay đổi chúng. Các router sử dụng bảng định tuyến tĩnh để chuyển tiếp gói tin từ nguồn đến đích dựa trên các tuyến đường mà quản trị viên đã chỉ định.

### 1. **Đặc điểm của Định tuyến Tĩnh**

- **Cấu hình thủ công**: Tất cả các tuyến đường phải được cấu hình thủ công, tức là người quản trị phải xác định các tuyến đường từ mỗi router tới các mạng khác trong hệ thống.
- **Không thay đổi tự động**: Bảng định tuyến tĩnh không tự động thay đổi khi có sự thay đổi trong mạng, ví dụ như khi một liên kết bị hỏng hoặc khi có sự thay đổi trong cấu trúc mạng.
- **Tính ổn định**: Định tuyến tĩnh cung cấp sự ổn định cao vì không có sự thay đổi tự động, phù hợp với các mạng không có sự thay đổi thường xuyên.

### 2. **Ưu điểm của Định tuyến Tĩnh**
- **Đơn giản và dễ quản lý**: Trong các mạng nhỏ và không thay đổi, việc cấu hình định tuyến tĩnh rất dễ dàng và dễ kiểm soát.
- **Tiết kiệm tài nguyên**: Không cần nhiều tài nguyên hệ thống vì không có quá trình tính toán phức tạp như trong định tuyến động.
- **Hiệu suất cao**: Định tuyến tĩnh giúp tiết kiệm băng thông và giảm tải cho router vì không cần trao đổi thông tin định tuyến giữa các router.
- **Bảo mật**: Vì không có giao thức định tuyến động để truyền tải thông tin định tuyến, định tuyến tĩnh có thể an toàn hơn trong các môi trường mạng nhỏ và có mức độ bảo mật cao.

### 3. **Nhược điểm của Định tuyến Tĩnh**
- **Không linh hoạt**: Khi có sự thay đổi trong mạng (như một liên kết bị hỏng), quản trị viên phải cập nhật lại cấu hình thủ công. Điều này có thể làm mạng không khả dụng tạm thời cho đến khi thay đổi được thực hiện.
- **Khó mở rộng**: Trong các mạng lớn, việc cấu hình và duy trì định tuyến tĩnh trở nên khó khăn và mất thời gian, vì mỗi router cần được cấu hình riêng biệt.
- **Không hỗ trợ tính năng phục hồi tự động**: Nếu một liên kết bị hỏng, các router không thể tự động tìm ra tuyến đường thay thế, yêu cầu người quản trị can thiệp.

### 4. **Cách Cấu Hình Định Tuyến Tĩnh**

Để cấu hình định tuyến tĩnh, bạn cần chỉ định **địa chỉ mạng đích** và **cổng tiếp theo (next-hop gateway)** cho router biết cách tiếp cận mạng đích. Dưới đây là cú pháp cơ bản để cấu hình định tuyến tĩnh trên một số router phổ biến:

#### Ví dụ trên router Cisco (CLI):
```
ip route <mạng đích> <subnet mask> <next-hop IP hoặc cổng giao diện>
```
Ví dụ:
```
ip route 192.168.2.0 255.255.255.0 192.168.1.1
```
Điều này có nghĩa là router này sẽ chuyển tiếp các gói tin đến mạng `192.168.2.0/24` thông qua cổng giao diện `192.168.1.1`.

#### Ví dụ trên hệ điều hành Linux:
Trên hệ điều hành Linux, bạn có thể cấu hình định tuyến tĩnh bằng lệnh `route` hoặc `ip route`. Ví dụ:
```
sudo ip route add 192.168.2.0/24 via 192.168.1.1
```
Lệnh trên sẽ thêm một tuyến đường tĩnh cho mạng `192.168.2.0/24` qua cổng tiếp theo `192.168.1.1`.

### 5. **Ứng dụng của Định tuyến Tĩnh**
- **Mạng nhỏ hoặc đơn giản**: Định tuyến tĩnh thường được sử dụng trong các mạng nhỏ, nơi cấu trúc mạng không thay đổi nhiều và không cần tính linh hoạt.
- **Mạng với các liên kết cố định**: Trong các môi trường có các kết nối mạng cố định, không có thay đổi lớn trong cấu trúc mạng, định tuyến tĩnh sẽ giúp giảm tải cho các router.
- **An ninh và kiểm soát**: Định tuyến tĩnh có thể được sử dụng trong các mạng yêu cầu kiểm soát chặt chẽ hơn về cách thức các gói tin đi qua mạng, ví dụ như trong các tổ chức yêu cầu tính bảo mật cao.

### 6. **Ví dụ thực tế về Định tuyến Tĩnh**
Giả sử bạn có một mạng với các router A và B, trong đó router A có một liên kết đến mạng `192.168.2.0/24` qua cổng `192.168.1.1`. Bạn muốn cấu hình định tuyến tĩnh trên router B để có thể truy cập mạng này thông qua router A. Cấu hình trên router B sẽ như sau:
```
ip route 192.168.2.0 255.255.255.0 192.168.1.1
```
Khi đó, bất kỳ gói tin nào cần đến mạng `192.168.2.0` từ router B sẽ được gửi đến router A, nơi mà router A sẽ chuyển tiếp chúng đến đích.

### 7. **Khi nào nên sử dụng Định tuyến Tĩnh?**
- **Mạng nhỏ**: Nếu bạn quản lý một mạng nhỏ với ít router và không có nhiều thay đổi, định tuyến tĩnh là một lựa chọn phù hợp.
- **Mạng ổn định**: Khi các kết nối trong mạng không thay đổi thường xuyên và không có sự thay đổi lớn trong cấu trúc mạng.
- **Yêu cầu bảo mật cao**: Định tuyến tĩnh giúp ngăn ngừa việc chia sẻ thông tin định tuyến qua các giao thức động, làm cho mạng an toàn hơn.
- **Mạng với yêu cầu kiểm soát nghiêm ngặt**: Định tuyến tĩnh cho phép người quản trị kiểm soát chính xác các tuyến đường và cách thức các gói tin được chuyển tiếp.

### 8. **Kết luận**
Định tuyến tĩnh là một phương pháp định tuyến đơn giản và hiệu quả cho các mạng nhỏ hoặc ổn định. Mặc dù có nhược điểm về tính linh hoạt và khả năng phục hồi, nhưng trong các trường hợp mạng không thay đổi nhiều, định tuyến tĩnh vẫn là một lựa chọn tuyệt vời. Việc cấu hình tĩnh giúp giảm tải cho các giao thức định tuyến động và tạo ra một mạng đơn giản, dễ kiểm soát.

### **Chi Tiết về Routing Table (Bảng Định Tuyến)**

**Bảng định tuyến (Routing Table)** là một phần quan trọng trong hoạt động của router hoặc các thiết bị mạng, cung cấp thông tin về cách router sẽ chuyển tiếp gói tin đến các đích mạng khác nhau. Mỗi router trong mạng đều có một bảng định tuyến riêng, chứa thông tin về các tuyến đường (routes) tới các mạng đích.

### **Cấu Trúc của Routing Table**

Bảng định tuyến bao gồm một hoặc nhiều mục (entries) chứa thông tin về các tuyến đường mà router sử dụng để quyết định cách chuyển tiếp gói tin. Mỗi mục thường có các thành phần chính sau:

1. **Network Destination (Địa chỉ mạng đích)**:
   - Đây là địa chỉ mạng mà router đang tìm cách chuyển tiếp gói tin tới.
   - Mạng đích được biểu diễn dưới dạng **địa chỉ IP** (ví dụ: `192.168.1.0/24`), trong đó `/24` là mặt nạ subnet, xác định phạm vi của mạng con.

2. **Subnet Mask (Mặt nạ mạng)**:
   - Mặt nạ mạng giúp router phân biệt đâu là **địa chỉ mạng** và đâu là **địa chỉ host** trong một gói tin.
   - Ví dụ, đối với `192.168.1.0/24`, mặt nạ mạng là `255.255.255.0`.

3. **Next-Hop (Cổng tiếp theo)**:
   - Địa chỉ IP của router hoặc thiết bị tiếp theo trong chuỗi chuyển tiếp.
   - Đây là nơi gói tin được chuyển đến sau khi rời khỏi router hiện tại. Nếu không có next-hop (trường hợp mạng đích được kết nối trực tiếp), thông tin này có thể là `0.0.0.0`.

4. **Interface (Giao diện)**:
   - Giao diện mạng mà gói tin sẽ được gửi qua. Giao diện này có thể là một cổng vật lý như `eth0`, `eth1` hoặc `wan0`.
   - Router sử dụng thông tin này để biết cổng nào sẽ truyền gói tin đi.

5. **Metric (Chi phí)**:
   - Đây là một giá trị chỉ ra "chi phí" của một tuyến đường. Nó có thể phụ thuộc vào nhiều yếu tố như độ dài tuyến đường (số lượng hop), băng thông, độ trễ, v.v.
   - Giao thức định tuyến sử dụng metric để chọn tuyến đường tối ưu (ví dụ: tuyến đường có metric thấp nhất).

6. **Route Source (Nguồn tuyến đường)**:
   - Cho biết tuyến đường đến từ đâu. Nó có thể là một **tuyến đường tĩnh**, **tuyến đường động** (được học từ các giao thức định tuyến như RIP, OSPF, BGP), hoặc **tuyến đường kết nối trực tiếp** (directly connected).

7. **TTL (Time To Live)**:
   - Trường này giúp kiểm soát vòng đời của gói tin trong mạng. Mỗi khi gói tin đi qua một router, TTL sẽ giảm đi một đơn vị. Khi TTL đạt 0, gói tin sẽ bị loại bỏ để tránh vòng lặp vô hạn.

### **Ví Dụ về Routing Table**

Dưới đây là ví dụ về một bảng định tuyến trên một router trong mạng:

| Network Destination | Subnet Mask       | Next Hop        | Interface  | Metric | Route Source  |
|---------------------|-------------------|-----------------|------------|--------|---------------|
| 0.0.0.0             | 0.0.0.0           | 192.168.1.1     | eth0       | 1      | Static        |
| 192.168.1.0         | 255.255.255.0     | 0.0.0.0         | eth0       | 0      | Connected     |
| 192.168.2.0         | 255.255.255.0     | 192.168.1.2     | eth1       | 1      | Static        |
| 192.168.3.0         | 255.255.255.0     | 192.168.1.3     | eth1       | 2      | Static        |

### **Giải Thích Cột trong Routing Table**

1. **Network Destination**:
   - Địa chỉ mạng đích mà router cần gửi gói tin tới. 
   - Ví dụ: `192.168.1.0/24` có nghĩa là mạng con có địa chỉ `192.168.1.x`.

2. **Subnet Mask**:
   - Mặt nạ mạng xác định phạm vi của mạng đích. 
   - Ví dụ: `255.255.255.0` có nghĩa là mạng con với 24 bit cho phần mạng và 8 bit cho phần host (có thể có tối đa 254 địa chỉ IP).

3. **Next Hop**:
   - Địa chỉ IP của router hoặc gateway tiếp theo mà router này sẽ chuyển gói tin tới.
   - Ví dụ: `192.168.1.2` là địa chỉ của router tiếp theo mà gói tin phải đi qua để đến mạng `192.168.2.0`.

4. **Interface**:
   - Giao diện mạng mà gói tin sẽ được chuyển tiếp qua. 
   - Ví dụ: `eth0` là giao diện mạng của router kết nối với mạng `192.168.1.x`.

5. **Metric**:
   - Chỉ ra chi phí của tuyến đường, có thể là giá trị tùy chỉnh hoặc được tính toán tự động.
   - Tuyến đường có metric thấp hơn thường được ưu tiên sử dụng.

6. **Route Source**:
   - Cho biết nguồn của tuyến đường. Ví dụ:
     - `Static`: Tuyến đường được cấu hình thủ công bởi người quản trị.
     - `Connected`: Tuyến đường mà router tự động nhận ra vì mạng được kết nối trực tiếp với giao diện của router.
     - `Dynamic`: Tuyến đường được học từ các giao thức định tuyến động như RIP, OSPF, BGP.

### **Các Loại Tuyến Đường trong Routing Table**

1. **Tuyến đường trực tiếp (Directly Connected Routes)**:
   - Các mạng mà router kết nối trực tiếp qua các giao diện mạng của nó.
   - Những mạng này tự động được thêm vào bảng định tuyến khi router được cấu hình với địa chỉ IP trên giao diện.
   - Ví dụ: `192.168.1.0/24` nếu router có giao diện `eth0` với địa chỉ IP `192.168.1.1`.

2. **Tuyến đường tĩnh (Static Routes)**:
   - Tuyến đường được cấu hình thủ công bởi người quản trị mạng, ví dụ qua các lệnh như `ip route`.
   - Ví dụ: `ip route 192.168.2.0 255.255.255.0 192.168.1.2` chỉ ra rằng các gói tin đến `192.168.2.0` sẽ được chuyển tiếp qua router có địa chỉ IP `192.168.1.2`.

3. **Tuyến đường động (Dynamic Routes)**:
   - Tuyến đường mà router học được thông qua các giao thức định tuyến động như **RIP**, **OSPF**, hoặc **BGP**. Các tuyến đường này có thể thay đổi theo thời gian nếu có sự thay đổi trong mạng.
   - Tuyến đường động có thể được xác định bởi các giao thức định tuyến dựa trên các thuật toán tối ưu như **distance-vector** hoặc **link-state**.

4. **Tuyến đường mặc định (Default Route)**:
   - Là tuyến đường được sử dụng khi không có tuyến đường cụ thể nào khớp với mạng đích của gói tin.
   - Tuyến đường mặc định thường được cấu hình với địa chỉ `0.0.0.0/0` và gửi tất cả các gói tin không xác định đến một router hoặc gateway bên ngoài.
   - Ví dụ: `ip route 0.0.0.0 0.0.0.0 192.168.1.1` có nghĩa là tất cả các gói tin không khớp với các tuyến đường khác sẽ được gửi đến router có địa chỉ `192.168.1.1`.

### **Kiểm Tra Routing Table trong Router**

Trong môi trường Cisco, bạn có thể kiểm tra bảng định tuyến của router bằng lệnh:

```
show ip route
```

Kết quả trả về có thể giống như sau:

```
Router# show ip route
C    192.168.1.0/24 is directly connected, Ethernet0
S    192.168.2.0/24 [1/0] via 192.168.1.2, Ethernet1
C    192.168.3.0/24 is directly connected, Ethernet1
S    0.0.0.0/0 [1/0] via 192.168.1.1, Ethernet0
```

- `C` (Connected): Mạng được kết nối trực tiếp với router.
- `S` (Static): Mạng được cấu hình thông qua định tuyến tĩnh.
- `[1/0]`: Metric của tuyến đường, với số đầu tiên là chi phí và số thứ hai là tuổi thọ của tuyến đường.
- Tuyến đường mặc định (`0.0.0.0/0`) trỏ đến `192.168.1.1`.

###

 **Tóm Tắt**
Bảng định tuyến (Routing Table) là một bảng chứa thông tin về các tuyến đường mà router sử dụng để chuyển tiếp gói tin đến các mạng đích. Nó bao gồm các tuyến đường trực tiếp, tĩnh, động và mặc định. Việc quản lý bảng định tuyến là rất quan trọng trong việc đảm bảo hiệu quả và độ tin cậy của việc chuyển tiếp dữ liệu trong mạng.
