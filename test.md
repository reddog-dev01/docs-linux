Cấu hình định tuyến tĩnh trên máy ảo Ubuntu chạy trong VMware có thể thực hiện qua các bước giống như cấu hình trên Ubuntu thông thường. Tuy nhiên, để đảm bảo rằng cấu hình được áp dụng chính xác trong môi trường máy ảo, bạn cần lưu ý một số điều kiện đặc biệt liên quan đến mạng trong VMware. Dưới đây là hướng dẫn chi tiết:

### **1. Kiểm Tra Cấu Hình Mạng Của Máy Ảo**

Trước khi cấu hình định tuyến tĩnh, bạn cần đảm bảo rằng máy ảo của bạn có cấu hình mạng hợp lý trong VMware:

#### **Kiểm Tra Thiết Lập Mạng trong VMware:**
- **Bridged Network (Mạng nối cầu)**: Máy ảo sẽ kết nối trực tiếp với mạng của máy chủ vật lý. Mạng máy ảo sẽ nhận địa chỉ IP từ cùng một DHCP server như máy chủ vật lý.
- **NAT Network (Mạng NAT)**: Máy ảo sẽ sử dụng mạng ảo và có một IP riêng, nhưng tất cả kết nối từ máy ảo ra ngoài đều đi qua máy chủ vật lý (máy chủ VMware).
- **Host-Only Network (Mạng chỉ có máy chủ)**: Máy ảo có thể kết nối với máy chủ vật lý và các máy ảo khác nhưng không thể truy cập internet.

Lựa chọn cấu hình mạng phù hợp với yêu cầu của bạn.

### **2. Cấu Hình Định Tuyến Tĩnh Trên Máy Ảo Ubuntu**

Sau khi xác nhận cấu hình mạng của máy ảo, bạn có thể tiếp tục cấu hình định tuyến tĩnh trên hệ thống Ubuntu trong máy ảo. Dưới đây là các bước cụ thể:

#### **Bước 1: Kiểm Tra Giao Diện Mạng**
Mở terminal trong máy ảo Ubuntu và kiểm tra các giao diện mạng hiện có bằng lệnh:
```bash
ip addr
```
Hoặc:
```bash
ifconfig
```
Lệnh này sẽ liệt kê tất cả các giao diện mạng có trên máy ảo, ví dụ `eth0`, `ens33`, `enp0s3`... (tên giao diện có thể thay đổi tùy vào bản phân phối Ubuntu và cấu hình mạng).

#### **Bước 2: Thêm Tuyến Đường Tĩnh**

Sử dụng lệnh `ip route` để thêm tuyến đường tĩnh. Ví dụ, bạn muốn thêm một tuyến đường đến mạng `192.168.2.0/24` qua gateway `192.168.1.1` trên giao diện `ens33`.

Cú pháp:
```bash
sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev ens33
```

- `192.168.2.0/24`: Mạng đích bạn muốn định tuyến.
- `192.168.1.1`: Gateway (địa chỉ IP của router hoặc next-hop).
- `ens33`: Tên giao diện mạng.

#### **Bước 3: Kiểm Tra Bảng Định Tuyến**
Sau khi thêm tuyến đường tĩnh, bạn có thể kiểm tra bảng định tuyến của máy ảo bằng lệnh:
```bash
ip route show
```

Nếu tuyến đường đã được thêm thành công, bạn sẽ thấy mạng đích và gateway trong bảng định tuyến.

---

### **3. Cấu Hình Định Tuyến Tĩnh Vĩnh Cửu**

Để đảm bảo rằng tuyến đường tĩnh vẫn tồn tại sau khi máy ảo khởi động lại, bạn cần thêm chúng vào các file cấu hình mạng.

#### **Trên Ubuntu 18.04 và các bản mới hơn (sử dụng `netplan`)**

Ubuntu 18.04 trở lên sử dụng **Netplan** để quản lý cấu hình mạng. Bạn cần chỉnh sửa các file cấu hình trong `/etc/netplan/` để thêm tuyến đường tĩnh.

1. Mở thư mục cấu hình Netplan:
   ```bash
   cd /etc/netplan/
   ```

2. Tìm và mở file cấu hình mạng (ví dụ: `00-installer-config.yaml` hoặc tên khác tùy thuộc vào hệ thống của bạn):
   ```bash
   sudo nano 00-installer-config.yaml
   ```

3. Thêm tuyến đường tĩnh vào phần cấu hình mạng dưới giao diện bạn đang sử dụng. Ví dụ:
   ```yaml
   network:
     version: 2
     renderer: networkd
     ethernets:
       ens33:
         dhcp4: true
         routes:
           - to: 192.168.2.0/24
             via: 192.168.1.1
   ```

   - `ens33`: Tên giao diện mạng bạn sử dụng.
   - `routes`: Phần này định nghĩa các tuyến đường tĩnh. Bạn có thể thêm nhiều tuyến đường nếu cần.

4. Lưu file và thoát trình soạn thảo.

5. Áp dụng cấu hình mới:
   ```bash
   sudo netplan apply
   ```

#### **Trên Ubuntu 16.04 và các bản cũ hơn (sử dụng `/etc/network/interfaces`)**

1. Mở file `/etc/network/interfaces` để chỉnh sửa:
   ```bash
   sudo nano /etc/network/interfaces
   ```

2. Thêm cấu hình cho mạng và tuyến đường tĩnh, ví dụ:
   ```bash
   iface ens33 inet static
       address 192.168.1.2
       netmask 255.255.255.0
       gateway 192.168.1.1
       up ip route add 192.168.2.0/24 via 192.168.1.1
   ```

   - `up ip route add ...` sẽ thêm tuyến đường tĩnh mỗi khi giao diện `ens33` được kích hoạt.

3. Lưu và đóng file.

4. Khởi động lại dịch vụ mạng:
   ```bash
   sudo systemctl restart networking
   ```

---

### **4. Kiểm Tra Định Tuyến Tĩnh Sau Khi Khởi Động**

Sau khi cấu hình vĩnh cửu, bạn có thể kiểm tra bảng định tuyến sau khi khởi động lại máy ảo bằng lệnh:
```bash
ip route show
```
Hoặc:
```bash
netstat -rn
```

Các tuyến đường tĩnh mà bạn đã cấu hình sẽ được hiển thị trong bảng định tuyến.

---

### **Tóm Tắt**

1. **Kiểm tra giao diện mạng**: Sử dụng `ip addr` hoặc `ifconfig` để xác định tên giao diện mạng trên máy ảo Ubuntu.
2. **Cấu hình tạm thời**: Dùng lệnh `ip route add` để thêm tuyến đường tĩnh.
3. **Cấu hình vĩnh cửu**:
   - **Ubuntu 18.04+**: Sử dụng `netplan` để cấu hình.
   - **Ubuntu 16.04 và các phiên bản cũ**: Sử dụng file `/etc/network/interfaces`.
4. **Kiểm tra định tuyến**: Sử dụng lệnh `ip route show` hoặc `netstat -rn` để kiểm tra bảng định tuyến.

Hy vọng hướng dẫn này giúp bạn cấu hình định tuyến tĩnh trên máy ảo Ubuntu trong VMware thành công!
