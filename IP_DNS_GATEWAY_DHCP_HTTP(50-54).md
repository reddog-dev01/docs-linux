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
### **1.4 Khi nào cấu hình IP động, khi nào cấu hình IP tĩnh**

### a. **Khi nào cấu hình IP động (DHCP)?**
IP động được cấp phát tự động bởi **DHCP server** mỗi khi thiết bị kết nối mạng. Điều này rất tiện lợi và phổ biến trong nhiều tình huống, đặc biệt là trong các mạng không yêu cầu địa chỉ IP cố định.

#### Sử dụng IP động khi:
- **Mạng nhỏ hoặc môi trường thay đổi thường xuyên**: Nếu bạn có một mạng trong nhà, văn phòng nhỏ, hoặc môi trường mà các thiết bị thường xuyên kết nối và rời đi (ví dụ: laptop, điện thoại), thì việc sử dụng DHCP sẽ rất thuận tiện. DHCP sẽ tự động cấp phát IP cho các thiết bị mà không cần cấu hình thủ công.
  
- **Sử dụng cho các thiết bị không yêu cầu IP cố định**: Nếu các thiết bị như điện thoại, laptop, hoặc máy tính bảng không cần kết nối cố định với các thiết bị khác trong mạng (như máy in hoặc máy chủ), IP động là lựa chọn hợp lý. Mỗi lần thiết bị kết nối lại với mạng, một địa chỉ IP mới sẽ được cấp phát.

- **Mạng với số lượng thiết bị thay đổi thường xuyên**: Trong các văn phòng lớn hoặc nhà với nhiều thiết bị di động, bạn sẽ không muốn phải quản lý thủ công từng địa chỉ IP cho từng thiết bị. DHCP sẽ giúp bạn tự động cấp phát IP mà không cần phải lo lắng về việc phân bổ và quản lý địa chỉ IP.

- **Tiết kiệm thời gian và công sức**: Với DHCP, bạn không cần phải thủ công cấu hình IP cho mỗi thiết bị. Đây là lựa chọn lý tưởng khi bạn không có yêu cầu đặc biệt về việc gắn địa chỉ IP cố định cho các thiết bị.

### b. **Khi nào cấu hình IP tĩnh?**
IP tĩnh là một địa chỉ IP được chỉ định cố định cho một thiết bị cụ thể và không thay đổi trừ khi bạn thay đổi cấu hình. Việc cấu hình IP tĩnh thường được sử dụng cho các thiết bị cần một địa chỉ IP cố định để các thiết bị khác có thể kết nối ổn định.

#### Sử dụng IP tĩnh khi:
- **Cần kết nối ổn định hoặc liên tục**: Nếu bạn đang chạy các dịch vụ cần các thiết bị khác kết nối với chúng qua một địa chỉ IP cố định (ví dụ: máy chủ web, máy chủ DNS, máy chủ cơ sở dữ liệu), bạn nên sử dụng IP tĩnh. Điều này đảm bảo rằng các thiết bị khác luôn có thể tìm thấy và kết nối với các dịch vụ của bạn mà không bị gián đoạn vì sự thay đổi IP.

- **Chạy dịch vụ mạng như máy chủ**: Các thiết bị như máy chủ, máy in mạng, hoặc thiết bị lưu trữ NAS cần có một địa chỉ IP cố định để các thiết bị khác trong mạng có thể kết nối ổn định. Ví dụ, nếu bạn muốn mọi người trong công ty truy cập vào một máy chủ web hoặc cơ sở dữ liệu, việc có một IP tĩnh là cần thiết.

- **Cấu hình mạng trong các doanh nghiệp lớn hoặc mạng phức tạp**: Nếu bạn quản lý một mạng phức tạp trong môi trường doanh nghiệp hoặc trường học, việc sử dụng IP tĩnh giúp bạn dễ dàng quản lý và theo dõi các thiết bị trong mạng. Các thiết bị như máy tính bàn, máy chủ, hoặc thiết bị giám sát có thể yêu cầu IP tĩnh để đảm bảo tính ổn định và kiểm soát.

- **Cần cấu hình cổng chuyển tiếp (Port Forwarding)**: Nếu bạn cần mở các cổng trên router để cho phép các kết nối đến máy tính hoặc thiết bị từ bên ngoài (ví dụ: chơi game, truy cập vào các dịch vụ từ xa), IP tĩnh là rất quan trọng. Bởi vì khi sử dụng IP động, cổng chuyển tiếp có thể không hoạt động đúng nếu IP của thiết bị thay đổi.

- **Tránh xung đột IP**: Khi cấu hình IP tĩnh, bạn có thể tránh được tình trạng xung đột địa chỉ IP trong mạng. DHCP có thể cấp phát lại các IP đã được sử dụng trước đó, gây ra sự cố khi các thiết bị kết nối cùng một IP. Với IP tĩnh, bạn có thể đảm bảo rằng mỗi thiết bị sẽ có một địa chỉ IP duy nhất trong mạng.

### c. **So Sánh giữa IP động và IP tĩnh**

| **Yếu tố**                | **IP động (DHCP)**                | **IP tĩnh**                       |
|---------------------------|-----------------------------------|-----------------------------------|
| **Cấu hình**               | Tự động cấp phát qua DHCP         | Cấu hình thủ công                 |
| **Thích hợp cho**          | Mạng nhỏ, thiết bị di động, mạng không yêu cầu IP cố định | Máy chủ, thiết bị cần kết nối ổn định |
| **Độ thay đổi**            | Địa chỉ IP có thể thay đổi khi kết nối lại | Địa chỉ IP không thay đổi         |
| **Dễ quản lý**             | Dễ dàng, không cần quản lý IP thủ công | Phải quản lý và theo dõi thủ công |
| **Tính ổn định**           | Ít ổn định đối với các thiết bị cần kết nối lâu dài | Ổn định và đáng tin cậy cho các thiết bị cần IP cố định |



--------------------------------------------------------
--------------------------------------------------------



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
```
ping -c 1 example.com
```
```
curl -s https://api64.ipify.org?domain=example.com
```

----------------------------------------------

### **3. GATEWAY**

- Gateway (cổng mạng) là một thiết bị mạng hoặc phần mềm được sử dụng để kết nối hai mạng khác nhau, hoặc một mạng nội bộ và mạng bên ngoài (ví dụ: Internet). Gateway hoạt động như một "cổng" cho phép các thiết bị trong mạng của bạn giao tiếp với các thiết bị trong mạng khác. Nó cũng có thể thực hiện các chức năng như định tuyến, chuyển tiếp gói tin và dịch địa chỉ IP giữa các mạng khác nhau.

**Gateway** (Cổng mạng) có một số chức năng quan trọng trong việc kết nối các mạng khác nhau. Dưới đây là các chức năng chính của một gateway:


### **Chức năng của Gateway**


#### 1. **Kết nối các mạng khác nhau**
- **Gateway** giúp kết nối hai mạng khác nhau, có thể là mạng nội bộ (LAN) và mạng ngoài (Internet) hoặc giữa các mạng sử dụng các giao thức khác nhau. Nó hoạt động như một "cổng" giữa các mạng này, giúp dữ liệu di chuyển từ mạng này sang mạng khác.

#### 2. **Định tuyến gói tin**
- **Định tuyến (Routing)** là một trong những chức năng chính của gateway. Gateway quyết định **đường đi** của các gói dữ liệu khi chúng rời mạng nội bộ và đi ra ngoài (hoặc ngược lại). Khi thiết bị trong mạng nội bộ muốn truy cập vào tài nguyên bên ngoài mạng, nó sẽ gửi yêu cầu tới gateway, và gateway sẽ định tuyến yêu cầu này tới đích đúng.

#### 3. **Dịch và chuyển đổi giao thức**
- Gateway có thể chuyển đổi **giao thức mạng** giữa các mạng sử dụng các giao thức khác nhau. Ví dụ, nếu một mạng sử dụng giao thức IPv4 và một mạng khác sử dụng IPv6, gateway có thể chuyển đổi giữa các giao thức này.
- Ngoài ra, gateway có thể chuyển đổi giữa các giao thức truyền thông khác nhau như **TCP/IP**, **DECnet**, **IPX**, **AppleTalk**, v.v., cho phép các thiết bị từ các mạng khác nhau giao tiếp với nhau.

#### 4. **Chuyển tiếp dữ liệu**
- **Gateway** chuyển tiếp các gói dữ liệu từ một mạng vào một mạng khác, giúp các thiết bị trong mạng nội bộ (LAN) giao tiếp với các thiết bị ngoài mạng (ví dụ: Internet).
- Khi bạn truy cập một trang web, các gói dữ liệu từ máy tính của bạn sẽ được gửi tới gateway, gateway sẽ chuyển tiếp chúng ra ngoài Internet và nhận phản hồi về lại mạng nội bộ của bạn.

#### 5. **Chức năng bảo mật**
- **Firewall (Tường lửa)**: Gateway có thể được cấu hình để kiểm tra và bảo vệ mạng khỏi các mối đe dọa từ bên ngoài. Tường lửa có thể lọc các gói dữ liệu vào và ra khỏi mạng dựa trên các quy tắc bảo mật.
- **Mã hóa**: Gateway có thể mã hóa và giải mã các gói dữ liệu để đảm bảo an toàn khi truyền qua các mạng không an toàn (như Internet).

#### 6. **Chuyển đổi địa chỉ mạng (NAT)**
- **NAT (Network Address Translation)**: Một chức năng phổ biến của gateway là thực hiện NAT, tức là chuyển đổi địa chỉ IP của các thiết bị trong mạng nội bộ thành một địa chỉ IP công cộng khi truy cập Internet, và ngược lại. Điều này giúp tiết kiệm địa chỉ IP và bảo mật mạng nội bộ.
  - Ví dụ: Các thiết bị trong mạng LAN có thể có địa chỉ IP riêng tư như `192.168.1.x`, và khi các thiết bị này truy cập Internet, gateway sẽ thay đổi địa chỉ IP thành địa chỉ công cộng của router (ví dụ: `203.0.113.x`).

#### 7. **Chức năng DHCP (Dynamic Host Configuration Protocol)**
- **DHCP**: Gateway có thể hoạt động như một **DHCP server**, cấp phát địa chỉ IP động cho các thiết bị trong mạng nội bộ. Thay vì phải cấu hình thủ công mỗi địa chỉ IP cho từng thiết bị, gateway sẽ tự động cấp phát địa chỉ IP cho các thiết bị khi chúng kết nối vào mạng.

#### 8. **Chức năng VPN (Virtual Private Network)**
- **VPN Gateway**: Gateway có thể hỗ trợ kết nối VPN, cho phép các thiết bị trong mạng nội bộ kết nối với mạng bên ngoài một cách an toàn qua một kênh mã hóa. Ví dụ, nhân viên làm việc từ xa có thể kết nối với mạng công ty thông qua VPN để truy cập các tài nguyên nội bộ.

#### 9. **Quản lý lưu lượng (Traffic Management)**
- **QoS (Quality of Service)**: Một số gateway cung cấp tính năng QoS để quản lý băng thông và đảm bảo các ứng dụng quan trọng (như video call, game trực tuyến) có đủ băng thông, giúp tối ưu hóa hiệu suất mạng.

#### 10. **Chuyển tiếp dự phòng và Load Balancing**
- **Load Balancing**: Trong các mạng phức tạp, gateway có thể thực hiện cân bằng tải (load balancing), giúp phân phối đều lưu lượng mạng tới các đường truyền khác nhau, tối ưu hóa hiệu suất và đảm bảo tính sẵn sàng cao.
- **High Availability**: Gateway có thể cấu hình để đảm bảo tính sẵn sàng cao, nghĩa là khi một gateway gặp sự cố, các gateway dự phòng sẽ tự động thay thế để duy trì kết nối mạng liên tục.


