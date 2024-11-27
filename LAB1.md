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

Bước 1: Trình duyệt gửi yêu cầu DNS

Khi bạn nhập một tên miền vào trình duyệt web (ví dụ: toilamlab.com), trình duyệt sẽ kiểm tra xem DNS cache của hệ thống có lưu sẵn địa chỉ IP của tên miền đó không.

Nếu địa chỉ IP đã được lưu trong cache (ví dụ, từ lần truy cập trước), trình duyệt sẽ sử dụng ngay địa chỉ đó mà không cần thực hiện truy vấn DNS lại.

Bước 2: Kiểm tra cache DNS của hệ thống

Nếu địa chỉ IP không có trong cache DNS local của hệ thống (ví dụ: trên máy tính của bạn), hệ thống sẽ tiếp tục gửi yêu cầu tới DNS resolver (có thể là DNS server của ISP hoặc DNS server công cộng như Google DNS, Cloudflare, v.v.).

Bước 3: DNS resolver gửi yêu cầu tới root DNS server

DNS resolver (hay còn gọi là DNS resolver recursive) sẽ gửi yêu cầu DNS đến một trong các root DNS server. Các root DNS server này quản lý thông tin về các top-level domain (TLD), như .com, .org, .net, v.v.

Root DNS server không lưu thông tin về tên miền cụ thể mà chỉ biết về các TLD name servers (ví dụ: .com).

Bước 4: TLD DNS server trả về Name Servers của domain

Root DNS server sẽ trả về địa chỉ của TLD DNS server tương ứng với tên miền yêu cầu. Ví dụ, nếu bạn yêu cầu phân giải toilamlab.com, root DNS server sẽ chuyển hướng yêu cầu đến .com TLD DNS server.

TLD DNS server chứa thông tin về các DNS server của các domain cụ thể (ví dụ: thông tin về DNS của toilamlab.com).

Bước 5: Truy vấn đến Authoritative DNS Server

Sau khi nhận được thông tin từ TLD DNS server, DNS resolver sẽ tiếp tục gửi yêu cầu đến authoritative DNS server của domain, nơi chứa bản ghi DNS chính thức cho tên miền đó.

Authoritative DNS server có thể là DNS server do chủ sở hữu domain tự quản lý hoặc dịch vụ DNS của nhà cung cấp tên miền.

Bước 6: Phản hồi từ Authoritative DNS Server

Authoritative DNS server sẽ trả về bản ghi DNS (thường là bản ghi A đối với địa chỉ IP) cho tên miền yêu cầu. Ví dụ, toilamlab.com có thể có bản ghi A trỏ đến 103.45.89.45.

Nếu tên miền yêu cầu có các bản ghi khác như MX (Mail Exchange), CNAME (Canonical Name), thì các bản ghi này cũng sẽ được trả về nếu có.

Bước 7: Cập nhật cache DNS của resolver và hệ thống

DNS resolver sẽ lưu trữ kết quả này vào DNS cache để sử dụng cho các truy vấn sau này trong một khoảng thời gian nhất định (TTL - Time to Live).

Sau đó, kết quả sẽ được gửi lại đến hệ thống của người dùng, và trình duyệt sẽ sử dụng địa chỉ IP này để kết nối đến server ứng với tên miền.

Bước 8: Trình duyệt kết nối đến máy chủ

Sau khi có địa chỉ IP, trình duyệt sử dụng nó để kết nối đến máy chủ của website, gửi yêu cầu HTTP/HTTPS, và hiển thị nội dung của website trên trình duyệt.

Tóm tắt quy trình phân giải domain

Người dùng nhập tên miền vào trình duyệt.

Hệ thống kiểm tra cache DNS cục bộ.

Nếu không có trong cache, yêu cầu được 

---
