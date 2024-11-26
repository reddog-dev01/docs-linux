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
