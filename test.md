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
