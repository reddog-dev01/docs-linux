### **Tạo DHCP và DNS tương tự LAB1 và 4**

### **Tạo iptables NAT**

Để cấu hình **iptables** cho **NAT (Network Address Translation)** chi tiết, bạn cần thực hiện một số bước sau:

#### Bước 1: Bật IP Forwarding
Trước tiên, bạn cần đảm bảo rằng hệ thống của bạn cho phép chuyển tiếp gói tin giữa các giao diện mạng (IP forwarding). Điều này là cần thiết để hoạt động NAT có thể diễn ra.

1. Kiểm tra xem IP forwarding đã được bật chưa:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Nếu kết quả trả về là `0`, bạn cần bật IP forwarding.

2. Để bật IP forwarding tạm thời (không cần khởi động lại):

```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
```

3. Để bật IP forwarding vĩnh viễn (giữ nguyên sau khi khởi động lại), chỉnh sửa file `/etc/sysctl.conf` và tìm (hoặc thêm) dòng sau:

```bash
net.ipv4.ip_forward = 1
```

Sau đó, áp dụng cấu hình:

```bash
sudo sysctl -p
```

#### Bước 2: Cấu hình iptables để NAT

1. **Cấu hình NAT để chuyển tiếp lưu lượng từ mạng nội bộ ra ngoài Internet:**

Giả sử rằng giao diện mạng bên ngoài của bạn là `eth0` (kết nối với Internet) và giao diện mạng nội bộ là `eth1` (mạng mà các client của bạn sẽ kết nối).

- **POSTROUTING**: Chúng ta sẽ thêm quy tắc vào chuỗi **POSTROUTING** của bảng **nat** để thay đổi địa chỉ nguồn của các gói tin (source address) khi chúng ra khỏi mạng nội bộ và ra ngoài Internet.

```bash
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Giải thích:
- `-t nat`: Chỉ định bảng **NAT**.
- `-A POSTROUTING`: Thêm quy tắc vào chuỗi **POSTROUTING** để xử lý gói tin sau khi chúng ra khỏi hệ thống.
- `-o eth0`: Đối với các gói tin gửi ra ngoài qua giao diện `eth0` (kết nối Internet).
- `-j MASQUERADE`: Thực hiện thao tác **masquerading**, thay đổi địa chỉ nguồn của gói tin thành địa chỉ IP của giao diện `eth0` (IP công cộng của server).

2. **Chuyển tiếp lưu lượng giữa các giao diện mạng:**

Giả sử bạn có mạng nội bộ kết nối với `eth1`. Để cho phép các gói tin từ mạng nội bộ được chuyển tiếp giữa `eth1` (mạng LAN) và `eth0` (Internet), bạn cần cấu hình **iptables** như sau:

```bash
sudo iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
sudo iptables -A FORWARD -i eth0 -o eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT
```

Giải thích:
- `-A FORWARD`: Thêm quy tắc vào chuỗi **FORWARD** để xử lý các gói tin được chuyển tiếp giữa các giao diện mạng.
- `-i eth1 -o eth0 -j ACCEPT`: Cho phép gói tin đi từ mạng nội bộ (`eth1`) ra ngoài Internet (`eth0`).
- `-i eth0 -o eth1 -m state --state ESTABLISHED,RELATED -j ACCEPT`: Cho phép các gói tin từ Internet (`eth0`) phản hồi lại các kết nối đã được thiết lập (và các kết nối liên quan) và chuyển tiếp về lại mạng nội bộ (`eth1`).

#### Bước 3: Lưu cấu hình iptables

Các quy tắc iptables được áp dụng chỉ trong phiên làm việc hiện tại. Để giữ các quy tắc này sau khi khởi động lại hệ thống, bạn cần lưu lại cấu hình:

1. **Cài đặt iptables-persistent** để lưu các quy tắc iptables:

```bash
sudo apt install iptables-persistent
```

2. Sau khi cài đặt, bạn sẽ được yêu cầu lưu các quy tắc iptables hiện tại. Nếu không, bạn có thể lưu thủ công bằng cách:

```bash
sudo netfilter-persistent save
```

3. Kiểm tra lại các quy tắc đã được lưu chưa:

```bash
sudo iptables -t nat -L -n -v
sudo iptables -L -n -v
```

#### Bước 4: Kiểm tra NAT và Forwarding

1. **Kiểm tra IP forwarding**:

Đảm bảo rằng IP forwarding đang bật:

```bash
cat /proc/sys/net/ipv4/ip_forward
```

Kết quả trả về phải là `1`.

2. **Kiểm tra iptables**:

Kiểm tra lại các quy tắc NAT đã áp dụng:

```bash
sudo iptables -t nat -L -n -v
```

Kiểm tra chuỗi **FORWARD**:

```bash
sudo iptables -L FORWARD -n -v
```

3. **Kiểm tra kết nối từ client**:

- Trên máy client, kiểm tra xem IP được cấp phát từ DHCP server có hợp lệ không.
- Thử truy cập Internet từ máy client để đảm bảo NAT hoạt động tốt.

#### Bước 5: Cấu hình Firewall (Tùy chọn)

Nếu bạn đang sử dụng **ufw** (Uncomplicated Firewall), bạn cần cho phép lưu lượng chuyển tiếp:

```bash
sudo ufw allow from 192.168.1.0/24 to any port 53,80,443
```

Điều này cho phép các client trong mạng nội bộ (ví dụ: 192.168.1.0/24) có thể truy cập các dịch vụ như DNS, HTTP và HTTPS.

