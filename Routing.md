### **Routing**

- Routing (Định tuyến) là quá trình định hướng cho các gói dữ liệu từ router này sang router khác.
- Router (Bộ định tuyến) là thiết bị chuyển tiếp các gói dữ liệu giữa các mạng.

**Quá trình Routing (Định tuyến)** là quá trình xác định đường đi của các gói dữ liệu từ nguồn đến đích trong mạng, thông qua các router và các thiết bị mạng trung gian khác. Quá trình này đảm bảo rằng các gói dữ liệu sẽ được chuyển qua các mạng khác nhau một cách hiệu quả và chính xác. 

**Các Bước trong Quá Trình Routing**

Quá trình định tuyến có thể được mô tả qua các bước chính sau:

**1. Gửi Gói Dữ Liệu**
- Một thiết bị (ví dụ: máy tính, điện thoại) tạo và gửi một gói dữ liệu đến đích qua mạng.
- Gói dữ liệu này chứa thông tin quan trọng như:
  - **Địa chỉ IP nguồn (Source IP)**: Địa chỉ IP của thiết bị gửi.
  - **Địa chỉ IP đích (Destination IP)**: Địa chỉ IP của thiết bị nhận.

**2. Kiểm Tra Địa Chỉ Đích**
- Khi một router nhận được gói dữ liệu, nó sẽ kiểm tra địa chỉ IP đích trong header của gói.
- Router không cần biết nội dung của gói, chỉ cần biết địa chỉ đích để quyết định gửi gói dữ liệu đi đâu.

**3. Tra Cứu Bảng Định Tuyến**
- Mỗi router có một bảng định tuyến (routing table) để quyết định đường đi của gói dữ liệu.
- Bảng định tuyến chứa các thông tin sau:
  - **Mạng đích (Destination network)**: Mạng mà gói dữ liệu sẽ đến.
  - **Gateway (Cổng tiếp theo)**: Địa chỉ IP của router tiếp theo để chuyển tiếp gói dữ liệu.
  - **Interface (Giao diện mạng)**: Cổng hoặc giao diện mà router sử dụng để gửi gói đến mạng đích.
  - **Metric (Chỉ số ưu tiên)**: Một chỉ số để xác định độ ưu tiên của một đường dẫn. Đường dẫn có metric thấp hơn sẽ được ưu tiên hơn.

Router sử dụng địa chỉ IP đích để tra cứu trong bảng định tuyến và tìm ra cổng tiếp theo để chuyển tiếp gói.

**4. Chuyển Tiếp Gói Dữ Liệu**
- Sau khi tìm được thông tin về cổng tiếp theo (gateway), router sẽ chuyển tiếp gói dữ liệu qua cổng này.
- Gói dữ liệu có thể đi qua nhiều router khác nhau trên đường đi từ nguồn đến đích.

**5. Đến Mạng Đích**
- Quá trình trên sẽ tiếp tục cho đến khi gói dữ liệu đến được mạng đích.
- Nếu router cuối cùng trong chuỗi kết nối tới mạng đích, gói dữ liệu sẽ được gửi trực tiếp đến thiết bị đích (máy tính, server...).

**6. Phản Hồi (Nếu Có)**
- Nếu ứng dụng ở thiết bị đích yêu cầu phản hồi (ví dụ: trong trường hợp gửi một yêu cầu HTTP), một gói dữ liệu phản hồi sẽ được tạo và quá trình routing sẽ lặp lại cho gói phản hồi.

**Ví Dụ Về Quá Trình Routing**

Giả sử bạn có một mạng với ba router:

- **Router A** kết nối với **Router B**, và **Router B** kết nối với **Router C**.
- Thiết bị nguồn (máy tính) có địa chỉ IP là `192.168.1.2` và muốn gửi gói dữ liệu đến một server có địa chỉ IP là `10.10.10.10`.

Quá trình sẽ như sau:

1. **Máy tính (Nguồn)**: Gói dữ liệu được tạo với địa chỉ đích là `10.10.10.10`.
2. **Router A**:
   - Router A sẽ kiểm tra bảng định tuyến và phát hiện rằng gói dữ liệu cần được chuyển tiếp qua **Router B** (thông qua cổng mạng của nó).
3. **Router B**:
   - Router B kiểm tra bảng định tuyến của mình và gửi gói dữ liệu đến **Router C**.
4. **Router C**:
   - Router C kiểm tra bảng định tuyến và gửi gói dữ liệu đến thiết bị đích có địa chỉ IP `10.10.10.10`.


**Các Loại Định Tuyến (Routing Types)**
1. **Direct Routing**: Khi gói dữ liệu đi trực tiếp từ một thiết bị đến thiết bị đích mà không cần qua các router trung gian.
2. **Indirect Routing**: Gói dữ liệu phải đi qua một hoặc nhiều router trung gian để đến đích.

-------------

### **1. Giao thức định tuyến (Routing Protocol)**

**Giao thức định tuyến** (Routing Protocol) là một tập hợp các quy tắc, quy trình và phương pháp mà các router hoặc thiết bị mạng sử dụng để quyết định con đường tối ưu (tuyến đường) để chuyển tiếp các gói tin từ nguồn 
đến đích trong mạng máy tính. Các giao thức này cho phép các router trao đổi thông tin về các tuyến đường khả dụng, từ đó cập nhật và duy trì bảng định tuyến của mình để đảm bảo dữ liệu được gửi đến đúng đích qua con đường tối ưu.

**Lý do cần giao thức định tuyến:**
- **Tối ưu hóa lưu lượng mạng**: Giao thức định tuyến giúp các router chọn lựa con đường tối ưu cho việc chuyển tiếp gói tin, từ đó giảm độ trễ và tăng hiệu suất mạng.
- **Khả năng phục hồi và chịu lỗi**: Khi một liên kết mạng bị hỏng, giao thức định tuyến có thể giúp tìm ra con đường thay thế để đảm bảo sự tiếp tục của việc truyền tải dữ liệu.
- **Quản lý mạng động**: Mạng máy tính không phải lúc nào cũng có cấu trúc cố định. Giao thức định tuyến giúp mạng thích nghi với sự thay đổi của cấu trúc mạng, thêm hoặc bớt các router, liên kết mới mà không cần cấu hình thủ công.
- **Khả năng mở rộng**: Khi mạng phát triển lớn hơn, các giao thức định tuyến giúp quản lý các tuyến đường và duy trì hiệu suất mạng mà không cần điều chỉnh thủ công.

**1.1 Định tuyến tĩnh (Static Routing)**

**Giao thức định tuyến tĩnh (Static Routing)**

**Giao thức định tuyến tĩnh** là phương pháp định tuyến trong đó các tuyến đường được cấu hình thủ công vào bảng định tuyến của router hoặc thiết bị mạng khác. Tuyến đường này không thay đổi tự động, chỉ khi có sự can thiệp của người quản trị mạng.

**Đặc điểm của Giao thức Định tuyến Tĩnh**:
1. **Cấu hình thủ công**: Mọi tuyến đường được người quản trị cấu hình trực tiếp vào router, không có sự trao đổi thông tin định tuyến tự động giữa các router.
2. **Không tự động thay đổi**: Các tuyến đường tĩnh không thay đổi khi có sự thay đổi trong mạng (ví dụ: router hỏng hoặc link bị mất). Người quản trị phải cập nhật lại nếu có sự thay đổi.
3. **Định tuyến cố định**: Các router sẽ sử dụng tuyến đường được cấu hình cố định để chuyển tiếp gói tin đến các đích cụ thể.
4. **Không sử dụng băng thông mạng**: Vì không có giao tiếp giữa các router để trao đổi thông tin định tuyến, nó không sử dụng băng thông mạng như trong các giao thức định tuyến động.

**Cấu trúc của một tuyến đường tĩnh**:
Một tuyến đường tĩnh thông thường sẽ có các thành phần sau:
- **Địa chỉ đích (Destination Address)**: Địa chỉ IP của mạng đích.
- **Mặt nạ mạng (Subnet Mask)**: Xác định phần mạng của địa chỉ đích.
- **Địa chỉ Gateway (Next-Hop)**: Địa chỉ IP của router tiếp theo, nơi gói tin sẽ được gửi tới.
- **Interface**: Giao diện mạng trên router mà gói tin sẽ rời đi.

**Ưu điểm của Giao thức Định tuyến Tĩnh**:
1. **Đơn giản và dễ cấu hình**: Cấu hình rất đơn giản và dễ dàng thực hiện, đặc biệt là trong các mạng nhỏ hoặc mạng ít thay đổi.
2. **Tiết kiệm tài nguyên**: Không cần tài nguyên hệ thống hoặc băng thông mạng để trao đổi thông tin định tuyến, nên rất tiết kiệm tài nguyên.
3. **Bảo mật**: Vì không có việc trao đổi thông tin định tuyến, giao thức tĩnh hạn chế nguy cơ tấn công liên quan đến việc chiếm quyền điều khiển định tuyến.
4. **Kiểm soát chính xác**: Người quản trị có thể kiểm soát hoàn toàn các tuyến đường, dễ dàng cấu hình và điều chỉnh chúng cho phù hợp với yêu cầu cụ thể.

**Nhược điểm của Giao thức Định tuyến Tĩnh**:
1. **Không linh hoạt**: Nếu có sự thay đổi trong cấu trúc mạng (chẳng hạn router bị lỗi hoặc link không khả dụng), các tuyến đường không thể tự động thay đổi. Người quản trị phải thay đổi cấu hình thủ công.
2. **Khó mở rộng**: Khi mạng trở nên lớn và phức tạp, việc quản lý các tuyến đường tĩnh có thể rất khó khăn và dễ xảy ra lỗi.
3. **Khả năng phục hồi kém**: Nếu một router hoặc link gặp sự cố, các tuyến đường tĩnh không thể tự động chuyển sang tuyến đường thay thế, dẫn đến gián đoạn dịch vụ.

**Cách cấu hình Định tuyến Tĩnh trên Ubuntu**:

Trên hệ điều hành Ubuntu, bạn có thể cấu hình định tuyến tĩnh bằng cách chỉnh sửa file cấu hình mạng hoặc sử dụng lệnh `ip route`.

1. **Sử dụng lệnh `ip route`**:
   Cấu hình một tuyến đường tĩnh từ terminal:
   ```bash
   sudo ip route add <Địa chỉ đích>/<mặt nạ mạng> via <Địa chỉ Gateway> dev <Tên giao diện>
   ```
   Ví dụ:
   ```bash
   sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
   ```
   Lệnh này sẽ thêm một tuyến đường tĩnh cho mạng `192.168.2.0/24` thông qua gateway `192.168.1.1` và sử dụng giao diện mạng `eth0`.

2. **Cấu hình trong file `/etc/network/interfaces`**:
   Bạn có thể cấu hình định tuyến tĩnh bằng cách thêm các dòng vào file cấu hình mạng:
   ```bash
   sudo nano /etc/network/interfaces
   ```
   Thêm các dòng sau vào file cấu hình để thêm tuyến đường tĩnh:
   ```bash
   up ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
   ```
   Sau đó, khởi động lại dịch vụ mạng để áp dụng cấu hình:
   ```bash
   sudo systemctl restart networking
   ```

3. **Cấu hình trong file `/etc/netplan/*.yaml` (Ubuntu 18.04 trở lên)**:
   Với Ubuntu 18.04 và các phiên bản mới hơn sử dụng Netplan, bạn có thể cấu hình định tuyến tĩnh bằng cách sửa file YAML trong thư mục `/etc/netplan/`.
   ```bash
   sudo nano /etc/netplan/00-installer-config.yaml
   ```
   Thêm phần cấu hình tĩnh vào file YAML:
   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       eth0:
         dhcp4: true
         routes:
           - to: 192.168.2.0/24
             via: 192.168.1.1
             metric: 100
   ```
   Áp dụng cấu hình mới:
   ```bash
   sudo netplan apply
   ```

**Khi nào nên sử dụng Định tuyến Tĩnh**:
1. **Mạng nhỏ và ổn định**: Đối với các mạng nhỏ hoặc mạng không thay đổi thường xuyên, định tuyến tĩnh là một giải pháp đơn giản và hiệu quả.
2. **Mạng không cần tính linh hoạt cao**: Nếu không yêu cầu khả năng phục hồi tự động hoặc thay đổi mạng thường xuyên, định tuyến tĩnh là một lựa chọn phù hợp.
3. **Bảo mật cao**: Khi cần kiểm soát chính xác các tuyến đường và giảm thiểu nguy cơ tấn công hoặc sự xâm nhập, định tuyến tĩnh sẽ đảm bảo rằng thông tin về định tuyến không được chia sẻ.
4. **Mạng với yêu cầu hiệu suất cao**: Định tuyến tĩnh không yêu cầu băng thông để trao đổi thông tin định tuyến, giúp tối ưu hóa hiệu suất mạng trong các tình huống nhất định.

**Ví dụ về một tình huống sử dụng Định tuyến Tĩnh**:
Giả sử bạn có một mạng công ty nhỏ gồm 3 router:
- **Router A** kết nối với **Router B** và **Router C**.
- **Router B** kết nối với mạng 192.168.1.0/24.
- **Router C** kết nối với mạng 192.168.2.0/24.

Giả sử router A cần gửi gói tin tới mạng 192.168.2.0/24 qua router B và router C.

1. Trên **Router A**, bạn sẽ cấu hình tuyến đường tĩnh như sau:
   ```bash
   ip route add 192.168.2.0/24 via 192.168.1.2
   ```
   (Giả sử 192.168.1.2 là địa chỉ của Router B)

2. Trên **Router B**, bạn sẽ cấu hình tuyến đường tĩnh như sau:
   ```bash
   ip route add 192.168.2.0/24 via 192.168.1.3
   ```
   (Giả sử 192.168.1.3 là địa chỉ của Router C)

Khi đó, Router A sẽ gửi gói tin đến Router B, và Router B sẽ tiếp tục chuyển gói tin đến Router C để đến mạng 192.168.2.0/24.

----------------

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

-----------------

**1.2 Định tuyến động (Dynamic Routing)**

Đây là quá trình mà các đường đi được học hoặc điều chỉnh tự động bởi các router thông qua sử dụng các giao thức định tuyến. Các giao thức này, như RIP, OSPF, EIGRP, BGP, v.v., cho phép router trao đổi thông tin và tự động cập nhật bảng định tuyến để phản ánh các thay đổi trong mạng, chẳng hạn như các đường liên kết mới hoặc các đường liên kết bị hỏng.

-------------------

### **Routing Table**

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


Dưới đây là hướng dẫn chi tiết:

**1. Xác định Tệp Cấu Hình Netplan**

Netplan sử dụng các tệp YAML để cấu hình mạng, thường nằm trong thư mục `/etc/netplan/`. Các tệp này có tên như `00-installer-config.yaml` hoặc các tệp khác tùy thuộc vào hệ thống của bạn.

Để xác định chính xác tệp cấu hình, bạn có thể liệt kê các tệp trong thư mục `/etc/netplan/`:
```bash
ls /etc/netplan/
```

**2. Sửa Tệp Cấu Hình Netplan**

Giả sử tệp cấu hình của bạn là `00-installer-config.yaml`. Bạn sẽ mở tệp này để chỉnh sửa.

```bash
sudo nano /etc/netplan/00-installer-config.yaml
```

---

**3. Thêm Định Tuyến Tĩnh vào Cấu Hình**

Trong tệp cấu hình Netplan, dưới phần cấu hình của giao diện mạng (thường là `eth0` hoặc `enpXsY`), bạn có thể thêm phần `routes` để cấu hình định tuyến tĩnh. 

Ví dụ: Cấu hình một tuyến đường tĩnh để gửi gói tin đến mạng `192.168.2.0/24` qua gateway `192.168.1.1`.

Cấu trúc file YAML có thể trông như sau:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
      routes:
        - to: 192.168.2.0/24
          via: 192.168.1.1
          metric: 100
```

**Giải thích**:
- `to: 192.168.2.0/24`: Địa chỉ đích là mạng `192.168.2.0/24`.
- `via: 192.168.1.1`: Địa chỉ gateway tiếp theo mà gói tin sẽ được gửi đến (router).
- `metric: 100`: (Tùy chọn) Chỉ định độ ưu tiên của tuyến đường, tuyến có `metric` thấp hơn sẽ được ưu tiên. Bạn có thể bỏ qua dòng này nếu không cần.


**4. Áp Dụng Cấu Hình**

Sau khi chỉnh sửa xong tệp YAML, bạn cần áp dụng cấu hình để các thay đổi có hiệu lực.

```bash
sudo netplan apply
```

Lệnh này sẽ áp dụng các thay đổi cấu hình mà bạn vừa thực hiện.

**5. Kiểm Tra Bảng Định Tuyến**

Sau khi áp dụng cấu hình, bạn có thể kiểm tra lại bảng định tuyến của hệ thống để đảm bảo rằng tuyến đường tĩnh đã được thêm vào.

```bash
ip route show
```

Bạn sẽ thấy một dòng tương tự như:
```
192.168.2.0/24 via 192.168.1.1 dev eth0 metric 100
```

Điều này chứng tỏ tuyến đường tĩnh đã được cấu hình và hệ thống có thể sử dụng nó để định tuyến gói tin đến mạng `192.168.2.0/24` qua gateway `192.168.1.1`.

---

**6. Cấu Hình Định Tuyến Tĩnh Nhiều Gateway**

Nếu bạn cần thêm nhiều tuyến đường tĩnh, chỉ cần thêm các mục vào phần `routes` trong tệp YAML.

Ví dụ, để thêm một tuyến đường đến mạng `192.168.3.0/24` qua gateway `192.168.1.2`, bạn có thể cấu hình như sau:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: true
      routes:
        - to: 192.168.2.0/24
          via: 192.168.1.1
        - to: 192.168.3.0/24
          via: 192.168.1.2
          metric: 200
```

---

**7. Các Lựa Chọn Thêm trong Cấu Hình Định Tuyến Tĩnh**

- **`metric`**: Như đã đề cập ở trên, `metric` là độ ưu tiên của tuyến đường. Nếu bạn có nhiều tuyến đường đến cùng một đích, tuyến đường có `metric` thấp sẽ được ưu tiên.
- **`on-link`**: Thêm tùy chọn này để báo cho hệ thống biết rằng gateway không cần phải có tuyến đường định sẵn. Điều này hữu ích khi gateway nằm trong cùng mạng con.
  
Ví dụ:
```yaml
        - to: 192.168.2.0/24
          via: 192.168.1.1
          on-link: true
```

**Tóm Tắt Các Bước Cấu Hình Định Tuyến Tĩnh trên Ubuntu 20.04 trở lên**

1. **Xác định tệp cấu hình Netplan**:
   - Mở thư mục `/etc/netplan/` để tìm tệp cấu hình (ví dụ `00-installer-config.yaml`).
   
2. **Chỉnh sửa tệp cấu hình**:
   - Thêm các tuyến đường tĩnh vào phần `routes` dưới giao diện mạng (ví dụ `eth0`).
   
3. **Áp dụng cấu hình**:
   - Dùng lệnh `sudo netplan apply` để áp dụng cấu hình mới.

4. **Kiểm tra bảng định tuyến**:
   - Sử dụng lệnh `ip route show` để xác nhận tuyến đường tĩnh đã được thêm vào.


