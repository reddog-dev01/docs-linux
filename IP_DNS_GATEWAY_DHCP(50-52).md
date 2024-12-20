### **Subnet Mask**

**Subnet Mask** là một chuỗi số được sử dụng trong các mạng IP để xác định phạm vi của mạng con và giúp phân biệt giữa phần **Network (mạng)** và phần **Host (thiết bị)** của một địa chỉ IP. Subnet mask có vai trò quan trọng trong việc xác định có bao nhiêu thiết bị có thể tồn tại trong một mạng con và cách mà các địa chỉ IP được phân chia.

#### Cấu trúc của Subnet Mask

Một **Subnet Mask** có cùng độ dài với một **địa chỉ IP** (32 bit đối với IPv4), và nó gồm hai phần:

1. **Phần mạng (Network)**: Các bit `1` trong subnet mask xác định phần mạng, tức là các bit của địa chỉ IP mà tất cả các thiết bị trong cùng một mạng con phải giống nhau.
2. **Phần host**: Các bit `0` trong subnet mask xác định phần host, tức là các bit của địa chỉ IP mà mỗi thiết bị trong mạng con có thể có giá trị khác nhau.

#### Ví dụ về Subnet Mask

1. **Subnet Mask 255.255.255.0**
   - Địa chỉ IP: `192.168.1.1`
   - Subnet Mask: `255.255.255.0`
   
   Địa chỉ `255.255.255.0` có nghĩa là 24 bit đầu tiên là phần **Network** và 8 bit còn lại là phần **Host**. Điều này có nghĩa là:
   - Mạng: `192.168.1.0/24`
   - Các địa chỉ IP trong mạng này có thể từ `192.168.1.1` đến `192.168.1.254`, vì phần host có 8 bit có thể thay đổi (2^8 - 2 = 254 host).

2. **Subnet Mask 255.255.0.0**
   - Địa chỉ IP: `172.16.0.1`
   - Subnet Mask: `255.255.0.0`
   
   Subnet mask `255.255.0.0` có nghĩa là 16 bit đầu tiên là phần **Network** và 16 bit còn lại là phần **Host**. Mạng này có thể chứa nhiều thiết bị hơn.
   - Mạng: `172.16.0.0/16`
   - Các địa chỉ IP trong mạng này có thể từ `172.16.0.1` đến `172.16.255.254`, với khả năng có 65,534 host (2^16 - 2).

#### Định dạng của Subnet Mask trong Địa Chỉ IP

Thông thường, subnet mask được viết dưới dạng **dấu chấm phân cách** (dotted-decimal), tương tự như địa chỉ IP. Các số trong subnet mask có thể là:

- **255.0.0.0**: Tương đương với **/8** (8 bit đầu tiên cho mạng)
- **255.255.0.0**: Tương đương với **/16** (16 bit đầu tiên cho mạng)
- **255.255.255.0**: Tương đương với **/24** (24 bit đầu tiên cho mạng)
- **255.255.255.255**: Tương đương với **/32** (mạng chỉ có 1 địa chỉ IP duy nhất)

#### Cách tính Subnet Mask

Một số **Subnet Mask** thông dụng và cách viết dạng **CIDR** (Classless Inter-Domain Routing):

- **/8**: Subnet mask `255.0.0.0`
- **/16**: Subnet mask `255.255.0.0`
- **/24**: Subnet mask `255.255.255.0`
- **/32**: Subnet mask `255.255.255.255`

Mỗi số sau dấu gạch chéo (/) cho biết số bit đầu tiên được dùng để chỉ mạng (network bits).

#### Cách hoạt động của Subnet Mask

Subnet mask giúp phân tách phần mạng và phần host của địa chỉ IP. Ví dụ, với một địa chỉ IP `192.168.1.10` và subnet mask `255.255.255.0`:

1. Địa chỉ IP dưới dạng nhị phân:
   - `192.168.1.10` = `11000000.10101000.00000001.00001010`

2. Subnet Mask dưới dạng nhị phân:
   - `255.255.255.0` = `11111111.11111111.11111111.00000000`

Khi áp dụng phép AND giữa địa chỉ IP và subnet mask, bạn sẽ có phần **mạng**:

- **Mạng**: `192.168.1.0`

Phần còn lại là phần **host** của địa chỉ:

- **Host**: `0.0.0.10` (tức là thiết bị có địa chỉ IP là `192.168.1.10`)

#### Ví dụ về cách sử dụng Subnet Mask

1. **Mạng con 255.255.255.0** (`/24`):
   - Mạng: `192.168.1.0/24`
   - Các IP có thể từ `192.168.1.1` đến `192.168.1.254` (254 host)
   
2. **Mạng con 255.255.0.0** (`/16`):
   - Mạng: `172.16.0.0/16`
   - Các IP có thể từ `172.16.0.1` đến `172.16.255.254` (65,534 host)
   
3. **Mạng con 255.255.255.0** (`/24`):
   - Mạng: `10.0.0.0/24`
   - Các IP có thể từ `10.0.0.1` đến `10.0.0.254` (254 host)



--------------------------------------------------------------------------------


### **1. Set static IP, DNS, GATEWAY**

#### **1.1 IP**

##### **IP là gì**

- IP (Internet Protocol) là một địa chỉ duy nhất xác định một thiết bị kết nối với internet hoặc mạng cục bộ. Địa chỉ này giúp xác định và phân biệt các thiết bị trong một mạng.

##### **IP dùng để làm gì?**

- Định tuyến: Các địa chỉ IP giúp các gói dữ liệu tìm đúng đường đi trong mạng Internet.
- Nhận diện thiết bị: Mỗi thiết bị kết nối vào mạng đều có một địa chỉ IP duy nhất, giúp các thiết bị nhận diện và giao tiếp với nhau.

##### **IP hoạt động như thế nào?**

- Mỗi thiết bị kết nối internet có 1 địa chỉ IP duy nhất (giống như địa chỉ nhà).
-  Dữ liệu được chia thành các gói tin nhỏ trước khi được gửi qua mạng. Mỗi gói tin chứa hai phần chính. Phần Header chứa thông tin điều khiển, như địa chỉ IP nguồn và đích, số thứ tự của gói tin, thông tin kiểm tra lỗi. Phần Payload sẽ chứa dữ liệu thực sự được truyền.
-  Khi một gói tin được gửi, nó sẽ được định tuyến qua các thiết bị mạng để đến đích. Các thiết bị này sẽ sử dụng bảng định tuyến để quyết định đường đi tốt nhất cho mỗi gói tin.
- Mỗi gói tin chứa thông tin kiểm tra lỗi để đảm bảo dữ liệu không bị hỏng trong quá trình truyền. Nếu một gói tin bị lỗi, nó có thể được yêu cầu gửi lại.

**Quá trình gửi và nhận**

Bước 1 - chuẩn bị dữ liệu: Dữ liệu từ ứng dụng (như một email) được phân đoạn thành các gói tin.

Bước 2 - Định dạng gói tin: Mỗi gói tin được gán header với địa chỉ IP nguồn và đích.

Bước 3 - Gửi gói tin: Các gói tin được gửi từ thiết bị nguồn qua mạng.

Bước 4 - Chuyển tiếp gói tin: Các router trên đường sẽ định tuyến các gói tin đến đích.

Bước 5 - Nhận và tái cấu trúc: Thiết bị đích nhận các gói tin, kiểm tra và tái cấu trúc chúng thành dữ liệu gốc.

##### **IP private (địa chỉ IP cá nhân)**

**IP Private** là địa chỉ IP được sử dụng trong **mạng nội bộ** (LAN - Local Area Network) và không thể truy cập trực tiếp từ internet. Được router cấp. Chỉ có thể kết nối mạng internet thông qua router.

**Các dải địa chỉ IP Private:**

Dưới đây là các dải địa chỉ IP được phân bổ cho **IP Private** theo chuẩn của **IETF (Internet Engineering Task Force)** trong **RFC 1918**:

1. **Dải 10.0.0.0 - 10.255.255.255** (IP Private)
   - Địa chỉ từ **10.0.0.0** đến **10.255.255.255**
   - Subnet mask: **255.0.0.0**

2. **Dải 172.16.0.0 - 172.31.255.255** (IP Private)
   - Địa chỉ từ **172.16.0.0** đến **172.31.255.255**
   - Subnet mask: **255.240.0.0**

3. **Dải 192.168.0.0 - 192.168.255.255** (IP Private)
   - Địa chỉ từ **192.168.0.0** đến **192.168.255.255**
   - Subnet mask: **255.255.0.0**

![image](https://github.com/user-attachments/assets/e51f9001-1940-4265-b87d-2d62ac6f2357)

**Tại sao sử dụng IP Private?**
- **Tiết kiệm địa chỉ IP**: Số lượng địa chỉ IPv4 có hạn, vì vậy sử dụng **IP Private** giúp tiết kiệm tài nguyên địa chỉ.
- **Bảo mật**: Các địa chỉ **IP Private** không thể truy cập trực tiếp từ internet, giúp bảo vệ các thiết bị trong mạng nội bộ khỏi các cuộc tấn công từ bên ngoài.
- **Sử dụng NAT (Network Address Translation)**: Để các thiết bị trong mạng sử dụng **IP Private** có thể truy cập internet, một hệ thống **NAT** sẽ chuyển đổi địa chỉ **IP Private** thành **IP Public** khi kết nối ra ngoài.

**Cách hoạt động của IP Private:**
1. **Mạng Nội Bộ**: Trong mạng gia đình hoặc công ty, mỗi thiết bị (máy tính, điện thoại, máy in, v.v.) sẽ được cấp một **IP Private** từ router hoặc máy chủ DHCP.
2. **Địa chỉ IP Public**: Để các thiết bị trong mạng nội bộ có thể kết nối ra ngoài internet, **router** hoặc **gateway** sẽ sử dụng **NAT** (Network Address Translation) để chuyển đổi **IP Private** thành **IP Public** khi gửi yêu cầu internet. IP public chỉ cấp cho router.
3. **Không thể truy cập từ ngoài**: Các thiết bị có **IP Private** không thể được truy cập trực tiếp từ internet. Nếu muốn truy cập một thiết bị trong mạng có **IP Private** từ bên ngoài, bạn cần sử dụng phương thức như **VPN**, **Port Forwarding**, hoặc **Reverse SSH**.

**Ví dụ:**
- **Máy tính tại nhà**: Trong mạng gia đình, router của bạn có thể cấp địa chỉ **IP Private** cho các thiết bị như máy tính, điện thoại. Ví dụ, một máy tính có thể có địa chỉ **192.168.1.10**, trong khi router của bạn có địa chỉ **192.168.1.1**.
- **Máy chủ công ty**: Trong môi trường công ty, các máy chủ hoặc thiết bị mạng có thể sử dụng **IP Private** (ví dụ, **10.0.1.100** hoặc **192.168.0.20**) để giao tiếp với các thiết bị trong cùng mạng nội bộ.


----------------------------------

##### **IP Public**

**IP Public** (địa chỉ IP công cộng) là một địa chỉ IP được cấp phát bởi nhà cung cấp dịch vụ Internet (ISP) và có thể được truy cập từ mọi nơi trên Internet. Đây là địa chỉ mà các thiết bị sử dụng để giao tiếp với các máy chủ, dịch vụ, và các thiết bị khác trên mạng Internet.

Đặc điểm của **IP Public**:

1. **Có thể truy cập từ bất kỳ đâu**: Địa chỉ IP công cộng có thể được truy cập từ bất kỳ thiết bị nào trên Internet. Điều này giúp cho các máy chủ web, dịch vụ lưu trữ đám mây, hoặc các dịch vụ trực tuyến có thể giao tiếp với người dùng từ xa.

2. **Được cấp phát công khai**: IP công cộng được cấp phát bởi các tổ chức quản lý Internet như **IANA (Internet Assigned Numbers Authority)** và các nhà cung cấp dịch vụ Internet (ISP). Mỗi địa chỉ IP công cộng là duy nhất và không trùng lặp trên toàn bộ Internet.

3. **Khác với IP Private**: Địa chỉ IP công cộng khác với địa chỉ **IP Private** (địa chỉ IP nội bộ), được sử dụng trong các mạng LAN và không thể được truy cập từ Internet. Địa chỉ IP private nằm trong các dải địa chỉ sau:
   - **10.0.0.0 - 10.255.255.255**
   - **172.16.0.0 - 172.31.255.255**
   - **192.168.0.0 - 192.168.255.255**

4. **Dùng cho các dịch vụ trực tuyến**: Các dịch vụ như **web hosting**, **email server**, **VPN**, **VoIP**, hoặc các dịch vụ trò chuyện trực tuyến cần có địa chỉ IP công cộng để người dùng từ bên ngoài có thể truy cập vào.

**Cấu trúc và định dạng của IP Public:**

IP công cộng có thể có dạng **IPv4** hoặc **IPv6**.

**1. IPv4 Public IP**:
- Địa chỉ IPv4 công cộng có dạng: `x.x.x.x`, trong đó mỗi `x` là một số từ 0 đến 255.
- Ví dụ: `8.8.8.8` (Google DNS), `203.0.113.5`.

**2. IPv6 Public IP**:
- Địa chỉ IPv6 công cộng dài hơn, có dạng: `xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx:xxxx`.
- Ví dụ: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.

**Cách để xác định IP Public của bạn**:
Nếu bạn muốn biết **IP Public** của thiết bị (như router hoặc máy chủ), bạn có thể vào các trang web sau để kiểm tra:
- [WhatIsMyIP](https://www.whatismyip.com/)
- [IPinfo](https://ipinfo.io/)
- [WhatIsMyIPaddress](https://whatismyipaddress.com/)

**Ví dụ về sử dụng IP Public**:
- **Web server**: Khi bạn mở một trang web, bạn sẽ truy cập vào máy chủ web thông qua một **IP Public**. Ví dụ: một trang web có thể có địa chỉ IP công cộng `203.0.113.5`.
- **SSH remote login**: Khi bạn kết nối từ xa đến một máy chủ thông qua **SSH**, bạn sẽ dùng địa chỉ IP công cộng của máy chủ đó.
  
**Tại sao IP Public quan trọng?**
- **Truy cập từ xa**: Các dịch vụ yêu cầu truy cập từ xa qua Internet, chẳng hạn như web hosting, VPN, hoặc truy cập SSH, cần có một **IP Public**.
- **Dịch vụ trực tuyến**: Các dịch vụ như email, game online, hoặc các ứng dụng IoT cũng cần IP Public để tương tác qua Internet.

**Kết luận:**
- **IP Public** là địa chỉ duy nhất trên Internet, có thể được truy cập từ bất kỳ nơi nào trên toàn cầu.
- Đây là địa chỉ không thay đổi và thường được cấp phát bởi nhà cung cấp dịch vụ Internet (ISP).
- Địa chỉ IP công cộng rất quan trọng cho các dịch vụ yêu cầu kết nối từ Internet, ví dụ như web hosting, VPN, hoặc các máy chủ dịch vụ.

##### **Static IP (IP tĩnh)**

- Là địa chỉ IP được cấu hình thủ công. Không thay đổi và được gán cố định cho thiết bị. Phù hợp cho các máy chủ, các dịch vụ yêu cầu kết nối ổn định.

##### **Dynamic IP (IP động)**

- Địa chỉ IP động là một địa chỉ IP mà nhà cung cấp dịch vụ Internet (ISP) cấp phát cho thiết bị của bạn mỗi khi nó kết nối vào mạng. Địa chỉ IP động có thể thay đổi mỗi khi thiết bị kết nối lại vào mạng hoặc sau 1 khoảng thời gian.

-------------------------------------------------------------

#### **1.2 Cấu hình ip động**

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
#### **1.4 Khi nào cấu hình IP động, khi nào cấu hình IP tĩnh**

Tùy thuộc vào mục đích sử dụng.

##### a. **Khi nào cấu hình IP động (DHCP)?**
IP động được cấp phát tự động bởi **DHCP server** mỗi khi thiết bị kết nối mạng. Điều này rất tiện lợi và phổ biến trong nhiều tình huống, đặc biệt là trong các mạng không yêu cầu địa chỉ IP cố định.

###### Sử dụng IP động khi:

- Sử dụng khi không cần 1 địa chỉ IP cố định cho thiết bị để duy trì kết nối ổn địng. các thiết bị thay đổi thường xuyên để giảm bớt việc phải tự cấp phát IP cho mỗi thiết bị

##### b. **Khi nào cấu hình IP tĩnh?**
IP tĩnh là một địa chỉ IP được chỉ định cố định cho một thiết bị cụ thể và không thay đổi trừ khi bạn thay đổi cấu hình. Việc cấu hình IP tĩnh thường được sử dụng cho các thiết bị cần một địa chỉ IP cố định để các thiết bị khác có thể kết nối ổn định.

- DHCP cấu hình IP tĩnh thông qua MAC. tức là IP nào cho MAC nào.

###### Sử dụng IP tĩnh khi:

- server, các thiết bị đòi hỏi kết nối ổn định vì để đảm bảo kết nối liên tục tránh mất kết nối khi thay đổi IP và dễ dàng quản lý.

##### c. **So Sánh giữa IP động và IP tĩnh**

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
- Lý do cần DNS là vì giúp dễ nhớ, dễ sử dụng, dễ truy cập vào web.

#### **2.1 Các khái niệm và cơ chế hoạt động của DNS**

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

- Recursive Resolver: 1 thằng trung gian xử lý các yêu cầu từ người dùng.
- Root Server: Máy chủ gốc, chỉ dẫn Resolver tới các TLD.
- TLD Server: Quản lý thông tin tên miền cấp cao như `.com`, `.vn`.
- Authoritative Server: Máy chủ ủy quyền chứa thông tin chính xác về tên miền (IP, CNAME).

**d. Bản ghi DNS (DNS Records):**

Các loại thông tin ánh xạ trong DNS:

- A Record: Tên miền → IPv4.
- AAAA Record: Tên miền → IPv6.
- CNAME Record: Alias tên miền, chuyển hướng từ tên này sang tên khác.
- MX Record: Máy chủ email.
- TXT Record: Chứa dữ liệu văn bản, dùng để xác thực bảo mật (SPF, DKIM).

#### **2.2 Cơ chế hoạt động của hệ thống DNS**

![image](https://github.com/user-attachments/assets/96517760-7269-4db1-9233-c3637a414299)


1. Người dùng gõ example.com vào trình duyệt. Truy vấn sẽ được gửi tới resolver (resolver do thằng DHCP cấp)
2. Resolver hỏi thằng root (.) để tìm thông tin về example.com
3. Root trả lời resolver địa chỉ TLD chịu trách nhiệm cho .com
4. Resolver gửi yêu cầu đến TLD .com
5. TLD .com trả về địa chỉ của authoritative nameserver cho example.com
6. Resolver truy vấn đến authoritative nameserver của example.com
7. authoritative nameserver trả lời về IP tương ứng example.com
8. DNS gửi IP về cho trình duyệt.

**VD:** DNS doc.hust.vn

1. Người dùng gõ "doc.hust.vn" vào trình duyệt web.
2. Trình duyệt gửi yêu cầu giải quyết tên miền đến DNS resolver (do DHCP cấp).
3. resolver gửi truy vấn đến root (DNS root nameserver).
4. root trả lời resolver địa chỉ của máy chủ TLD cho .vn, nơi lưu trữ thông tin cho các miền có đuôi .vn.
5. resolver gửi truy vấn đến TLD .vn
6. TLD .vn trả lời resolver địa chỉ IP của máy chủ nameserver(second) cho hust.vn, nơi lưu trữ thông tin về các subdomain bên trong hust.vn.
7. resolver truy vấn đến máy chủ nameserver hust.vn
8. Máy chủ nameserver(second) trả lời resolver địa chỉ authoritative nameserver để lấy thông tin về doc.hust.vn.
9. Resolver truy vấn đến authoritative nameserver của doc.hust.vn.
10. authoritative nameserver trả lời về IP tương ứng doc.hust.vn.
11. DNS gửi IP về cho trình duyệt.


### **Các thành phần chính trong hệ thống DNS**:

1. **DNS Resolver**: Là máy chủ DNS chịu trách nhiệm nhận yêu cầu và thực hiện quá trình phân giải từ tên miền thành địa chỉ IP. Resolver có thể là một máy chủ DNS của nhà cung cấp Internet hoặc một máy chủ DNS công cộng như Google DNS.

2. **Root DNS Servers**: Là các máy chủ gốc của hệ thống DNS, giúp xác định máy chủ DNS chịu trách nhiệm phân giải các tên miền cấp cao.

3. **TLD DNS Servers**: Máy chủ DNS này quản lý các miền cấp cao nhất (top-level domain), như `.com`, `.org`, `.net`.

4. **Authoritative DNS Servers**: Là các máy chủ DNS chịu trách nhiệm cung cấp thông tin cuối cùng về tên miền cụ thể (ví dụ, `google.com`). Các máy chủ này có dữ liệu chính thức và đầy đủ về các tên miền và địa chỉ IP tương ứng.

5. **DNS Cache**: Là bộ nhớ đệm lưu trữ thông tin về các tên miền đã được phân giải, giúp tăng tốc độ phân giải tên miền cho các yêu cầu sau.


##### **Tóm tắt cơ chế hoạt động**:

1. Người dùng yêu cầu một tên miền.
2. Resolver kiểm tra bộ nhớ cache của nó và gửi yêu cầu tới root server nếu không có kết quả.
3. Root server trả về thông tin về TLD server.
4. TLD server trả về máy chủ DNS cho tên miền cụ thể.
5. Resolver gửi yêu cầu cuối cùng tới authoritative DNS server và nhận địa chỉ IP.
6. Địa chỉ IP được trả về cho người dùng và lưu trong bộ nhớ cache.


#### **2.3 Các loại máy chủ DNS, các loại query DNS**

##### **2.3.1 Các loại máy chủ DNS**

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

##### **2.3.2 Các loại Query DNS**

**1. Recursive Query (Truy vấn đệ quy):**

- DNS sẽ thực hiện tất cả các bước để giải quyết tên miền cho đến khi ra IP hoặc thông báo lỗi nếu không tìm thấy

**2. Iterative Query (Truy vấn lặp):**

- Khi yêu cầu DNS không biết nó sẽ gửi đến DNS khác để giải quyết. Lặp đi lặp lại cho đến khi ra kq hoặc gặp lỗi (không có tên miền hoặc timeout)

**3. Non-recursive Query (Truy vấn Không Đệ quy)**

- Khi nó biết thằng DNS nào có thẩm quyền trực tiếp hoặc lưu cache

#### **2.4 các loại DNS bản ghi DNS thường sử dụng**

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

### **2.5 Cách tìm IP domain**
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

--------------------------------------------------------------------------------
-------------------------------------------------------------------------------------

### **3. GATEWAY**

- Gateway (cổng mạng) là một nút mạng dùng để kết nối hai mạng khác nhau, hoặc một mạng nội bộ và mạng bên ngoài (ví dụ: Internet).

**Default Gateway:**  
- Là 1 nút để truyền gói tin từ mạng nguồn đến mạng đích khi bảng định tuyến không chứa tuyến đường tới địa chỉ mạng đích. Ví dụ như khi máy tính muốn gửi gói tin đến mạng A (k nằm trong mạng LAN), nhưng trong bảng định tuyến không có tuyến nào dẫn đến A thì nó sẽ đi qua default gateway để định tuyến gói tin đến đích hoặc qua 1 gateway khác.
-  Thường là 1 router hoặc 1 thiết bị có thể kết nối từ LAN ra internet. 

**Chức năng của Gateway**

- quản lý dữ liệu ra vào mạng.
- Hoạt động ở bất kì layer nào
- Chia nhỏ dữ liệu để gửi thay vì gửi hàng loại.
- Bảo mật

**Vì sao cần**
- Vì nó giống như 1 điểm thoát cho tất cả các gói tin từ mạng nội bộ ra máy chủ đích. Không có thì sẽ không thể giao tiếp vs các mạng khác ngoài mạng cục bộ. 
-------------------------------------------
------------------------------------------

### **4.DHCP** 

- DHCP (Dynamic Host Configuration Protocol) là một giao thức mạng được sử dụng để tự động cấp phát địa chỉ IP và các thông tin cấu hình mạng khác cho các thiết bị (hệ thống) trong một mạng máy tính. Giao thức này giúp các thiết bị kết nối vào mạng mà không cần phải cấu hình thủ công các tham số mạng như địa chỉ IP, gateway, DNS, v.v.

#### **Phân Biệt Giao Thức DHCP và Máy Chủ DHCP**

Mặc dù **giao thức DHCP** và **máy chủ DHCP** có mối liên quan chặt chẽ, nhưng chúng là hai khái niệm khác nhau. Dưới đây là sự phân biệt giữa hai yếu tố này:

##### 1. **Giao Thức DHCP (Dynamic Host Configuration Protocol)**
   - **Định nghĩa**: DHCP là một **giao thức mạng** được sử dụng để tự động cấp phát địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị trong mạng mà không cần người dùng phải cấu hình thủ công.
   - **Chức năng chính**:
     - Giao thức này xác định cách các thiết bị trong mạng (máy tính, điện thoại, máy in, v.v.) có thể nhận được địa chỉ IP và các thông tin cấu hình mạng khác như subnet mask, gateway, DNS server từ một máy chủ DHCP.
     - DHCP cung cấp phương thức giao tiếp giữa thiết bị và máy chủ DHCP để cấp phát và quản lý địa chỉ IP động trong mạng.
   - **Quá trình hoạt động**: Giao thức này quy định các bước cụ thể để trao đổi giữa các thiết bị (khách hàng DHCP) và máy chủ DHCP, bao gồm các bước như:
     1. **DHCP Discover** (yêu cầu từ thiết bị).
     2. **DHCP Offer** (phản hồi từ máy chủ).
     3. **DHCP Request** (yêu cầu xác nhận từ thiết bị).
     4. **DHCP Acknowledge** (xác nhận từ máy chủ).
   - **Vai trò**: Giao thức DHCP quy định cách thức cấp phát và quản lý địa chỉ IP động trong mạng.

##### 2. **Máy Chủ DHCP (DHCP Server)**
   - **Định nghĩa**: Máy chủ DHCP là một **máy chủ** chịu trách nhiệm **cung cấp và quản lý** địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị trong mạng theo yêu cầu của giao thức DHCP.
   - **Chức năng chính**:
     - Máy chủ DHCP quản lý một **dãy địa chỉ IP** (gọi là **IP Pool**) và cấp phát các địa chỉ này cho các thiết bị yêu cầu kết nối mạng.
     - Ngoài việc cấp phát địa chỉ IP, máy chủ DHCP còn cung cấp các thông tin khác như subnet mask, default gateway, DNS server, và thời gian thuê địa chỉ IP (lease time).
     - Máy chủ DHCP có thể **gia hạn hoặc thu hồi** địa chỉ IP mà nó đã cấp phát cho các thiết bị.
   - **Vai trò**: Máy chủ DHCP là "nguồn cung cấp" địa chỉ IP cho các thiết bị trong mạng, đảm bảo rằng các thiết bị có thể tự động nhận các thông tin cấu hình mạng mà không cần sự can thiệp thủ công.
   - **Cấu hình**: Máy chủ DHCP có thể được cấu hình trên một máy tính, router hoặc thiết bị mạng chuyên dụng. Thông qua đó, người quản trị có thể chỉ định phạm vi địa chỉ IP có thể được cấp phát, thời gian thuê địa chỉ IP và các thông số khác.

##### **So Sánh Giao Thức DHCP và Máy Chủ DHCP**

| **Tiêu chí**              | **Giao Thức DHCP**                                            | **Máy Chủ DHCP**                                               |
|---------------------------|--------------------------------------------------------------|---------------------------------------------------------------|
| **Định nghĩa**             | Là giao thức mạng dùng để cấp phát và quản lý địa chỉ IP động cho các thiết bị trong mạng. | Là phần mềm hoặc thiết bị cung cấp địa chỉ IP và các thông tin mạng cho các thiết bị. |
| **Chức năng chính**        | Xác định cách thức cấp phát địa chỉ IP và các thông tin cấu hình mạng. | Cung cấp địa chỉ IP, subnet mask, gateway, DNS server, v.v. cho các thiết bị. |
| **Quá trình hoạt động**    | Đảm nhiệm việc thiết lập quy trình cấp phát địa chỉ IP qua các gói DHCP Discover, Offer, Request, và Acknowledge. | Thực hiện các chức năng cấp phát và quản lý địa chỉ IP động dựa trên giao thức DHCP. |
| **Vai trò**                | Giao thức xác định cách thức trao đổi thông tin giữa các thiết bị và máy chủ DHCP. | Máy chủ cấp phát địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị yêu cầu. |
| **Cài đặt và cấu hình**    | Không cần cấu hình cụ thể trên thiết bị (chỉ cần bật tính năng DHCP trên thiết bị). | Cần được cài đặt và cấu hình để quản lý phạm vi IP và các thông số mạng. |


#### **4.1 Chức năng chính DHCP**

**Chức năng chính của DHCP (Dynamic Host Configuration Protocol)** là tự động cấp phát địa chỉ IP và các thông tin cấu hình mạng cho các thiết bị trong một mạng máy tính. Điều này giúp thiết bị có thể kết nối vào mạng mà không cần phải cấu hình thủ công các tham số mạng. Cụ thể, các chức năng chính của DHCP bao gồm:

##### 1. **Cấp Phát Địa Chỉ IP**
   - DHCP cấp phát địa chỉ IP cho các thiết bị (máy tính, điện thoại, máy in, v.v.) khi chúng kết nối vào mạng. Điều này giúp các thiết bị có địa chỉ IP hợp lệ để có thể giao tiếp trong mạng và với các thiết bị khác.
   - Địa chỉ IP có thể là **tĩnh** (được chỉ định cho thiết bị cụ thể) hoặc **động** (cấp phát từ phạm vi các địa chỉ IP có sẵn của máy chủ DHCP).

##### 2. **Cung Cấp Thông Tin Cấu Hình Mạng**
   Ngoài địa chỉ IP, DHCP còn cấp phát các thông tin mạng quan trọng khác như:
   - **Subnet Mask**: Giúp thiết bị xác định phạm vi mạng con. Router quyết định gói dữ liệu sẽ đi qua mạng nào và đến thiết bị nào.
   - **Default Gateway**: Địa chỉ của router hoặc thiết bị dùng để kết nối mạng nội bộ với mạng ngoài (ví dụ: Internet).
   - **DNS Server**: Địa chỉ của máy chủ DNS để chuyển đổi tên miền thành địa chỉ IP (ví dụ: `www.google.com` thành `172.217.5.68`).

##### 3. **Quản Lý Lease Time (Thời Gian Cấp Phát)**
   - Mỗi địa chỉ IP cấp phát cho thiết bị sẽ có một thời gian sử dụng gọi là **lease time** (thời gian thuê). Khi hết thời gian này, thiết bị sẽ phải yêu cầu cấp phát lại địa chỉ IP.
   - Nếu thiết bị vẫn đang sử dụng mạng, nó có thể yêu cầu gia hạn thời gian thuê mà không cần thay đổi địa chỉ IP.

##### 4. **Cung Cấp Địa Chỉ IP Động**
   - DHCP cấp phát **địa chỉ IP động** cho các thiết bị, nghĩa là mỗi khi thiết bị kết nối vào mạng, nó có thể nhận được một địa chỉ IP khác, miễn là trong phạm vi được cấu hình sẵn của máy chủ DHCP.
   - Điều này giúp tối ưu hóa việc sử dụng tài nguyên IP, đặc biệt trong các mạng có số lượng thiết bị thay đổi thường xuyên.

##### 5. **Hỗ Trợ DHCP Relay**
   - DHCP Relay là tính năng cho phép yêu cầu DHCP từ các thiết bị trong các mạng con khác nhau (subnets) được chuyển tiếp đến một máy chủ DHCP duy nhất, thay vì phải có một máy chủ DHCP trong mỗi mạng con.
   - Tính năng này hữu ích trong các mạng lớn, giúp giảm chi phí và dễ dàng quản lý cấu hình IP.

##### 6. **Cấu Hình Tự Động**
   - DHCP giúp tự động cấu hình các thiết bị trong mạng mà không cần can thiệp thủ công, đặc biệt trong các môi trường mạng lớn, giúp tiết kiệm thời gian và giảm thiểu sai sót.

#### **4.2 Cơ chế hoạt động của giao thức DHCP và máy chủ DHCP**

##### **Các Bước Hoạt Động Cơ Bản của Giao Thức DHCP**

Khi một thiết bị (máy khách DHCP) muốn kết nối vào mạng, nó sẽ thực hiện một quá trình gọi là **DHCP Lease Process** (Quá trình cấp phát địa chỉ IP). Các bước của quá trình này như sau:

1. **DHCP Discover** (Khách hàng tìm kiếm máy chủ DHCP):
   - Khi thiết bị mới kết nối vào mạng và chưa có địa chỉ IP, nó sẽ gửi một **gói DHCP Discover** ra mạng (thường là một thông điệp quảng bá).
   - Gói tin này được gửi đi với địa chỉ đích là **255.255.255.255** (địa chỉ broadcast) để tất cả các thiết bị trên mạng có thể nhận được, bao gồm cả máy chủ DHCP. Để xác định xem thằng nào là DHCP

2. **DHCP Offer** (Máy chủ DHCP đưa ra đề nghị):
   - Máy chủ DHCP nhận được yêu cầu DHCP Discover và sẽ phản hồi bằng một **gói DHCP Offer**.
   - Trong gói DHCP Offer, máy chủ DHCP cung cấp cho thiết bị một địa chỉ IP khả dụng từ phạm vi (IP Pool) của nó, cùng với các thông tin cấu hình khác như:
     - Subnet mask: cấp để xác định phạm vi và các mạng khác có cùng mạng vs nó hay không.
     - Default gateway (router): cấp để cho phép mạng cục bộ có thể giao tiếp ra bên ngoài internet
     - DNS server: chính là DNS resolver
     - Lease time (Thời gian thuê địa chỉ IP)
   - Gói **DHCP Offer** sẽ được gửi đến máy khách qua mạng.

3. **DHCP Request** (Khách hàng yêu cầu cấp phát địa chỉ IP):
   - Sau khi nhận được một hoặc nhiều gói DHCP Offer từ các máy chủ DHCP (nếu có nhiều máy chủ DHCP), thiết bị (máy khách DHCP) sẽ chọn một địa chỉ IP từ gói offer và gửi một **gói DHCP Request** về phía máy chủ DHCP.
   - Gói DHCP Request yêu cầu xác nhận và yêu cầu máy chủ DHCP cấp phát địa chỉ IP cho thiết bị.

4. **DHCP Acknowledge** (Máy chủ DHCP xác nhận):
   - Máy chủ DHCP nhận được yêu cầu DHCP Request từ thiết bị và sẽ gửi một **gói DHCP Acknowledge** để xác nhận rằng địa chỉ IP đã được cấp phát thành công.
   - Từ đó, thiết bị sẽ được cấp phát địa chỉ IP và các thông tin cấu hình mạng để sử dụng.

5. **Renewal (Gia hạn Lease Time)**:
   - Sau một khoảng thời gian nhất định (lease time), thiết bị sẽ phải gia hạn địa chỉ IP. Khi lease time còn một nửa, thiết bị sẽ tự động gửi một yêu cầu **DHCP Request** để gia hạn địa chỉ IP. Máy chủ DHCP sẽ gửi lại một gói **DHCP Acknowledge** để xác nhận gia hạn.

6. **Releasing IP**:
   - Khi thiết bị không còn sử dụng mạng hoặc ngắt kết nối, nó có thể gửi một gói **DHCP Release** để thông báo cho máy chủ DHCP rằng nó không còn cần địa chỉ IP nữa. Máy chủ DHCP sau đó sẽ giải phóng địa chỉ IP và đưa vào kho địa chỉ IP có thể sử dụng lại.

##### **Chi Tiết về Máy Chủ DHCP**
Máy chủ DHCP đóng vai trò là **trung tâm cấp phát địa chỉ IP và thông tin mạng** cho các thiết bị trong mạng. Cơ chế hoạt động của máy chủ DHCP có thể được mô tả qua các chức năng chính sau:

1. **Quản Lý Phạm Vi Địa Chỉ IP (IP Pool)**
   - Máy chủ DHCP có một **danh sách các địa chỉ IP khả dụng** (gọi là IP Pool). Các địa chỉ này được cấp phát cho các thiết bị yêu cầu kết nối mạng.
   - Máy chủ DHCP sẽ **cấp phát địa chỉ IP từ dải này** cho các thiết bị, đảm bảo rằng không có sự trùng lặp địa chỉ IP trong mạng.

2. **Thời Gian Thuê Địa Chỉ IP (Lease Time)**
   - Mỗi địa chỉ IP được cấp phát cho thiết bị trong một khoảng thời gian xác định, gọi là **lease time**.
   - Sau khi hết thời gian thuê, địa chỉ IP này sẽ bị thu hồi và có thể được cấp phát lại cho các thiết bị khác.
   - Máy chủ DHCP có thể gia hạn thời gian thuê nếu thiết bị yêu cầu và vẫn đang sử dụng mạng.

3. **Cấu Hình Thông Tin Mạng**
   - Máy chủ DHCP không chỉ cấp phát địa chỉ IP, mà còn cung cấp các thông tin quan trọng khác cho thiết bị, bao gồm:
     - **Subnet mask**: Để thiết bị xác định phạm vi mạng con.
     - **Default gateway**: Địa chỉ của router để thiết bị có thể kết nối với các mạng khác (ví dụ: Internet).
     - **DNS server**: Để thiết bị có thể phân giải tên miền.
     - Các thông tin khác như **NTP server** (máy chủ thời gian), **WINS server** (máy chủ tên NetBIOS), v.v.

4. **Chức Năng Gia Hạn (Renewal)**
   - Khi một thiết bị đang sử dụng địa chỉ IP, nó sẽ liên tục gia hạn **lease time** trước khi hết hạn, thường là một nửa thời gian thuê. Nếu máy chủ DHCP vẫn còn địa chỉ IP trong phạm vi của nó và thiết bị yêu cầu gia hạn, máy chủ sẽ tiếp tục cấp phát địa chỉ này.

5. **Cơ Chế Quản Lý IP**
   - Máy chủ DHCP có thể **phân loại và phân bổ địa chỉ IP** cho các nhóm thiết bị khác nhau trong mạng. Ví dụ, máy chủ có thể cấp phát một dải địa chỉ IP cho các máy tính trong văn phòng và một dải khác cho các thiết bị di động.

##### **Tóm Tắt Các Bước Hoạt Động**

| **Bước**              | **Mô Tả**                                                    |
|-----------------------|--------------------------------------------------------------|
| **1. DHCP Discover**   | Thiết bị gửi yêu cầu DHCP để tìm máy chủ DHCP.               |
| **2. DHCP Offer**      | Máy chủ DHCP gửi thông tin cấp phát địa chỉ IP và cấu hình mạng cho thiết bị. |
| **3. DHCP Request**    | Thiết bị yêu cầu cấp phát địa chỉ IP từ máy chủ DHCP.        |
| **4. DHCP Acknowledge**| Máy chủ DHCP xác nhận và cấp phát địa chỉ IP cho thiết bị.    |
| **5. Renewal**         | Sau khi hết thời gian thuê, thiết bị yêu cầu gia hạn địa chỉ IP. |
| **6. Release**         | Thiết bị gửi thông báo giải phóng địa chỉ IP khi không còn sử dụng. |
