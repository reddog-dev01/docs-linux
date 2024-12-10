### **Tạo máy ảo khi cấu hình DHCP**

- 2 máy ảo đều phải có adapter như hình

![image](https://github.com/user-attachments/assets/d4c8f569-d545-4091-8294-3636a8f7393e)

### **Cấu hình netplan**

**máy server**
```
sudo vim /etc/netplan/00-installer-config.yaml
```

![image](https://github.com/user-attachments/assets/92b83a7a-0836-4cac-8aab-3e7cc812ea59)

**máy client**

![image](https://github.com/user-attachments/assets/de24492c-959e-4642-9f1a-30ce1e6e3f70)


### Bước 1: Cài đặt ISC DHCP Server
Trước tiên, cần cài đặt ISC DHCP Server bằng lệnh:
```bash
sudo apt update
sudo apt install isc-dhcp-server
```

### Bước 2: Cấu hình DHCP Server
Tiếp theo, cấu hình DHCP Server bằng cách chỉnh sửa file `dhcpd.conf`.
```bash
sudo vim /etc/dhcp/dhcpd.conf
```
Thêm hoặc chỉnh sửa các dòng sau trong file cấu hình để thiết lập dải địa chỉ IP và các thông số mạng khác:

```bash
subnet 10.0.10.0 netmask 255.255.255.0 {
   range 10.0.10.10 10.0.10.100;  # Phạm vi địa chỉ IP cấp phát cho client
   option routers 10.0.10.1;       # Default gateway
   option subnet-mask 255.255.255.0; # Subnet mask
   option domain-name-servers 8.8.8.8, 8.8.4.4; # DNS Servers
   default-lease-time 600;         # Thời gian thuê mặc định
   max-lease-time 7200;            # Thời gian thuê tối đa
}
```

#### Giải thích các tham số cấu hình:
- **subnet 10.0.10.0 netmask 255.255.255.0**: Khai báo một subnet với địa chỉ mạng là 10.0.10.0 và subnet mask là 255.255.255.0.
- **range 10.0.10.10 10.0.10.100**: Xác định dải địa chỉ IP từ 10.0.10.10 đến 10.0.10.100 mà DHCP sẽ cấp cho các máy client.
- **option routers 10.0.10.1**: Chỉ định default gateway cho các máy client sử dụng là 10.0.10.1.
- **option subnet-mask 255.255.255.0**: Chỉ định subnet mask cho các máy client là 255.255.255.0.
- **option domain-name-servers 8.8.8.8, 8.8.4.4**: Chỉ định các DNS server mà các máy client sẽ sử dụng, trong trường hợp này là Google DNS.
- **default-lease-time 600**: Thời gian thuê mặc định cho một địa chỉ IP là 600 giây (10 phút).
- **max-lease-time 7200**: Thời gian thuê tối đa cho một địa chỉ IP là 7200 giây (2 giờ).

đặt IP tĩnh

```
host Server1 {
    hardware ethernet 08:00:07:26:c0:a5;
    fixed-address 10.0.10.88;
  }
```
host Server1 { ... }:

Tạo một khối cấu hình cho một thiết bị cụ thể trong mạng. Tên Server1 là tên mà bạn có thể đặt tùy ý để dễ nhận diện thiết bị.
hardware ethernet 08:00:07:26:c0:a5;:

Địa chỉ MAC của thiết bị. Địa chỉ MAC là một mã nhận diện duy nhất của card mạng (NIC) trên thiết bị. Trong ví dụ này, địa chỉ MAC là 08:00:07:26:c0:a5. Bạn cần thay thế giá trị này bằng địa chỉ MAC thực tế của thiết bị mà bạn muốn cấp IP cố định.
fixed-address 10.0.10.88;:

Địa chỉ IP cố định mà máy chủ DHCP sẽ cấp phát cho thiết bị có địa chỉ MAC 08:00:07:26:c0:a5. Khi thiết bị này yêu cầu một địa chỉ IP từ DHCP, nó sẽ luôn nhận được địa chỉ IP 10.0.10.88.

### Bước 3: Chỉ định giao diện mạng cho DHCP Server
Bạn cần chỉ định giao diện mạng mà DHCP server sẽ lắng nghe các yêu cầu. Mở file `/etc/default/isc-dhcp-server` để cấu hình:

```bash
sudo vim /etc/default/isc-dhcp-server
```
Tìm đến dòng `INTERFACESv4` và thêm tên giao diện mạng mà bạn muốn DHCP server sử dụng, ví dụ `eth0`:
```bash
INTERFACESv4="ens37"
```

### Bước 4: Khởi động lại dịch vụ DHCP
Sau khi đã cấu hình xong, khởi động lại dịch vụ DHCP để áp dụng cấu hình:
```bash
sudo systemctl restart isc-dhcp-server
```
Bạn có thể kiểm tra trạng thái của dịch vụ để đảm bảo nó đang hoạt động:
```bash
sudo systemctl status isc-dhcp-server
```
