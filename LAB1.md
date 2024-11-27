### **Máy 1: Cài đặt và cấu hình DNS server**

1. **Cài đặt DNS server (Bind9 hoặc tương đương)**:
   - Với hệ điều hành Linux (Ubuntu/Debian):
     ```bash
     sudo apt update
     sudo apt install bind9 -y
     ```

2. **Cấu hình file zone cho domain `toilamlab.com`**:
   - Mở file cấu hình DNS:
     ```bash
     sudo nano /etc/bind/named.conf.local
     ```
   - Thêm cấu hình zone:
     ```conf
     zone "toilamlab.com" {
         type master;
         file "/etc/bind/zones/db.toilamlab.com";
     };
     ```
   - Tạo thư mục lưu file zone:
     ```bash
     sudo mkdir -p /etc/bind/zones
     ```

3. **Tạo file zone `db.toilamlab.com`**:
   ```bash
   sudo nano /etc/bind/zones/db.toilamlab.com
   ```
   - Nội dung file zone:
     ```
     $TTL 86400
     @   IN  SOA ns1.toilamlab.com. admin.toilamlab.com. (
             2024112701 ; Serial
             3600       ; Refresh
             1800       ; Retry
             604800     ; Expire
             86400      ; Minimum TTL
         )
     @   IN  NS  ns1.toilamlab.com.
     ns1 IN  A   103.45.89.45
     @   IN  A   103.45.89.45
     ```
   - Lưu và đóng file.

4. **Kiểm tra cấu hình và khởi động lại dịch vụ**:
   - Kiểm tra cấu hình:
     ```bash
     sudo named-checkconf
     sudo named-checkzone toilamlab.com /etc/bind/zones/db.toilamlab.com
     ```
   - Khởi động lại Bind9:
     ```bash
     sudo systemctl restart bind9
     ```

---

### **Máy 2: Kiểm tra trước khi trỏ DNS server**
1. **Kiểm tra IP domain `toilamlab.com`**:
   - Sử dụng lệnh `dig` hoặc `nslookup`:
     ```bash
     dig toilamlab.com
     ```
     Hoặc:
     ```bash
     nslookup toilamlab.com
     ```
   - Nếu chưa cấu hình trỏ về máy 1, kết quả sẽ không có địa chỉ IP.

---

### **Máy 2: Cấu hình DNS server trỏ về máy 1**

1. **Chỉnh sửa file cấu hình DNS trên máy 2**:
   - Mở file cấu hình DNS (`resolv.conf`):
     ```bash
     sudo nano /etc/resolv.conf
     ```
   - Thêm địa chỉ IP của máy 1 (giả sử máy 1 có IP là `192.168.1.100`):
     ```
     nameserver 192.168.1.100
     ```
   - Lưu và đóng file.

2. **Kiểm tra lại IP domain `toilamlab.com`**:
   - Sử dụng `dig` hoặc `nslookup`:
     ```bash
     dig toilamlab.com
     ```
     Hoặc:
     ```bash
     nslookup toilamlab.com
     ```
   ![image](https://github.com/user-attachments/assets/6d285748-4906-4d26-8e2e-99562b243f61)

- DNS sử dụng port 53 (cổng mặc định cho DNS, đây là 1 phần trong quy chuẩn của giao thức internet). Sử dụng cho tất cả các truy vấn DNS giữa các máy. Khi máy 2 gửi y/c đến máy 1 để lấy thông tin DNS, máy 1 sẽ trả về thông qua port 53
- UDP port 53 sẽ được sử dụng chủ yếu khi gửi các truy vấn DNS đơn giản
- TCP port 53 sẽ được sử dụng nếu có yêu cầu transfer dữ liệu zone hoặc nếu yêu cầu DNS quá lớn không thể trả lời qua UDP

**Quá trình phân giải domain**

B1: Trình duyệt gửi yêu cầu DNS
- Khi nhập 1 tên miền vào trình duyệt web (VDL toilamlab.com) trình duyệt sẽ kiểm tra xem DNS cache của hệ thống có lưu sẵn địa chỉ IP của 

---
