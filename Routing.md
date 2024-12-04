### **1. Giao thức định tuyến (Routing Protocol)**

**Giao thức định tuyến** (Routing Protocol) là một tập hợp các quy tắc, quy trình và phương pháp mà các router hoặc thiết bị mạng sử dụng để quyết định con đường tối ưu (tuyến đường) để chuyển tiếp các gói tin từ nguồn 
đến đích trong mạng máy tính. Các giao thức này cho phép các router trao đổi thông tin về các tuyến đường khả dụng, từ đó cập nhật và duy trì bảng định tuyến của mình để đảm bảo dữ liệu được gửi đến đúng đích qua con đường tối ưu.

**Lý do cần giao thức định tuyến:**
- **Tối ưu hóa lưu lượng mạng**: Giao thức định tuyến giúp các router chọn lựa con đường tối ưu cho việc chuyển tiếp gói tin, từ đó giảm độ trễ và tăng hiệu suất mạng.
- **Khả năng phục hồi và chịu lỗi**: Khi một liên kết mạng bị hỏng, giao thức định tuyến có thể giúp tìm ra con đường thay thế để đảm bảo sự tiếp tục của việc truyền tải dữ liệu.
- **Quản lý mạng động**: Mạng máy tính không phải lúc nào cũng có cấu trúc cố định. Giao thức định tuyến giúp mạng thích nghi với sự thay đổi của cấu trúc mạng, thêm hoặc bớt các router, liên kết mới mà không cần cấu hình thủ công.
- **Khả năng mở rộng**: Khi mạng phát triển lớn hơn, các giao thức định tuyến giúp quản lý các tuyến đường và duy trì hiệu suất mạng mà không cần điều chỉnh thủ công.

**1.1 Định tuyến tĩnh (Static Routing)**

- phương pháp định tuyến trong đó các tuyến đường được cấu hình thủ công và không thay đổi trừ khi người quản trị mạng thay đổi chúng. Các router sử dụng bảng định tuyến tĩnh để chuyển tiếp gói tin từ nguồn đến đích dựa trên các tuyến đường mà quản trị viên đã chỉ định.

**Đặc điểm của Định tuyến Tĩnh**

- **Cấu hình thủ công**: Tất cả các tuyến đường phải được cấu hình thủ công, tức là người quản trị phải xác định các tuyến đường từ mỗi router tới các mạng khác trong hệ thống.
- **Không thay đổi tự động**: Bảng định tuyến tĩnh không tự động thay đổi khi có sự thay đổi trong mạng, ví dụ như khi một liên kết bị hỏng hoặc khi có sự thay đổi trong cấu trúc mạng.
- **Tính ổn định**: Định tuyến tĩnh cung cấp sự ổn định cao vì không có sự thay đổi tự động, phù hợp với các mạng không có sự thay đổi thường xuyên.

**Ưu điểm của Định tuyến Tĩnh**
- **Đơn giản và dễ quản lý**: Trong các mạng nhỏ và không thay đổi, việc cấu hình định tuyến tĩnh rất dễ dàng và dễ kiểm soát.
- **Tiết kiệm tài nguyên**: Không cần nhiều tài nguyên hệ thống vì không có quá trình tính toán phức tạp như trong định tuyến động.
- **Hiệu suất cao**: Định tuyến tĩnh giúp tiết kiệm băng thông và giảm tải cho router vì không cần trao đổi thông tin định tuyến giữa các router.
- **Bảo mật**: Vì không có giao thức định tuyến động để truyền tải thông tin định tuyến, định tuyến tĩnh có thể an toàn hơn trong các môi trường mạng nhỏ và có mức độ bảo mật cao.

**Nhược điểm của Định tuyến Tĩnh**
- **Không linh hoạt**: Khi có sự thay đổi trong mạng (như một liên kết bị hỏng), quản trị viên phải cập nhật lại cấu hình thủ công. Điều này có thể làm mạng không khả dụng tạm thời cho đến khi thay đổi được thực hiện.
- **Khó mở rộng**: Trong các mạng lớn, việc cấu hình và duy trì định tuyến tĩnh trở nên khó khăn và mất thời gian, vì mỗi router cần được cấu hình riêng biệt.
- **Không hỗ trợ tính năng phục hồi tự động**: Nếu một liên kết bị hỏng, các router không thể tự động tìm ra tuyến đường thay thế, yêu cầu người quản trị can thiệp.

**Ứng dụng của Định tuyến Tĩnh**
- **Mạng nhỏ hoặc đơn giản**: Định tuyến tĩnh thường được sử dụng trong các mạng nhỏ, nơi cấu trúc mạng không thay đổi nhiều và không cần tính linh hoạt.
- **Mạng với các liên kết cố định**: Trong các môi trường có các kết nối mạng cố định, không có thay đổi lớn trong cấu trúc mạng, định tuyến tĩnh sẽ giúp giảm tải cho các router.
- **An ninh và kiểm soát**: Định tuyến tĩnh có thể được sử dụng trong các mạng yêu cầu kiểm soát chặt chẽ hơn về cách thức các gói tin đi qua mạng, ví dụ như trong các tổ chức yêu cầu tính bảo mật cao.

**Khi nào nên sử dụng Định tuyến Tĩnh?**
- **Mạng nhỏ**: Nếu bạn quản lý một mạng nhỏ với ít router và không có nhiều thay đổi, định tuyến tĩnh là một lựa chọn phù hợp.
- **Mạng ổn định**: Khi các kết nối trong mạng không thay đổi thường xuyên và không có sự thay đổi lớn trong cấu trúc mạng.
- **Yêu cầu bảo mật cao**: Định tuyến tĩnh giúp ngăn ngừa việc chia sẻ thông tin định tuyến qua các giao thức động, làm cho mạng an toàn hơn.
- **Mạng với yêu cầu kiểm soát nghiêm ngặt**: Định tuyến tĩnh cho phép người quản trị kiểm soát chính xác các tuyến đường và cách thức các gói tin được chuyển tiếp.

- Định tuyến tĩnh bảo mật cao vì không trao đổi thông tin (địa chỉ mạng, gateway, đoạn đường...) giữa các router. Mỗi router chỉ biết tuyến đường mà nó đã được cấu hình cụ thể. 

**1.2 Định tuyến động (Dynamic Routing)**
Định tuyến động là phương pháp mà các router sử dụng giao thức định tuyến để tự động trao đổi thông tin và xác định các tuyến đường tối ưu. Các giao thức định tuyến động chia sẻ thông tin giữa các router, giúp tự động cập nhật bảng định tuyến.

### ** Routing Table**

- cung cấp thông tin về cách router sẽ chuyển tiếp gói tin đến các đích mạng khác nhau. Mỗi router trong mạng đều có một bảng định tuyến riêng, chứa thông tin về các tuyến đường (routes) tới các mạng đích. Ngoài ra còn chứa các thông tin liên quan đến cách router xử lý và chuyển tiếp gói tin. 

**Cấu Trúc của Routing Table**

Bảng định tuyến bao gồm một hoặc nhiều mục (entries) chứa thông tin về các tuyến đường mà router sử dụng để quyết định cách chuyển tiếp gói tin. Mỗi mục thường có các thành phần chính sau:

1. **Network Destination (Địa chỉ mạng đích)**:
   - Đây là địa chỉ mạng mà router đang tìm cách chuyển tiếp gói tin tới.
   - Mạng đích được biểu diễn dưới dạng **địa chỉ IP** (ví dụ: `192.168.1.0/24`), trong đó `/24` là subnet mask, xác định phạm vi của mạng con.

2. **Subnet Mask (Mặt nạ mạng)**:
   - Subnet Mask giúp router phân biệt đâu là **địa chỉ mạng** và đâu là **địa chỉ host** trong một gói tin.
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

**Các Loại Tuyến Đường trong Routing Table**

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
  
### **Cách cấu hình Routing Table**

- Gateway phải thuộc cùng một subnet với giao diện mạng sử dụng để định tuyến.
- 

Cấu hình tạm thời reboot hoăc tắt máy là mất

**Bước 1: Thêm Tuyến Đường Tĩnh**

Cú pháp:
```bash
sudo ip route add 192.168.1.0/24 via 192.168.1.1 dev ens33
```

- `192.168.1.0/24`: Mạng đích bạn muốn định tuyến.
- `192.168.1.1`: Gateway (địa chỉ IP của router hoặc next-hop).
- `ens33`: Tên giao diện mạng.

**Bước 2: Kiểm Tra Bảng Định Tuyến**
Sau khi thêm tuyến đường tĩnh, kiểm tra bảng định tuyến của máy ảo bằng lệnh:
```bash
ip route show
```
