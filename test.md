Trong file cấu hình mạng trên Ubuntu, bạn sẽ thấy một số tham số quan trọng. Dưới đây là ý nghĩa của các tham số trong ví dụ cấu hình IP động mà tôi đã cung cấp:

### 1. **network**:
   - Đây là phần chính của cấu hình, chỉ ra rằng chúng ta đang cấu hình các thiết lập mạng cho hệ thống.

### 2. **version**:
   - Xác định phiên bản cấu hình của `netplan`. Phiên bản `2` là phiên bản hiện tại và được sử dụng trong các bản Ubuntu gần đây.

### 3. **renderer**:
   - Chỉ định trình điều khiển hoặc công cụ được sử dụng để xử lý các cấu hình mạng. Trong trường hợp này, `networkd` là trình điều khiển hệ thống mạng của `systemd`, được sử dụng để quản lý các kết nối mạng.

### 4. **ethernets**:
   - Đây là phần cấu hình dành cho kết nối mạng Ethernet (mạng có dây). Bạn sẽ thấy các thông tin liên quan đến card mạng của bạn dưới mục này.

### 5. **enp3s0**:
   - Đây là tên của card mạng bạn muốn cấu hình. Trong ví dụ này, "enp3s0" là tên của card mạng Ethernet. Tên này có thể khác nhau trên các hệ thống khác nhau, và bạn có thể kiểm tra tên card mạng của mình bằng cách chạy lệnh `ip a`.

### 6. **dhcp4**:
   - Tham số này cho phép card mạng sử dụng giao thức DHCP để tự động nhận địa chỉ IP. 
   - `dhcp4: true` có nghĩa là bạn đang cấu hình card mạng nhận địa chỉ IPv4 động từ DHCP server. Nếu bạn muốn sử dụng DHCP cho IPv6, bạn có thể sử dụng tham số `dhcp6: true`.

### Cấu hình ví dụ đầy đủ:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: true
```

**Giải thích**: Cấu hình này nói rằng:
- Hệ thống mạng sử dụng cấu hình phiên bản 2.
- Dùng trình điều khiển `networkd` để quản lý các kết nối mạng.
- Card mạng "enp3s0" sẽ sử dụng DHCP để nhận địa chỉ IPv4 tự động.

Nếu bạn cần thay đổi cấu hình IP tĩnh hoặc thực hiện các thay đổi khác, bạn có thể thay đổi các tham số phù hợp trong file này.

Khi cấu hình IP động trên hệ thống Ubuntu (hoặc các hệ điều hành Linux khác sử dụng `netplan`), bạn sẽ thấy một số tham số quan trọng trong tệp cấu hình mạng (`/etc/netplan/xxx.yaml`). Dưới đây là các tham số cấu hình IP động cơ bản và ý nghĩa của chúng:

### 1. **network**:
   - Đây là phần chứa cấu hình mạng chính cho hệ thống. Tất cả các thông số mạng đều được định nghĩa dưới mục này.

### 2. **version**:
   - **Ý nghĩa**: Chỉ ra phiên bản của cấu hình `netplan` đang sử dụng. Ví dụ:
     - `version: 2` là phiên bản hiện tại của cấu hình mạng.
   
   **Cấu hình mẫu**:
   ```yaml
   version: 2
   ```

### 3. **renderer**:
   - **Ý nghĩa**: Chỉ định công cụ hoặc trình điều khiển sử dụng để quản lý cấu hình mạng. Có hai renderer phổ biến:
     - **networkd**: Dùng `systemd-networkd`, thường được sử dụng trong các máy chủ hoặc hệ thống không có giao diện đồ họa.
     - **NetworkManager**: Dùng cho các hệ thống desktop, có giao diện đồ họa và hỗ trợ quản lý kết nối mạng dễ dàng hơn.

   **Cấu hình mẫu**:
   ```yaml
   renderer: networkd  # Hoặc networkmanager
   ```

### 4. **ethernets**:
   - **Ý nghĩa**: Đây là mục cấu hình dành cho các kết nối mạng Ethernet (mạng có dây). Bạn sẽ cấu hình các card mạng trong mục này.
   - **ethernets** chứa tên các thiết bị mạng và các thiết lập mạng liên quan như IP, gateway, DNS, v.v.

   **Cấu hình mẫu**:
   ```yaml
   ethernets:
     enp3s0:  # Tên card mạng, thay thế theo tên thiết bị mạng của bạn
       dhcp4: true  # Sử dụng DHCP để nhận địa chỉ IPv4 tự động
   ```

### 5. **dhcp4**:
   - **Ý nghĩa**: Chỉ định việc sử dụng DHCP (Dynamic Host Configuration Protocol) cho địa chỉ IPv4. Nếu đặt `dhcp4: true`, hệ thống sẽ tự động nhận địa chỉ IP từ máy chủ DHCP.
   - **Giá trị**:
     - `true`: Kích hoạt DHCP cho IPv4.
     - `false`: Tắt DHCP cho IPv4 (nếu bạn muốn cấu hình địa chỉ IP tĩnh).
   
   **Cấu hình mẫu**:
   ```yaml
   dhcp4: true
   ```

### 6. **dhcp6**:
   - **Ý nghĩa**: Chỉ định việc sử dụng DHCP cho IPv6. Giống như `dhcp4`, nếu đặt `dhcp6: true`, hệ thống sẽ tự động nhận địa chỉ IP từ máy chủ DHCP hỗ trợ IPv6.
   - **Giá trị**:
     - `true`: Kích hoạt DHCP cho IPv6.
     - `false`: Tắt DHCP cho IPv6.
   
   **Cấu hình mẫu**:
   ```yaml
   dhcp6: true
   ```

### 7. **nameservers**:
   - **Ý nghĩa**: Cấu hình DNS (Domain Name System) để hệ thống có thể giải quyết tên miền (ví dụ: `google.com`).
   - **Giá trị**: Danh sách các địa chỉ IP của máy chủ DNS (có thể là DNS của ISP, hoặc công cộng như Google DNS, Cloudflare DNS).
   
   **Cấu hình mẫu**:
   ```yaml
   nameservers:
     addresses:
       - 8.8.8.8      # DNS của Google
       - 8.8.4.4      # DNS dự phòng của Google
   ```

### 8. **gateway4**:
   - **Ý nghĩa**: Chỉ định địa chỉ của cổng mặc định (gateway) cho IPv4. Đây là địa chỉ IP của router hoặc gateway mà hệ thống sẽ sử dụng để kết nối ra ngoài mạng.
   - **Giá trị**: Địa chỉ IP của cổng mặc định.
   
   **Cấu hình mẫu**:
   ```yaml
   gateway4: 192.168.1.1
   ```

### 9. **routes**:
   - **Ý nghĩa**: Cấu hình các tuyến đường mạng tĩnh cho hệ thống.
   - **Giá trị**: Địa chỉ mạng đích và địa chỉ gateway để định tuyến.
   
   **Cấu hình mẫu**:
   ```yaml
   routes:
     - to: 0.0.0.0/0        # Địa chỉ mạng đích
       via: 192.168.1.1     # Gateway để đi qua
   ```

### 10. **mtu**:
   - **Ý nghĩa**: Maximum Transmission Unit (MTU) là kích thước tối đa của một gói dữ liệu mà giao thức mạng có thể truyền đi. Cấu hình này có thể thay đổi tùy theo yêu cầu của mạng (đối với các mạng cần tối ưu hóa hiệu suất).
   - **Giá trị**: Kích thước MTU tính bằng byte (ví dụ: `1500`).
   
   **Cấu hình mẫu**:
   ```yaml
   mtu: 1500
   ```

### Cấu hình IP động đầy đủ:

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: true  # Dùng DHCP để nhận địa chỉ IP IPv4 động
      dhcp6: true  # Dùng DHCP để nhận địa chỉ IPv6 động
      nameservers:
        addresses:
          - 8.8.8.8  # DNS của Google
          - 8.8.4.4  # DNS dự phòng của Google
      gateway4: 192.168.1.1  # Địa chỉ Gateway IPv4
```

### Tổng kết:

- **dhcp4** và **dhcp6**: Cho phép cấu hình IP động cho các phiên bản IPv4 và IPv6.
- **nameservers**: Cấu hình DNS để hệ thống có thể giải quyết tên miền.
- **gateway4**: Cấu hình cổng mặc định (gateway) cho IPv4.
- **renderer**: Chỉ định công cụ quản lý kết nối mạng.
- **ethernets**: Cấu hình các card mạng có dây (Ethernet).

Như vậy, cấu hình IP động giúp thiết bị tự động nhận địa chỉ IP từ máy chủ DHCP, giảm thiểu công việc cấu hình thủ công và dễ dàng quản lý mạng.
**Cấu hình IP động** là việc cấu hình cho hệ thống (máy tính, thiết bị mạng, v.v.) tự động nhận địa chỉ IP từ một máy chủ DHCP (Dynamic Host Configuration Protocol). Mục đích của việc này là giúp thiết bị tự động kết nối với mạng mà không cần người dùng phải cấu hình địa chỉ IP thủ công.

### Tại sao phải cấu hình IP động?

1. **Dễ dàng và tự động hóa**:
   - **Tiện lợi**: Khi sử dụng IP động, thiết bị không cần phải cấu hình thủ công địa chỉ IP, subnet mask, gateway, và DNS. Các thông tin này sẽ được cung cấp tự động từ máy chủ DHCP.
   - **Tiết kiệm thời gian**: Đặc biệt là trong các mạng lớn, việc cấu hình IP động giúp tiết kiệm rất nhiều thời gian và công sức. Mỗi thiết bị chỉ cần kết nối với mạng và nhận địa chỉ IP tự động mà không cần phải can thiệp thủ công.

2. **Quản lý mạng dễ dàng**:
   - **Không cần phải theo dõi từng địa chỉ IP**: DHCP sẽ tự động cấp phát địa chỉ IP mà không gây ra xung đột hoặc trùng lặp, điều này giúp quản lý mạng trở nên đơn giản hơn, đặc biệt với một số lượng thiết bị lớn.
   - **Phân phối địa chỉ IP hiệu quả**: Máy chủ DHCP có thể quản lý phạm vi các địa chỉ IP và cấp phát chúng cho các thiết bị khi cần thiết, giảm thiểu việc lãng phí địa chỉ IP.

3. **Tính linh hoạt**:
   - **Di chuyển giữa các mạng**: Nếu một thiết bị di chuyển giữa các mạng (ví dụ: laptop, điện thoại), IP động giúp thiết bị dễ dàng kết nối với các mạng khác mà không cần cấu hình lại địa chỉ IP mỗi khi thay đổi mạng.
   - **Mạng không cố định**: IP động rất hữu ích trong các môi trường mạng mà thiết bị thường xuyên kết nối và ngắt kết nối như Wi-Fi công cộng, nơi bạn không cần phải quản lý mỗi địa chỉ IP cụ thể.

4. **Giảm thiểu sai sót và xung đột**:
   - **Tránh xung đột IP**: Nếu có hai thiết bị trong cùng một mạng đều được cấp cùng một địa chỉ IP tĩnh, sẽ dẫn đến xung đột IP và gây lỗi kết nối. DHCP giúp tránh được tình trạng này vì nó tự động cấp phát địa chỉ IP duy nhất cho từng thiết bị.
   
5. **Quản lý hiệu quả trong môi trường thay đổi**:
   - **Mạng có sự thay đổi liên tục**: Trong các mạng có sự thay đổi nhiều thiết bị (có thể là các thiết bị di động, laptop của nhân viên, khách hàng kết nối vào mạng), việc sử dụng DHCP giúp dễ dàng quản lý hơn, vì các địa chỉ IP được cấp phát và thu hồi một cách tự động.

### Ví dụ ứng dụng của IP động:
- **Mạng gia đình**: Nếu bạn có nhiều thiết bị như máy tính, điện thoại, máy in kết nối vào mạng Wi-Fi của mình, bạn không cần phải cấu hình thủ công mỗi thiết bị. DHCP sẽ cấp phát địa chỉ IP tự động cho từng thiết bị khi chúng kết nối vào mạng.
- **Mạng công ty**: Trong các doanh nghiệp với hàng nghìn máy tính và thiết bị di động, việc sử dụng DHCP giúp quản lý mạng dễ dàng hơn vì không cần cấu hình thủ công từng thiết bị. Hệ thống DHCP sẽ tự động cấp phát địa chỉ IP cho các thiết bị khi chúng kết nối vào mạng của công ty.

### Tóm lại:
Cấu hình IP động giúp việc quản lý mạng trở nên đơn giản, linh hoạt và giảm thiểu sai sót trong việc cấp phát địa chỉ IP cho các thiết bị. Nó giúp tự động hóa quá trình kết nối thiết bị vào mạng mà không cần sự can thiệp thủ công của người dùng, đồng thời tránh được các vấn đề về xung đột địa chỉ IP.



Để cấu hình IP tĩnh cho một giao diện mạng (network interface) trên Ubuntu, bạn sẽ chỉnh sửa file cấu hình của `netplan`. Dưới đây là các bước chi tiết:

### 1. **Xác định tên của interface mạng**:
   Trước tiên, bạn cần biết tên của card mạng mà bạn muốn cấu hình IP tĩnh. Bạn có thể sử dụng lệnh sau để liệt kê các giao diện mạng:

   ```bash
   ip a
   ```

   Hoặc bạn cũng có thể sử dụng lệnh `ifconfig` nếu công cụ này đã được cài đặt.

   Giả sử tên giao diện mạng của bạn là `enp3s0`.

### 2. **Chỉnh sửa file cấu hình netplan**:
   Tệp cấu hình của `netplan` thường nằm trong thư mục `/etc/netplan/`. Các tệp này có phần mở rộng `.yaml`. Bạn cần chỉnh sửa tệp phù hợp với giao diện của bạn.

   Ví dụ, nếu tệp cấu hình của bạn là `01-netcfg.yaml`, bạn có thể mở nó bằng lệnh:

   ```bash
   sudo nano /etc/netplan/01-netcfg.yaml
   ```

### 3. **Cấu hình IP tĩnh**:
   Trong tệp cấu hình, bạn cần chỉ định thông tin IP tĩnh cho giao diện mạng. Cấu hình ví dụ dưới đây cho phép bạn cấu hình IP tĩnh cho giao diện `enp3s0`:

   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       enp3s0:
         dhcp4: false  # Tắt DHCP IPv4
         addresses:
           - 192.168.1.100/24  # Địa chỉ IP tĩnh và subnet mask
         gateway4: 192.168.1.1  # Cổng mặc định (gateway)
         nameservers:
           addresses:
             - 8.8.8.8   # DNS của Google
             - 8.8.4.4   # DNS dự phòng của Google
   ```

   Giải thích cấu hình:
   - **dhcp4: false**: Tắt chế độ DHCP cho IPv4 (sử dụng IP tĩnh thay vì DHCP).
   - **addresses**: Địa chỉ IP tĩnh và subnet mask (`/24` là subnet mask 255.255.255.0).
   - **gateway4**: Địa chỉ của cổng mặc định (gateway).
   - **nameservers**: Các máy chủ DNS để phân giải tên miền.

### 4. **Áp dụng cấu hình**:
   Sau khi lưu và đóng tệp cấu hình (nhấn `Ctrl + X`, sau đó chọn `Y` để lưu và `Enter`), bạn cần áp dụng cấu hình mới bằng cách sử dụng lệnh:

   ```bash
   sudo netplan apply
   ```

   Điều này sẽ áp dụng cấu hình IP tĩnh cho giao diện mạng của bạn.

### 5. **Kiểm tra kết quả**:
   Để kiểm tra xem cấu hình IP tĩnh đã được áp dụng thành công, bạn có thể sử dụng lệnh `ip a` để xem địa chỉ IP của giao diện:

   ```bash
   ip a
   ```

   Đảm bảo rằng địa chỉ IP bạn cấu hình hiển thị trong kết quả.

### Ví dụ cấu hình IP tĩnh đầy đủ:

Giả sử bạn muốn cấu hình một địa chỉ IP tĩnh cho giao diện mạng `enp3s0` với địa chỉ IP `192.168.1.100`, gateway `192.168.1.1`, và sử dụng DNS của Google (`8.8.8.8` và `8.8.4.4`):

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: false
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses:
          - 8.8.8.8
          - 8.8.4.4
```

Sau khi áp dụng, giao diện `enp3s0` sẽ sử dụng IP tĩnh `192.168.1.100` thay vì nhận IP tự động từ DHCP.

--------

Giao thức **DHCP (Dynamic Host Configuration Protocol)** là một giao thức mạng cho phép các thiết bị trong mạng tự động nhận các thông tin cấu hình mạng, như **địa chỉ IP**, **cổng mặc định (default gateway)**, **DNS server**, và các thông số khác mà không cần phải cấu hình thủ công trên mỗi thiết bị. Cơ chế hoạt động của DHCP giúp giảm thiểu việc quản lý địa chỉ IP thủ công và giúp các thiết bị dễ dàng tham gia vào mạng mà không cần phải thiết lập chi tiết.

---

### **Cơ chế hoạt động của giao thức DHCP**

1. **Khởi tạo yêu cầu DHCP (DHCP Discover)**
   - Khi một thiết bị (chẳng hạn như máy tính, điện thoại hoặc máy chủ) được kết nối vào mạng lần đầu tiên hoặc sau khi khởi động lại, nó cần một **địa chỉ IP** để giao tiếp với các thiết bị khác trên mạng.
   - Thiết bị này gửi một **gói tin DHCP Discover** (gọi là broadcast) tới **các máy chủ DHCP** trong mạng. Yêu cầu này không có địa chỉ IP, vì thiết bị chưa có IP và không biết địa chỉ máy chủ DHCP, nên gói tin được gửi đi dưới dạng broadcast (quét toàn mạng).

2. **Máy chủ DHCP trả lời (DHCP Offer)**
   - Máy chủ DHCP nhận được gói tin DHCP Discover và gửi lại một **gói tin DHCP Offer**. Gói tin này chứa các thông tin cấu hình mạng cần thiết, bao gồm:
     - **Địa chỉ IP** mà máy chủ DHCP đề xuất cho thiết bị.
     - **Thời gian thuê (lease time)** của địa chỉ IP.
     - **Cổng mặc định** (default gateway).
     - **DNS server**.
     - Một số thông tin khác (tùy thuộc vào cấu hình của DHCP server).

3. **Thiết bị gửi yêu cầu xác nhận (DHCP Request)**
   - Sau khi nhận được **gói tin DHCP Offer**, thiết bị sẽ chọn một trong các gói tin (nếu có nhiều máy chủ DHCP phản hồi) và gửi lại một **gói tin DHCP Request**. Gói tin này yêu cầu **xác nhận** địa chỉ IP và các thông tin cấu hình mạng từ máy chủ DHCP.
   - Gói tin này cũng được gửi dưới dạng **broadcast**, thông báo cho tất cả các máy chủ DHCP biết rằng thiết bị đã chọn một máy chủ để cấu hình địa chỉ IP.

4. **Máy chủ DHCP xác nhận (DHCP Acknowledgment)**
   - Khi nhận được yêu cầu từ thiết bị (DHCP Request), máy chủ DHCP sẽ gửi lại một **gói tin DHCP Acknowledgment (DHCP ACK)** để xác nhận rằng thiết bị đã được cấp phát địa chỉ IP và có thể sử dụng địa chỉ này trong một khoảng thời gian cụ thể.
   - Sau khi nhận được gói tin **DHCP ACK**, thiết bị có thể bắt đầu sử dụng địa chỉ IP được cấp và các thông tin cấu hình khác để giao tiếp với mạng.

5. **Cập nhật lại thông tin khi hết thời gian thuê (DHCP Lease Renewal)**
   - Địa chỉ IP được cấp cho thiết bị qua DHCP có một **thời gian thuê** (lease time). Trước khi thời gian thuê kết thúc, thiết bị sẽ tự động gửi yêu cầu gia hạn (lease renewal) đến máy chủ DHCP để giữ lại địa chỉ IP.
   - Nếu máy chủ DHCP không phản hồi hoặc không gia hạn, thiết bị sẽ phải tìm một địa chỉ IP khác.

---

### **Các thành phần chính trong quá trình DHCP**
- **Client (Máy khách)**: Là thiết bị yêu cầu và nhận các thông tin mạng từ máy chủ DHCP. Ví dụ: máy tính, điện thoại, máy in, v.v.
- **Server (Máy chủ DHCP)**: Cung cấp địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị trong mạng.
- **Relay Agent (Máy chủ chuyển tiếp DHCP)**: Trong một số mạng phức tạp (khi máy chủ DHCP và client không nằm trong cùng một mạng con), có thể sử dụng **DHCP relay agent** để chuyển tiếp các gói tin DHCP giữa client và server.

---

### **Các loại địa chỉ IP cấp phát bởi DHCP**
- **Dynamic IP**: Địa chỉ IP được cấp phát cho client từ một **pool** địa chỉ IP mà máy chủ DHCP quản lý. Đây là loại IP thông dụng và sẽ hết hạn sau một thời gian.
- **Static IP**: Trong một số trường hợp, máy chủ DHCP có thể cấu hình cấp phát các **địa chỉ IP tĩnh** cho các thiết bị cụ thể dựa trên **địa chỉ MAC** của thiết bị.
- **Automatic IP**: Cung cấp địa chỉ IP từ một dải IP cố định, nhưng có thể thay đổi theo thời gian tùy theo yêu cầu.

---

### **Quá trình hoạt động chi tiết hơn**
- **Gói tin DHCP Discover**: 
  - Được gửi từ thiết bị yêu cầu (client) đến địa chỉ broadcast `255.255.255.255` hoặc địa chỉ multicast đặc biệt của mạng.
  
- **Gói tin DHCP Offer**: 
  - Máy chủ DHCP gửi lại thông tin đề xuất địa chỉ IP cho client, bao gồm cả **thời gian thuê** (lease time).
  
- **Gói tin DHCP Request**: 
  - Thiết bị client gửi yêu cầu xác nhận (broadcast) đến tất cả các máy chủ DHCP có thể, xác nhận máy chủ đã chọn.

- **Gói tin DHCP Acknowledgment**: 
  - Máy chủ DHCP gửi gói tin xác nhận rằng client đã được cấp phát IP và các thông tin cấu hình mạng.

---

### **Ưu điểm của DHCP**
1. **Tiết kiệm thời gian và công sức**: Không cần phải cấu hình địa chỉ IP thủ công cho từng thiết bị trong mạng.
2. **Quản lý linh hoạt**: Các địa chỉ IP có thể được cấp phát và thu hồi tự động, giúp quản lý mạng dễ dàng hơn.
3. **Giảm rủi ro lỗi cấu hình**: Các thiết bị nhận thông tin cấu hình chính xác từ máy chủ DHCP, giảm thiểu khả năng lỗi trong việc cấu hình mạng thủ công.

---

### **Tóm tắt**
Giao thức DHCP giúp tự động cấp phát địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị trong mạng mà không cần cấu hình thủ công. Quá trình này bao gồm các bước: yêu cầu, trả lời, xác nhận và cấp phát địa chỉ IP từ máy chủ DHCP. DHCP giúp quản lý mạng hiệu quả, giảm thiểu lỗi và tiết kiệm thời gian trong việc cấu hình mạng.

Lưu lại zalo nếu hết Plus 4.0: [08686.01263](https://zalo.me/0868601263).


-----

Để tạo và sử dụng Ansible Role, bạn cần tạo thư mục cho role và các tệp cấu hình trên máy tính của bạn. Dưới đây là hướng dẫn chi tiết về nơi và cách bạn có thể tạo các tệp và thư mục cần thiết.

### 1. **Tạo thư mục cho Role**

Trước hết, bạn cần xác định thư mục nơi bạn sẽ lưu trữ các role của Ansible. Thông thường, các role của Ansible được tạo trong thư mục `roles` trong thư mục dự án của bạn.

Giả sử bạn đang làm việc trong một dự án Ansible, bạn có thể tạo thư mục này trong thư mục chính của dự án:

```bash
mkdir -p ~/ansible-project/roles/my_role
```

### 2. **Tạo cấu trúc thư mục của Role**

Sau khi đã tạo thư mục cho role, bạn cần tạo các thư mục con bên trong `my_role` để tổ chức các tệp cấu hình, như đã mô tả ở trên.

Ví dụ, bạn có thể tạo cấu trúc thư mục như sau:

```bash
mkdir -p ~/ansible-project/roles/my_role/{defaults,files,handlers,meta,tasks,templates,vars,tests}
```

Cấu trúc này sẽ có dạng:

```
~/ansible-project/
├── roles/
│   └── my_role/
│       ├── defaults/
│       ├── files/
│       ├── handlers/
│       ├── meta/
│       ├── tasks/
│       ├── templates/
│       ├── vars/
│       └── tests/
```

### 3. **Tạo các tệp trong Role**

Tiếp theo, bạn cần tạo các tệp trong các thư mục mà bạn đã tạo. Ví dụ:

#### a. **defaults/main.yml**
Tạo tệp **defaults/main.yml** để khai báo các biến mặc định cho DHCP và DNS.

```bash
nano ~/ansible-project/roles/my_role/defaults/main.yml
```

Dán nội dung sau vào tệp:

```yaml
dhcp_subnet: "192.168.1.0"
dhcp_netmask: "255.255.255.0"
dhcp_range_start: "192.168.1.100"
dhcp_range_end: "192.168.1.200"
dhcp_gateway: "192.168.1.1"
dhcp_dns: "8.8.8.8"

dns_domains:
  - domain: "test1.com"
    ip: "1.2.3.4"
  - domain: "test2.com"
    ip: "1.2.3.4"
```

#### b. **vars/main.yml**
Tạo tệp **vars/main.yml** để cấu hình các biến nâng cao (ví dụ, tên dịch vụ DHCP và DNS tùy thuộc vào hệ điều hành).

```bash
nano ~/ansible-project/roles/my_role/vars/main.yml
```

Dán nội dung sau vào tệp:

```yaml
dhcp_interface: "eth0"  # Interface mạng cho DHCP server

dns_service_ubuntu: "bind9"
dns_service_centos: "named"

dhcp_service_ubuntu: "isc-dhcp-server"
dhcp_service_centos: "dhcpd"
```

#### c. **tasks/main.yml**
Tạo tệp **tasks/main.yml** để định nghĩa các tác vụ (ví dụ, cài đặt và cấu hình DHCP và DNS).

```bash
nano ~/ansible-project/roles/my_role/tasks/main.yml
```

Dán nội dung sau vào tệp:

```yaml
# Cài đặt DHCP server trên Ubuntu
- name: Install DHCP server (Ubuntu)
  apt:
    name: isc-dhcp-server
    state: present
  when: ansible_os_family == "Debian"

# Cài đặt DHCP server trên CentOS 7
- name: Install DHCP server (CentOS 7)
  yum:
    name: dhcp
    state: present
  when: ansible_os_family == "RedHat"

# Cài đặt Bind DNS server trên Ubuntu
- name: Install Bind DNS server (Ubuntu)
  apt:
    name: bind9
    state: present
  when: ansible_os_family == "Debian"

# Cài đặt Bind DNS server trên CentOS 7
- name: Install Bind DNS server (CentOS 7)
  yum:
    name: bind
    state: present
  when: ansible_os_family == "RedHat"

# Cấu hình DHCP server
- name: Configure DHCP server
  template:
    src: dhcpd.conf.j2
    dest: /etc/dhcp/dhcpd.conf
  notify:
    - Restart DHCP service

# Cấu hình DNS server
- name: Configure DNS server
  template:
    src: named.conf.j2
    dest: /etc/bind/named.conf.local
  notify:
    - Restart DNS service

# Khởi động và kích hoạt DHCP service
- name: Ensure DHCP service is running (Ubuntu)
  service:
    name: "{{ dhcp_service_ubuntu }}"
    state: started
    enabled: yes
  when: ansible_os_family == "Debian"

- name: Ensure DHCP service is running (CentOS 7)
  service:
    name: "{{ dhcp_service_centos }}"
    state: started
    enabled: yes
  when: ansible_os_family == "RedHat"

# Khởi động và kích hoạt DNS service
- name: Ensure DNS service is running (Ubuntu)
  service:
    name: "{{ dns_service_ubuntu }}"
    state: started
    enabled: yes
  when: ansible_os_family == "Debian"

- name: Ensure DNS service is running (CentOS 7)
  service:
    name: "{{ dns_service_centos }}"
    state: started
    enabled: yes
  when: ansible_os_family == "RedHat"
```

#### d. **templates/dhcpd.conf.j2**
Tạo tệp **templates/dhcpd.conf.j2** chứa cấu hình mẫu cho **DHCP server**.

```bash
nano ~/ansible-project/roles/my_role/templates/dhcpd.conf.j2
```

Dán nội dung sau vào tệp:

```jinja
subnet {{ dhcp_subnet }} netmask {{ dhcp_netmask }} {
  range {{ dhcp_range_start }} {{ dhcp_range_end }};
  option routers {{ dhcp_gateway }};
  option domain-name-servers {{ dhcp_dns }};
}
```

#### e. **templates/named.conf.j2**
Tạo tệp **templates/named.conf.j2** chứa cấu hình mẫu cho **DNS server**.

```bash
nano ~/ansible-project/roles/my_role/templates/named.conf.j2
```

Dán nội dung sau vào tệp:

```jinja
{% for domain in dns_domains %}
zone "{{ domain.domain }}" {
  type master;
  file "/etc/bind/db.{{ domain.domain }}";
};
{% endfor %}
```

#### f. **handlers/main.yml**
Tạo tệp **handlers/main.yml** để cấu hình các tác vụ sẽ được gọi khi có sự thay đổi (ví dụ: khởi động lại dịch vụ).

```bash
nano ~/ansible-project/roles/my_role/handlers/main.yml
```

Dán nội dung sau vào tệp:

```yaml
- name: Restart DHCP service (Ubuntu)
  service:
    name: "{{ dhcp_service_ubuntu }}"
    state: restarted
  when: ansible_os_family == "Debian"

- name: Restart DHCP service (CentOS 7)
  service:
    name: "{{ dhcp_service_centos }}"
    state: restarted
  when: ansible_os_family == "RedHat"

- name: Restart DNS service (Ubuntu)
  service:
    name: "{{ dns_service_ubuntu }}"
    state: restarted
  when: ansible_os_family == "Debian"

- name: Restart DNS service (CentOS 7)
  service:
    name: "{{ dns_service_centos }}"
    state: restarted
  when: ansible_os_family == "RedHat"
```

### 4. **Tạo Playbook**

Cuối cùng, tạo một **playbook** để sử dụng role này. Tạo tệp `playbook.yml` trong thư mục dự án của bạn:

```bash
nano ~/ansible-project/playbook.yml
```

Dán nội dung sau vào tệp:

```yaml
- hosts: all
  become: yes
  roles:
    - my_role
```

### 5. **Chạy Playbook**

Bây giờ bạn đã tạo xong role và playbook, bạn có thể chạy playbook để thực thi cấu hình trên các máy chủ.

```bash
ansible-playbook -i hosts playbook.yml
```

Trong đó, `hosts` là file inventory của bạn chứa danh sách các máy chủ mà bạn muốn áp dụng cấu hình.

---

### **Tóm tắt các bước:**

1. Tạo thư mục cho role và các thư mục con.
2. Tạo các tệp cấu hình trong role (`defaults`, `vars`, `tasks`, `templates`, `handlers`).
3. Tạo playbook sử dụng role.
4. Chạy playbook với lệnh `ansible-playbook`.

Lưu lại zalo nếu hết Plus 4.0: [08686.01263](https://zalo.me/0868601263).
