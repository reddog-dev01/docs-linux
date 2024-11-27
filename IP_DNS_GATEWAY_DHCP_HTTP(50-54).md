### **1. Set static IP, DNS, GATEWAY**

**1.1 Các khái niệm**

**a. DHCP**

- DHCP (Dynamic Host Configuration Protocol) là một giao thức mạng tự động gán thông tin cấu hình IP cho các thiết bị trên mạng. VD: mạng gia đình là router đóng vai trò như máy chủ DHCP, doanh nghiệp là DHCP chuyên dụng (Windows Server hoặc Linux)
- hoạt động theo mô hình máy chủ - khách (Server-Client). Khi một thiết bị kết nối vào mạng, nó sẽ yêu cầu một địa chỉ IP và các thông tin cấu hình mạng từ máy chủ DHCP

**b. IP động**

- địa chỉ IP được gán tự động cho thiết bị bởi một máy chủ DHCP

**c. IP tĩnh**

địa chỉ IP được gán cố định cho một thiết bị trong mạng. Không giống như IP động, địa chỉ này không thay đổi trừ khi bạn tự thay đổi nó theo cách thủ công hoặc thông qua cấu hình của quản trị viên mạng.

**1.2 Cấu hình ip động**

**network**:
   - Đây là phần chứa cấu hình mạng chính cho hệ thống. Tất cả các thông số mạng đều được định nghĩa dưới mục này.

**version**:
   - **Ý nghĩa**: Chỉ ra phiên bản của cấu hình `netplan` đang sử dụng. Ví dụ:
     - `version: 2` là phiên bản hiện tại của cấu hình mạng.
   
   **Cấu hình mẫu**:
   ```yaml
   version: 2
   ```

**renderer**:
   - **Ý nghĩa**: Chỉ định công cụ hoặc trình điều khiển sử dụng để quản lý cấu hình mạng. Có hai renderer phổ biến:
     - **networkd**: Dùng `systemd-networkd`, thường được sử dụng trong các máy chủ hoặc hệ thống không có giao diện đồ họa.
     - **NetworkManager**: Dùng cho các hệ thống desktop, có giao diện đồ họa và hỗ trợ quản lý kết nối mạng dễ dàng hơn.

   **Cấu hình mẫu**:
   ```yaml
   renderer: networkd  # Hoặc networkmanager
   ```

**ethernets**:
   - **Ý nghĩa**: Đây là mục cấu hình dành cho các kết nối mạng Ethernet (mạng có dây). Bạn sẽ cấu hình các card mạng trong mục này.
   - **ethernets** chứa tên các thiết bị mạng và các thiết lập mạng liên quan như IP, gateway, DNS, v.v.

   **Cấu hình mẫu**:
   ```yaml
   ethernets:
     enp3s0:  # Tên card mạng, thay thế theo tên thiết bị mạng của bạn
       dhcp4: true  # Sử dụng DHCP để nhận địa chỉ IPv4 tự động
   ```

**dhcp4**:
   - **Ý nghĩa**: Chỉ định việc sử dụng DHCP (Dynamic Host Configuration Protocol) cho địa chỉ IPv4. Nếu đặt `dhcp4: true`, hệ thống sẽ tự động nhận địa chỉ IP từ máy chủ DHCP.
   - **Giá trị**:
     - `true`: Kích hoạt DHCP cho IPv4.
     - `false`: Tắt DHCP cho IPv4 (nếu bạn muốn cấu hình địa chỉ IP tĩnh).
   
   **Cấu hình mẫu**:
   ```yaml
   dhcp4: true
   ```
**dhcp6**:
   - **Ý nghĩa**: Chỉ định việc sử dụng DHCP cho IPv6. Giống như `dhcp4`, nếu đặt `dhcp6: true`, hệ thống sẽ tự động nhận địa chỉ IP từ máy chủ DHCP hỗ trợ IPv6.
   - **Giá trị**:
     - `true`: Kích hoạt DHCP cho IPv6.
     - `false`: Tắt DHCP cho IPv6.
   
   **Cấu hình mẫu**:
   ```yaml
   dhcp6: true
   ```

**nameservers**:
   - **Ý nghĩa**: Cấu hình DNS (Domain Name System) để hệ thống có thể giải quyết tên miền (ví dụ: `google.com`).
   - **Giá trị**: Danh sách các địa chỉ IP của máy chủ DNS (có thể là DNS của ISP, hoặc công cộng như Google DNS, Cloudflare DNS).
   
   **Cấu hình mẫu**:
   ```yaml
   nameservers:
     addresses:
       - 8.8.8.8      # DNS của Google
       - 8.8.4.4      # DNS dự phòng của Google
   ```

**gateway4**:
   - **Ý nghĩa**: Chỉ định địa chỉ của cổng mặc định (gateway) cho IPv4. Đây là địa chỉ IP của router hoặc gateway mà hệ thống sẽ sử dụng để kết nối ra ngoài mạng.
   - **Giá trị**: Địa chỉ IP của cổng mặc định.
   
   **Cấu hình mẫu**:
   ```yaml
   gateway4: 192.168.1.1
   ```

**routes**:
   - **Ý nghĩa**: Cấu hình các tuyến đường mạng tĩnh cho hệ thống.
   - **Giá trị**: Địa chỉ mạng đích và địa chỉ gateway để định tuyến.
   
   **Cấu hình mẫu**:
   ```yaml
   routes:
     - to: 0.0.0.0/0        # Địa chỉ mạng đích
       via: 192.168.1.1     # Gateway để đi qua
   ```

**mtu**:
   - **Ý nghĩa**: Maximum Transmission Unit (MTU) là kích thước tối đa của một gói dữ liệu mà giao thức mạng có thể truyền đi. Cấu hình này có thể thay đổi tùy theo yêu cầu của mạng (đối với các mạng cần tối ưu hóa hiệu suất).
   - **Giá trị**: Kích thước MTU tính bằng byte (ví dụ: `1500`).
   
   **Cấu hình mẫu**:
   ```yaml
   mtu: 1500
   ```

1. Kiểm tra tên interface mạng
```
ip link
```
2. Kiểm tra quyền file xem được truy cập hay không
```
ls -l /etc/netplan/
```
3. Sửa file cấu hình
```
sudo vim /etc/netplan/01-netcfg.yaml
```
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: true
```

cấu hình đầy đủ
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
4. Áp dụng cấu hình
```
sudo netplan apply
```
5. Kiểm tra IP được cấp và ping kết nối
```
ip addr show ens33
```

**1.3 Cấu hình IP tĩnh**
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
**1.4 Khi nào cấu hình IP động, khi nào cấu hình IP tĩnh**

**a. Khi nào cấu hình IP động**

-

### **2. DNS System**

- DNS là một hệ thống phân dải giúp chuyển đổi tên miền (domain name) thành địa chỉ IP (IP address) và ngược lại.

**2.1 Các khái niệm và cơ chế hoạt động của DNS**

**a. Tên miền (Domain name)**

- Là tên được dùng để định dạng các tài nguyên trên internet

**Cấu trúc phân cấp:**
- Root Domain: Là cấp cao nhất, biểu thị bằng dấu chấm (`.`)
- Top-Level Domain (TLD): Phân chia theo loại (.com, .org, .vn) hoặc quốc gia (.uk, .jp).
- Second-Level Domain (SLD): Phần tên cụ thể, ví dụ: `google` trong `google.com`.
- Subdomain: Tên miền con, ví dụ: www trong `www.google.com`.

**b. Địa chỉ IP**

- Dùng để định danh thiết bị hoặc máy chủ trên Internet.
- IPv4: 32-bit, dạng `192.168.1.1`
- IPv6: 128-bit, dạng `2001:0db8::1`

**c. Máy chủ DNS(DNS Server)**

Lưu trữ thông tin ánh xạ giữa tên miền và địa chỉ IP.

Các loại máy chủ:

- Recursive Resolver: Máy chủ trung gian xử lý các yêu cầu từ người dùng.
- Root Server: Máy chủ gốc, quản lý thông tin cấp cao nhất.
- TLD Server: Quản lý thông tin tên miền cấp cao như `.com`, `.vn`.
- Authoritative Server: Máy chủ ủy quyền chứa thông tin chính xác về tên miền.

**d. Bản ghi DNS (DNS Records):**

Các loại thông tin ánh xạ trong DNS:

- A Record: Tên miền → IPv4.
- AAAA Record: Tên miền → IPv6.
- CNAME Record: Alias tên miền, chuyển hướng từ tên này sang tên khác.
- MX Record: Máy chủ email.
- TXT Record: Chứa dữ liệu văn bản, dùng để xác thực bảo mật (SPF, DKIM).

**2.2 Cơ chế hoạt động của hệ thống DNS**

Khi người dùng nhập một tên miền vào trình duyệt, DNS sẽ phân giải thành địa chỉ IP qua các bước sau:

1. Người dùng gửi yêu cầu phân giải DNS:

Trình duyệt gửi yêu cầu phân giải tên miền (DNS query) đến máy chủ DNS cục bộ (thường là của ISP).

2. Máy chủ DNS cục bộ kiểm tra cache:

Nếu kết quả phân giải đã được lưu trữ trong bộ nhớ cache, máy chủ trả lại ngay địa chỉ IP.

Nếu không có, yêu cầu sẽ được gửi tiếp đến hệ thống DNS để phân giải.

3. Truy vấn đến Root Server:

Máy chủ DNS cục bộ gửi yêu cầu đến Root Server.

Root Server không lưu địa chỉ IP chính xác nhưng trả về địa chỉ của máy chủ TLD Server phù hợp (ví dụ .com).

4. Truy vấn đến TLD Server:

Máy chủ TLD trả về địa chỉ của Authoritative Server cho tên miền cụ thể.

5. Truy vấn đến Authoritative Server:

Máy chủ ủy quyền trả về địa chỉ IP chính xác của tên miền.

6. Trả kết quả về trình duyệt:

Địa chỉ IP được gửi ngược về trình duyệt.

Trình duyệt sử dụng địa chỉ IP này để kết nối đến máy chủ đích. 

**2.3 Các loại máy chủ DNS, các loại query DNS**

**2.3.1 Các loại máy chủ DNS**

**a. Recursive Resolver (Máy chủ phân giải đệ quy):**

Là máy chủ DNS cục bộ, thường thuộc ISP hoặc nhà cung cấp dịch vụ DNS (như Google DNS, Cloudflare DNS).

Chức năng:

Nhận yêu cầu từ người dùng và tìm kiếm địa chỉ IP tương ứng thông qua các máy chủ DNS khác.

Kiểm tra cache và trả lời nhanh nếu thông tin đã có sẵn.

Ví dụ: 8.8.8.8 (Google Public DNS).

**b. Root Server (Máy chủ gốc):**

Điểm bắt đầu của hệ thống DNS, quản lý thông tin phân cấp các miền TLD (Top-Level Domain).

Chức năng:

Hướng dẫn Recursive Resolver đến máy chủ TLD Server phù hợp.

Số lượng: 13 cụm máy chủ Root Server (được nhân bản trên toàn cầu).

**c. TLD Server (Máy chủ miền cấp cao nhất):**

Quản lý thông tin về các miền cấp cao (TLD), ví dụ .com, .org, .vn.

Chức năng:

Trả về địa chỉ của Authoritative Server quản lý tên miền cụ thể.

Ví dụ:

Máy chủ quản lý .com: Verisign.

Máy chủ quản lý .vn: VNNIC.

**d. Authoritative Server (Máy chủ ủy quyền):**

Lưu trữ thông tin chính xác nhất về tên miền.

Chức năng:

Trả lời cuối cùng cho các truy vấn DNS với địa chỉ IP của tài nguyên mạng.

Ví dụ:

Tên miền example.com được quản lý bởi một máy chủ DNS cụ thể (của nhà cung cấp hosting hoặc tổ chức sở hữu tên miền).

**2.3.2 Các loại Query DNS**

**1. Recursive Query (Truy vấn đệ quy):**

Người dùng (client) yêu cầu máy chủ DNS cục bộ tìm kiếm và trả về kết quả cuối cùng.

Cách hoạt động:

Máy chủ DNS phải tự tìm kiếm thông qua các máy chủ khác (Root Server, TLD Server, Authoritative Server).

Nếu không tìm thấy kết quả, máy chủ trả về lỗi.

Ví dụ: Người dùng truy cập www.example.com, Recursive Resolver trả về địa chỉ IP cuối cùng hoặc lỗi.

**2. Iterative Query (Truy vấn lặp):**

Máy chủ DNS chỉ trả về thông tin gần đúng nhất hoặc chỉ dẫn (hướng đến máy chủ khác).

Cách hoạt động:

Máy chủ DNS không tìm kiếm toàn bộ chuỗi; thay vào đó, nó trả về địa chỉ máy chủ kế tiếp mà client cần truy vấn.

Ví dụ: Recursive Resolver hỏi Root Server, Root Server chỉ dẫn đến TLD Server.

**3. Reverse Query (Truy vấn ngược):**

Dùng để ánh xạ địa chỉ IP thành tên miền (ngược lại với truy vấn thông thường).

Cách hoạt động:

Truy vấn sử dụng PTR Record trong DNS.

Ví dụ:

Địa chỉ IP: 192.168.1.1.

Kết quả: example.com.

**2.4 các loại DNS bản ghi DNS thường sử dụng**

- Lưu trữ thông tin ánh xạ giữa tên miền và tài nguyên mạng

1. A Record (Address Record)

Ánh xạ tên miền thành địa chỉ IPv4.

Ứng dụng: Dùng để truy cập website hoặc dịch vụ qua tên miền.

Ví dụ:

Tên miền: example.com

Địa chỉ IPv4: 192.168.1.1

2. AAAA Record (IPv6 Address Record)

Ánh xạ tên miền thành địa chỉ IPv6.

Ứng dụng: Dùng cho các mạng hỗ trợ IPv6.

Ví dụ:

Tên miền: example.com

Địa chỉ IPv6: 2001:0db8:85a3:0000:0000:8a2e:0370:7334

3. CNAME Record (Canonical Name Record)

Tạo bí danh (alias) cho một tên miền khác.

Ứng dụng: Dùng để chuyển hướng truy cập từ một tên miền sang tên miền khác.

Ví dụ:

Alias: www.example.com

Tên chính: example.com

4. MX Record (Mail Exchange Record)

Xác định máy chủ email chịu trách nhiệm xử lý thư điện tử cho tên miền.

Ứng dụng: Cấu hình email hosting.

Ví dụ:

Tên miền: example.com

Máy chủ email: mail.example.com, độ ưu tiên: 10

5. NS Record (Name Server Record)

Xác định các máy chủ DNS chịu trách nhiệm phân giải tên miền.

Ứng dụng: Cấu hình tên miền với máy chủ DNS phù hợp.

Ví dụ:

Tên miền: example.com

Máy chủ DNS: ns1.example.com, ns2.example.com

6. SOA Record (Start of Authority Record)

Chứa thông tin quản trị của tên miền, như máy chủ DNS chính, email quản trị, thời gian làm mới bản ghi.

Ứng dụng: Quản lý vùng DNS (DNS zone).

Ví dụ:

Máy chủ chính: ns1.example.com

Email quản trị: admin@example.com

7. TXT Record (Text Record)

Lưu trữ dữ liệu văn bản tùy chỉnh. Thường dùng cho xác thực và bảo mật.

Ứng dụng:

Xác thực email (SPF, DKIM, DMARC).

Xác minh tên miền với dịch vụ bên thứ ba (Google, AWS).

Ví dụ:

SPF: v=spf1 include:_spf.example.com ~all

8. PTR Record (Pointer Record)

Ánh xạ địa chỉ IP thành tên miền (truy vấn ngược).

Ứng dụng: Dùng trong kiểm tra xác thực IP gửi email (Reverse DNS Lookup).

Ví dụ:

IP: 192.168.1.1

Tên miền: example.com

9. SRV Record (Service Record)

Chỉ định thông tin về các dịch vụ mạng cụ thể.

Ứng dụng: Cấu hình VoIP, XMPP, hoặc các dịch vụ khác.

Ví dụ:

Dịch vụ: _sip._tcp.example.com

Máy chủ: sipserver.example.com, cổng: 5060

10. CAA Record (Certification Authority Authorization Record)

Xác định tổ chức nào được phép cấp chứng chỉ SSL cho tên miền.

Ứng dụng: Bảo vệ tên miền khỏi chứng chỉ không hợp lệ.

Ví dụ:

Tên miền: example.com

CA được phép: letsencrypt.org

11. HINFO Record (Host Information Record)

Lưu trữ thông tin về phần cứng và hệ điều hành của máy chủ.

Ứng dụng: Cung cấp thông tin mô tả máy chủ (ít dùng).

Ví dụ:

CPU: Intel i7

Hệ điều hành: Ubuntu

12. DS Record (Delegation Signer Record)

Lưu chữ ký số dùng trong DNSSEC (DNS Security Extensions).

Ứng dụng: Đảm bảo tính toàn vẹn và xác thực của dữ liệu DNS.

Ví dụ:

Tên miền: example.com

Chữ ký: 12345abcde...

**2.5 Cách tìm IP domain**
```
nslookup example.com
```
```
dig example.com
```
```
host example.com
```
```ping -c 1 example.com```
```curl -s https://api64.ipify.org?domain=example.com```
