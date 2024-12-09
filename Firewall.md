### **`IPTABLES`**

- `iptables` là một công cụ dòng lệnh trong Linux dùng để cấu hình tường lửa (firewall) và lọc các gói tin trong hệ thống mạng. Nó cho phép bạn quản lý các quy tắc (rules) kiểm tra và điều khiển lưu lượng mạng, từ đó bảo vệ hệ thống của bạn khỏi các mối đe dọa từ bên ngoài và điều chỉnh cách dữ liệu được gửi qua mạng.

`iptables` là một công cụ mạnh mẽ dùng để kiểm soát lưu lượng mạng trong hệ thống Linux, cung cấp khả năng lọc gói tin, NAT, và kiểm tra các điều kiện kết nối. Các thành phần chính của `iptables` bao gồm **bảng** (tables), **chuỗi** (chains), **quy tắc** (rules), **mô-đun** (modules), và **hành động** (targets). Dưới đây là chi tiết về các thành phần này.


### 1. **Bảng (Tables)**

Mỗi bảng trong `iptables` chứa một tập hợp các chuỗi và quy tắc dùng để xử lý các gói tin. Các bảng chính trong `iptables` là:

#### a. **filter** (Mặc định)
Bảng `filter` là bảng mặc định và chủ yếu dùng để lọc gói tin. Các quy tắc trong bảng này quyết định xem gói tin có được phép vào hệ thống hay không.
- **Chuỗi chính trong bảng filter**:
  - **INPUT**: Kiểm tra các gói tin đến hệ thống.
  - **OUTPUT**: Kiểm tra các gói tin xuất phát từ hệ thống.
  - **FORWARD**: Kiểm tra các gói tin được chuyển tiếp qua hệ thống (router).
  
  **Lưu ý**: Đây là bảng mặc định khi sử dụng `iptables` để lọc các kết nối mạng.

#### b. **nat** (Network Address Translation)
Bảng `nat` dùng để thực hiện NAT (Đổi địa chỉ mạng), chẳng hạn như chuyển tiếp cổng hoặc thay đổi địa chỉ IP của các gói tin. Bảng này đặc biệt hữu ích trong các cấu hình router hoặc gateway.
- **Chuỗi trong bảng `nat`**:
  - **PREROUTING**: Được sử dụng để thay đổi các gói tin ngay khi chúng đến hệ thống, trước khi định tuyến.
  - **POSTROUTING**: Được sử dụng để thay đổi các gói tin sau khi chúng đã được định tuyến.
  - **OUTPUT**: Kiểm tra các gói tin được tạo ra từ chính hệ thống (thường là gói tin ra ngoài internet).

#### c. **mangle**
Bảng `mangle` được sử dụng để thay đổi các thuộc tính của gói tin, như thay đổi TTL (Time To Live), QoS (Quality of Service), hoặc các đánh dấu khác.
- **Chuỗi trong bảng `mangle`**:
  - **PREROUTING**: Chỉnh sửa gói tin khi chúng vừa vào hệ thống.
  - **POSTROUTING**: Chỉnh sửa gói tin sau khi định tuyến.
  - **INPUT, OUTPUT, FORWARD**: Kiểm tra gói tin vào hoặc ra từ hệ thống.

#### d. **raw**
Bảng `raw` được sử dụng trước khi các gói tin đi qua các bảng khác. Nó chủ yếu dùng để bỏ qua việc theo dõi trạng thái kết nối, giúp tăng tốc độ xử lý đối với các ứng dụng không yêu cầu kiểm tra trạng thái.
- **Chuỗi trong bảng `raw`**:
  - **PREROUTING**: Xử lý gói tin khi chúng đến hệ thống.
  - **POSTROUTING**: Xử lý gói tin trước khi chúng ra khỏi hệ thống.

#### e. **security**
Bảng `security` hỗ trợ các chính sách bảo mật, đặc biệt là trong môi trường SELinux (Security-Enhanced Linux). Nó cho phép xác định các chính sách bảo mật cho các gói tin đi qua hệ thống.


### 2. **Chuỗi (Chains)**

Mỗi bảng chứa các chuỗi. Một **chuỗi** là một tập hợp các quy tắc, nơi các gói tin sẽ được kiểm tra. Các chuỗi chính trong `iptables` gồm:

#### a. **INPUT**:
Dùng để xử lý các gói tin đi vào hệ thống. Quy tắc trong chuỗi này quyết định xem gói tin có được phép đến hệ thống hay không.

#### b. **OUTPUT**:
Dùng để xử lý các gói tin xuất phát từ hệ thống (ví dụ: kết nối HTTP, SSH). Quy tắc trong chuỗi này quyết định xem gói tin có được phép gửi ra ngoài hay không.

#### c. **FORWARD**:
Dùng trong các thiết lập router hoặc gateway, xử lý các gói tin được chuyển tiếp từ một giao diện mạng đến giao diện khác.

#### d. **PREROUTING**:
Chạy trước khi các gói tin được định tuyến đến các địa chỉ đích. Quy tắc trong chuỗi này có thể thay đổi hoặc chuyển hướng các gói tin trước khi định tuyến.

#### e. **POSTROUTING**:
Chạy sau khi các gói tin đã được định tuyến. Chuỗi này thường được sử dụng trong NAT để thay đổi địa chỉ IP hoặc port của gói tin khi ra ngoài hệ thống.


### 3. **Quy Tắc (Rules)**

Mỗi chuỗi chứa một hoặc nhiều **quy tắc** (rules), định nghĩa cách thức xử lý gói tin. Một quy tắc bao gồm:
- **Điều kiện** (Conditions): Kiểm tra các đặc điểm của gói tin, ví dụ:
  - **Địa chỉ IP nguồn (Source IP)**: Xác định địa chỉ IP của máy gửi.
  - **Địa chỉ IP đích (Destination IP)**: Xác định địa chỉ IP của máy nhận.
  - **Cổng (Port)**: Xác định cổng giao thức.
  - **Giao thức (Protocol)**: TCP, UDP, ICMP, v.v.
  - **Trạng thái kết nối (Connection State)**: (new, established, related, invalid).
  
- **Hành động (Action)**: Định nghĩa hành động thực hiện nếu gói tin khớp với quy tắc, ví dụ:
  - **ACCEPT**: Cho phép gói tin tiếp tục.
  - **DROP**: Từ chối gói tin mà không thông báo.
  - **REJECT**: Từ chối gói tin và gửi một thông báo lỗi.
  - **LOG**: Ghi lại thông tin gói tin vào hệ thống nhật ký.


### 4. **Mô-đun (Modules)**

`iptables` có thể sử dụng các mô-đun để mở rộng khả năng kiểm tra và xử lý gói tin. Mô-đun cho phép kiểm tra thêm các điều kiện hoặc thực hiện các chức năng cụ thể. Ví dụ:
- **state**: Kiểm tra trạng thái của kết nối (new, established, related, invalid).
- **limit**: Giới hạn tốc độ lưu lượng mạng (ví dụ: chỉ cho phép một số lượng gói tin nhất định trong một khoảng thời gian).
- **tcp**: Kiểm tra các thuộc tính của giao thức TCP (ví dụ: cổng, flags, v.v.).
- **icmp**: Kiểm tra các gói tin ICMP (ping, traceroute).
- **multiport**: Kiểm tra nhiều cổng một lúc.


### 5. **Hành Động (Targets)**

Mỗi quy tắc có thể bao gồm một **hành động** (target), quyết định cách xử lý gói tin khi chúng khớp với quy tắc. Các hành động phổ biến bao gồm:
- **ACCEPT**: Cho phép gói tin tiếp tục.
- **DROP**: Từ chối gói tin mà không gửi thông báo (tiết kiệm tài nguyên).
- **REJECT**: Từ chối gói tin và gửi một thông báo lỗi (thường là ICMP "Destination Unreachable").
- **LOG**: Ghi lại thông tin gói tin vào nhật ký mà không thay đổi trạng thái của gói tin.
- **SNAT**: Thực hiện Source NAT, thay đổi địa chỉ IP nguồn của gói tin.
- **DNAT**: Thực hiện Destination NAT, thay đổi địa chỉ IP đích của gói tin.
- **MASQUERADE**: Dùng cho Source NAT, tự động thay đổi địa chỉ nguồn khi địa chỉ IP của hệ thống thay đổi (thường dùng khi chia sẻ kết nối internet).
  

-------------------------------------

### **Quy trình xử lý gói tin trong `iptables`**

Quy trình xử lý gói tin trong `iptables` diễn ra qua các bước sau khi một gói tin được gửi tới hệ thống. Mỗi gói tin sẽ được kiểm tra theo các quy tắc trong các bảng và chuỗi tương ứng. Sau đây là quy trình chi tiết:

1. **Nhận Gói Tin**
Khi một gói tin đến từ một nguồn (máy tính khác hoặc mạng bên ngoài), nó sẽ được gửi đến máy chủ đang chạy `iptables`. Gói tin này sẽ được phân loại và xử lý dựa trên các bảng và chuỗi trong `iptables`.

2. **Xử Lý Qua Các Bảng (Tables)**
Mỗi gói tin sẽ đi qua một trong các bảng của `iptables`. Các bảng chính là:
- **filter**: Bảng mặc định để lọc các gói tin.
- **nat**: Bảng dùng cho Network Address Translation (NAT), ví dụ như để chuyển tiếp cổng hoặc thay đổi địa chỉ IP nguồn.
- **mangle**: Bảng dùng để thay đổi các thuộc tính của gói tin, như thay đổi TTL, QoS, hoặc đánh dấu gói tin.
- **raw**: Bảng này được xử lý trước các bảng khác, và chủ yếu được sử dụng để bỏ qua trạng thái kết nối.
- **security**: Bảng này được sử dụng trong SELinux để thực thi các chính sách bảo mật.

3. **Xử Lý Qua Các Chuỗi (Chains)**
Mỗi bảng có các **chuỗi** để xử lý gói tin. Các chuỗi chính bao gồm:
- **INPUT**: Dùng để kiểm tra gói tin đi vào hệ thống (gói tin đến máy chủ).
- **OUTPUT**: Dùng để kiểm tra gói tin xuất phát từ hệ thống (gói tin gửi đi từ máy chủ).
- **FORWARD**: Dùng để kiểm tra gói tin chuyển tiếp qua hệ thống (gói tin đi qua router hoặc gateway).
- **PREROUTING**: Dùng trong bảng `nat` để xử lý gói tin ngay khi chúng vào hệ thống, trước khi định tuyến.
- **POSTROUTING**: Dùng trong bảng `nat` để xử lý gói tin sau khi đã được định tuyến, trước khi chúng rời khỏi hệ thống.

4. **Kiểm Tra Các Quy Tắc (Rules)**
Mỗi chuỗi chứa các **quy tắc** (rules) mà gói tin sẽ phải kiểm tra. Quy tắc có thể kiểm tra các thông tin như:
- Địa chỉ IP nguồn và đích.
- Cổng giao thức (TCP, UDP).
- Giao thức (TCP, UDP, ICMP, v.v.).
- Trạng thái kết nối (new, established, related).

Quy tắc trong chuỗi được kiểm tra theo thứ tự từ trên xuống dưới. Nếu gói tin khớp với một quy tắc, hành động của quy tắc đó sẽ được thực thi (ví dụ: ACCEPT, DROP, REJECT, LOG).

5. **Hành Động Quy Tắc**
Khi một gói tin khớp với quy tắc, hành động của quy tắc đó sẽ được thực thi. Các hành động phổ biến bao gồm:
- **ACCEPT**: Cho phép gói tin tiếp tục (gói tin được chuyển tiếp hoặc gửi đi).
- **DROP**: Từ chối gói tin mà không gửi thông báo, gói tin sẽ bị loại bỏ.
- **REJECT**: Từ chối gói tin và gửi một thông báo lỗi (thường là ICMP "Destination Unreachable").
- **LOG**: Ghi lại thông tin về gói tin trong nhật ký nhưng không thay đổi trạng thái của nó.
- **SNAT**: Thực hiện Source NAT, thay đổi địa chỉ IP nguồn của gói tin (thường dùng cho NAT).
- **DNAT**: Thực hiện Destination NAT, thay đổi địa chỉ IP đích của gói tin (thường dùng cho chuyển tiếp cổng).
- **MASQUERADE**: Một loại SNAT tự động thay đổi địa chỉ IP nguồn của gói tin khi hệ thống gửi gói tin ra ngoài, thường dùng trong các kết nối chia sẻ internet.

6. **Tiến Trình Quá Trình Xử Lý**
- **Đối với gói tin đến (INPUT)**: Gói tin sẽ đi qua chuỗi `INPUT` trong bảng `filter`. Nếu không khớp với bất kỳ quy tắc nào trong chuỗi, hành động mặc định (thường là **ACCEPT**) sẽ được thực thi.
- **Đối với gói tin đi ra (OUTPUT)**: Gói tin sẽ đi qua chuỗi `OUTPUT`. Nếu không khớp với quy tắc nào, hành động mặc định sẽ được áp dụng.
- **Đối với gói tin chuyển tiếp (FORWARD)**: Gói tin sẽ đi qua chuỗi `FORWARD`. Nếu máy chủ đang hoạt động như một router hoặc gateway, gói tin sẽ được xử lý và chuyển tiếp dựa trên các quy tắc ở chuỗi này.

7. **Chuyển Tiếp Hoặc Từ Chối Gói Tin**
- Nếu gói tin được phép (ACCEPT), nó sẽ được chuyển tiếp hoặc ra ngoài hệ thống (tùy thuộc vào chuỗi xử lý).
- Nếu gói tin bị từ chối (DROP hoặc REJECT), nó sẽ không được gửi đi và có thể bị ghi lại nếu có quy tắc **LOG**.

8. **Trạng Thái Kết Nối (Connection Tracking)**
`iptables` có thể theo dõi trạng thái của các kết nối bằng cách sử dụng mô-đun **state** hoặc **conntrack**. Điều này cho phép hệ thống xác định xem một gói tin là:
- **NEW**: Một kết nối mới.
- **ESTABLISHED**: Kết nối đã được thiết lập.
- **RELATED**: Gói tin liên quan đến một kết nối đã thiết lập (ví dụ: gói tin FTP DATA).
- **INVALID**: Gói tin không hợp lệ.

Trạng thái của gói tin sẽ ảnh hưởng đến việc áp dụng quy tắc. Ví dụ, các gói tin đã được thiết lập có thể được phép mà không cần kiểm tra kỹ hơn.

9. **Kết Thúc Quy Trình**
Quá trình xử lý gói tin tiếp tục cho đến khi gói tin được xử lý hết, có thể là được phép tiếp tục (ACCEPT), từ chối (DROP/REJECT), hoặc ghi lại thông tin (LOG). Nếu không có quy tắc nào khớp và không có hành động mặc định, gói tin sẽ bị từ chối.

-----------------------------------------------

### **Cách dùng `iptables`**

`iptables` là một công cụ quản lý firewall trên Linux, được sử dụng để kiểm soát luồng lưu lượng mạng (traffic) qua các quy tắc, giúp tăng cường bảo mật và cấu hình mạng. Dưới đây là hướng dẫn cách sử dụng `iptables` cơ bản:

### 1. **Cấu trúc của iptables**
Các lệnh `iptables` thường có cấu trúc như sau:

```bash
iptables -[A|I|D|L|F|P] [CHAIN] [options]
```

- `-A`: Thêm quy tắc vào chuỗi (append).
- `-I`: Chèn quy tắc vào đầu chuỗi (insert).
- `-D`: Xóa quy tắc (delete).
- `-L`: Liệt kê các quy tắc hiện tại (list).
- `-F`: Xóa tất cả các quy tắc (flush).
- `-P`: Thiết lập chính sách mặc định cho chuỗi (policy).

### 2. **Các chuỗi (Chains) trong iptables**
iptables có 3 chuỗi mặc định:
- **INPUT**: Chỉ định các gói tin đến hệ thống.
- **OUTPUT**: Chỉ định các gói tin xuất phát từ hệ thống.
- **FORWARD**: Chỉ định các gói tin đi qua hệ thống (nếu hệ thống làm gateway).

### 3. **Các đối tượng thường dùng với iptables**
- **-p [protocol]**: Chỉ định giao thức (TCP, UDP, ICMP, v.v.).
- **--dport [port]**: Cổng đích.
- **--sport [port]**: Cổng nguồn.
- **-s [ip]**: Địa chỉ IP nguồn.
- **-d [ip]**: Địa chỉ IP đích.
- **-j [action]**: Hành động (ACCEPT, DROP, REJECT, v.v.).

### 4. **Ví dụ các lệnh cơ bản**

#### 4.1. **Xem các quy tắc hiện tại**
Để xem các quy tắc hiện tại trong `iptables`, bạn dùng lệnh:

```bash
sudo iptables -L
```

Nếu muốn liệt kê chi tiết hơn, có thể thêm tham số `-v`:

```bash
sudo iptables -L -v
```

#### 4.2. **Thêm quy tắc (Add rules)**

##### Cho phép một cổng cụ thể (ví dụ: cổng 80 cho HTTP)

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

- `-A INPUT`: Thêm quy tắc vào chuỗi INPUT (gói tin đến hệ thống).
- `-p tcp`: Sử dụng giao thức TCP.
- `--dport 80`: Cổng đích là 80 (HTTP).
- `-j ACCEPT`: Cho phép kết nối.

##### Cho phép SSH từ một địa chỉ IP cụ thể

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.10 -j ACCEPT
```

- `--dport 22`: Cổng SSH.
- `-s 192.168.1.10`: Chỉ cho phép kết nối SSH từ địa chỉ IP `192.168.1.10`.

##### Chặn một cổng (ví dụ: cổng 23 cho Telnet)

```bash
sudo iptables -A INPUT -p tcp --dport 23 -j DROP
```

- `-j DROP`: Từ chối tất cả các kết nối đến cổng 23 (Telnet).

#### 4.3. **Xóa quy tắc (Delete rules)**

Nếu bạn muốn xóa một quy tắc, bạn sử dụng `-D`. Ví dụ:

```bash
sudo iptables -D INPUT -p tcp --dport 80 -j ACCEPT
```

#### 4.4. **Xóa tất cả quy tắc (Flush rules)**

Để xóa tất cả các quy tắc trong `iptables`, bạn sử dụng lệnh sau:

```bash
sudo iptables -F
```

#### 4.5. **Thiết lập chính sách mặc định (Default policy)**

Chính sách mặc định của chuỗi là hành động được áp dụng cho các gói tin không khớp với bất kỳ quy tắc nào. Để đặt chính sách mặc định, bạn sử dụng `-P`.

##### Ví dụ: Đặt chính sách mặc định là `DROP` cho chuỗi INPUT

```bash
sudo iptables -P INPUT DROP
```

Điều này có nghĩa là **chặn tất cả các gói tin** đến hệ thống trừ khi có quy tắc nào cho phép chúng.

#### 4.6. **Tạo NAT (Network Address Translation)**

Nếu bạn muốn sử dụng `iptables` như một **gateway** NAT, cho phép các máy trong mạng LAN truy cập Internet qua IP của máy chủ, bạn cần sử dụng bảng `nat`.

##### Ví dụ: Thiết lập NAT để cho phép chia sẻ kết nối Internet từ `eth0` (cổng ngoài) sang `eth1` (cổng LAN)

```bash
sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

- `-t nat`: Chỉ định bảng `nat`.
- `POSTROUTING`: Quy tắc xử lý gói tin sau khi ra khỏi hệ thống.
- `-o eth0`: Sử dụng interface `eth0` (cổng ra Internet).
- `MASQUERADE`: Áp dụng NAT để các gói tin sẽ mang địa chỉ IP của server.

#### 4.7. **Cho phép chuyển tiếp gói tin (IP Forwarding)**

Để hệ thống có thể chuyển tiếp gói tin giữa các mạng (chẳng hạn như một gateway), bạn cần bật **IP forwarding**.

##### Để bật IP forwarding tạm thời:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

##### Để bật IP forwarding vĩnh viễn:

Chỉnh sửa file `/etc/sysctl.conf`:

```bash
sudo nano /etc/sysctl.conf
```

Tìm và bỏ comment dòng sau:

```bash
net.ipv4.ip_forward=1
```

Sau đó, áp dụng thay đổi:

```bash
sudo sysctl -p
```

#### 4.8. **Lưu các quy tắc iptables**

Để đảm bảo các quy tắc sẽ không bị mất sau khi khởi động lại hệ thống, bạn có thể lưu chúng:

Trên Ubuntu/Debian:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```

Trên CentOS/Fedora:

```bash
sudo service iptables save
```

### 5. **Kiểm tra và xem lại quy tắc iptables**

Để kiểm tra các quy tắc hiện tại trong `iptables`, bạn có thể sử dụng:

```bash
sudo iptables -L -n -v
```

Lệnh này sẽ hiển thị tất cả các quy tắc hiện tại, bao gồm cả thông tin về lượng lưu lượng mạng (số gói tin và byte) đã được xử lý bởi từng quy tắc.


------------------------------------------------

### **Cách cấu hình `iptables`**

Cấu hình `iptables` trên Linux có thể thực hiện qua dòng lệnh, thường xuyên sử dụng quyền root hoặc sudo. Dưới đây là một số bước cơ bản để cấu hình `iptables`:

1. **Kiểm Tra Trạng Thái Hiện Tại**
Trước khi cấu hình `iptables`, bạn nên kiểm tra các quy tắc hiện tại trong hệ thống:

```bash
sudo iptables -L
```

Lệnh này sẽ liệt kê các quy tắc hiện tại trong hệ thống, bao gồm các chuỗi **INPUT**, **OUTPUT**, **FORWARD**, và các quy tắc trong các bảng khác.

2. **Cấu Hình Quy Tắc Cơ Bản**
Bạn có thể thêm các quy tắc để cho phép hoặc từ chối các kết nối mạng. Dưới đây là một số ví dụ về cách cấu hình các quy tắc `iptables`.

#### a. **Cho phép kết nối SSH (Cổng 22)**
Để cho phép kết nối SSH vào hệ thống, sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
- `-A INPUT`: Thêm quy tắc vào chuỗi INPUT.
- `-p tcp`: Chỉ định giao thức TCP.
- `--dport 22`: Chỉ định cổng đích là 22 (cổng SSH).
- `-j ACCEPT`: Hành động là cho phép gói tin.

#### b. **Chặn một địa chỉ IP cụ thể**
Để chặn một địa chỉ IP nhất định, ví dụ như 192.168.1.100, từ việc kết nối tới hệ thống:

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
- `-s 192.168.1.100`: Chỉ định địa chỉ IP nguồn.
- `-j DROP`: Từ chối các gói tin từ địa chỉ này.

#### c. **Cho phép tất cả các kết nối ra ngoài**
Để cho phép tất cả các kết nối đi ra ngoài hệ thống (đi từ máy chủ tới internet), bạn có thể thêm quy tắc vào chuỗi OUTPUT:

```bash
sudo iptables -A OUTPUT -j ACCEPT
```

#### d. **Chặn tất cả kết nối vào hệ thống trừ các kết nối SSH**
Nếu bạn muốn chặn tất cả các kết nối đến máy chủ trừ kết nối SSH (cổng 22), có thể cấu hình như sau:

1. **Chặn tất cả kết nối vào:**

```bash
sudo iptables -A INPUT -j DROP
```

2. **Cho phép kết nối SSH vào:**

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

#### e. **Chặn tất cả kết nối từ một mạng con (IP range)**
Ví dụ, chặn tất cả các kết nối từ dải IP `192.168.1.0/24`:

```bash
sudo iptables -A INPUT -s 192.168.1.0/24 -j DROP
```

3. **Lưu Quy Tắc**
Các quy tắc `iptables` sẽ bị mất sau khi hệ thống khởi động lại. Để lưu các quy tắc, bạn có thể sử dụng các công cụ như `iptables-save` và `iptables-restore`.

- **Lưu quy tắc hiện tại vào một file**:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```

- **Khôi phục quy tắc từ file đã lưu**:

```bash
sudo iptables-restore < /etc/iptables/rules.v4
```

#### Cấu hình để tự động tải lại quy tắc `iptables` khi khởi động lại hệ thống:

- Trên hệ thống Debian/Ubuntu, bạn có thể cài đặt gói `iptables-persistent` để tự động lưu và khôi phục quy tắc:

```bash
sudo apt-get install iptables-persistent
```

- Trên CentOS/RedHat, bạn có thể sử dụng `service iptables save` để lưu quy tắc vào file cấu hình.

4. **Cấu Hình NAT (Network Address Translation)**

#### a. **Source NAT (SNAT)**
Giả sử bạn muốn thay đổi địa chỉ IP nguồn của các gói tin từ một mạng nội bộ (ví dụ: `192.168.1.0/24`) khi chúng đi ra ngoài:

```bash
sudo iptables -t nat -A POSTROUTING -s 192.168.1.0/24 -j MASQUERADE
```
- `-t nat`: Sử dụng bảng NAT.
- `-A POSTROUTING`: Thêm quy tắc vào chuỗi POSTROUTING.
- `-s 192.168.1.0/24`: Chỉ định dải địa chỉ IP nguồn.
- `-j MASQUERADE`: Áp dụng NAT, thay đổi địa chỉ nguồn của các gói tin.

#### b. **Destination NAT (DNAT)**
Nếu bạn muốn chuyển tiếp các gói tin đến một máy chủ cụ thể trong mạng nội bộ, ví dụ, chuyển tiếp từ cổng 80 đến địa chỉ IP `192.168.1.10`:

```bash
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10
```

5. **Xóa Quy Tắc**
Để xóa một quy tắc đã thêm vào `iptables`, bạn có thể sử dụng lệnh `-D`:

- Xóa quy tắc cho phép kết nối SSH (cổng 22) trong chuỗi `INPUT`:

```bash
sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT
```

- Xóa một quy tắc cụ thể dựa trên số thứ tự của quy tắc:

```bash
sudo iptables -D INPUT 1
```
Lệnh trên xóa quy tắc đầu tiên trong chuỗi INPUT.

6. **Liệt Kê Quy Tắc**
Để liệt kê tất cả các quy tắc trong `iptables`, bạn có thể sử dụng:

```bash
sudo iptables -L
```

Để liệt kê chi tiết các quy tắc, bao gồm số lượng gói tin và byte đã xử lý:

```bash
sudo iptables -L -v
```

Để liệt kê quy tắc trong bảng NAT:

```bash
sudo iptables -t nat -L
```

7. **Khôi Phục Quy Tắc Mặc Định**
Để khôi phục lại các quy tắc mặc định (chặn mọi kết nối), bạn có thể sử dụng:

```bash
sudo iptables -F
```

Lệnh này sẽ **xóa tất cả các quy tắc** hiện tại trong các chuỗi của `iptables`.


-------------------------------------------------------

### **Chặn 1 port**

### 1. **Chặn một cổng TCP**

Để chặn một cổng TCP cụ thể (ví dụ cổng 80 - HTTP):

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j DROP
```
**Giải thích:**
- `-A INPUT`: Thêm quy tắc vào chuỗi `INPUT`, có nghĩa là xử lý các gói tin đến (inbound).
- `-p tcp`: Chỉ định giao thức TCP.
- `--dport 80`: Cổng đích là 80 (cổng HTTP).
- `-j DROP`: Nếu gói tin khớp, nó sẽ bị từ chối và không được tiếp tục xử lý.

**Ví dụ:**
- Nếu muốn ngừng truy cập vào dịch vụ web (HTTP) trên cổng 80, sử dụng lệnh trên để chặn tất cả các yêu cầu đến cổng 80.

---

### 2. **Chặn một cổng UDP**

Để chặn một cổng UDP (ví dụ cổng 123 - NTP), bạn sử dụng lệnh:

```bash
sudo iptables -A INPUT -p udp --dport 123 -j DROP
```
**Giải thích:**
- `-p udp`: Chỉ định giao thức UDP.
- `--dport 123`: Cổng đích là 123 (cổng NTP).
- `-j DROP`: Từ chối tất cả các gói tin UDP đến cổng 123.

**Ví dụ:**
- Nếu hệ thống của bạn không sử dụng dịch vụ NTP (Network Time Protocol), bạn có thể chặn cổng 123 để ngừng các yêu cầu NTP từ các máy khác.

---

### 3. **Chặn một cổng TCP cho một địa chỉ IP cụ thể**

Để chặn một cổng TCP từ một địa chỉ IP cụ thể (ví dụ cổng 22 - SSH từ IP `192.168.1.100`), bạn có thể sử dụng lệnh:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.100 -j DROP
```
**Giải thích:**
- `-s 192.168.1.100`: Chỉ định địa chỉ IP nguồn là `192.168.1.100`.
- `--dport 22`: Cổng đích là 22 (cổng SSH).
- `-j DROP`: Từ chối kết nối từ địa chỉ IP `192.168.1.100` đến cổng 22.

**Ví dụ:**
- Nếu bạn muốn chặn kết nối SSH từ một địa chỉ IP cụ thể, chẳng hạn `192.168.1.100`, bạn có thể dùng lệnh trên để ngừng truy cập từ IP đó.

---

### 4. **Chặn cổng cho tất cả các giao diện mạng (Interface)**

Để chặn tất cả các kết nối đến một cổng từ mọi giao diện mạng (ví dụ cổng 8080), bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```
**Giải thích:**
- `-p tcp`: Giao thức TCP.
- `--dport 8080`: Cổng đích là 8080 (cổng HTTP alternative).
- `-j DROP`: Từ chối tất cả các gói tin đến cổng 8080.

**Ví dụ:**
- Nếu bạn muốn chặn tất cả các kết nối đến cổng 8080 (thường dùng cho các ứng dụng web khác), bạn có thể dùng lệnh này.

---

### 5. **Chặn cổng từ tất cả các địa chỉ IP ngoại trừ một IP cụ thể**

Để chặn một cổng (ví dụ cổng 443 - HTTPS) từ tất cả các địa chỉ IP ngoại trừ một địa chỉ IP cụ thể (ví dụ `192.168.1.10`), bạn có thể làm như sau:

```bash
# Chặn tất cả kết nối đến cổng 443
sudo iptables -A INPUT -p tcp --dport 443 -j DROP

# Cho phép kết nối từ IP cụ thể
sudo iptables -A INPUT -p tcp --dport 443 -s 192.168.1.10 -j ACCEPT
```
**Giải thích:**
- Quy tắc đầu tiên sẽ chặn tất cả các kết nối đến cổng 443.
- Quy tắc thứ hai sẽ cho phép kết nối từ `192.168.1.10` đến cổng 443, ngay cả khi quy tắc đầu tiên đã chặn nó.

**Ví dụ:**
- Bạn muốn chặn tất cả các kết nối HTTPS từ bên ngoài, nhưng vẫn cho phép địa chỉ IP nội bộ (như `192.168.1.10`) kết nối vào cổng này.

---

### 6. **Chặn tất cả các kết nối đến cổng từ một địa chỉ IP**

Nếu bạn muốn chặn tất cả các kết nối đến bất kỳ cổng nào từ một địa chỉ IP cụ thể, chẳng hạn `192.168.1.100`, sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
**Giải thích:**
- `-s 192.168.1.100`: Chỉ định địa chỉ IP nguồn.
- `-j DROP`: Từ chối tất cả các kết nối từ IP `192.168.1.100` đến hệ thống của bạn.

**Ví dụ:**
- Nếu bạn muốn chặn tất cả các kết nối từ địa chỉ IP `192.168.1.100` vào hệ thống của bạn (bất kể cổng nào), bạn có thể dùng lệnh trên.

---

### 7. **Chặn một dải cổng TCP hoặc UDP**

Để chặn một dải cổng (ví dụ cổng từ 1000 đến 2000), bạn có thể sử dụng lệnh:

```bash
sudo iptables -A INPUT -p tcp --dport 1000:2000 -j DROP
```
**Giải thích:**
- `--dport 1000:2000`: Chặn tất cả các cổng trong dải từ 1000 đến 2000.
- `-p tcp`: Giao thức TCP.

**Ví dụ:**
- Nếu bạn muốn ngừng tất cả các kết nối đến các cổng từ 1000 đến 2000, sử dụng lệnh này.

---

### 8. **Xóa Quy Tắc Chặn Cổng**

Để xóa một quy tắc đã chặn cổng (ví dụ cổng 80 TCP), bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -D INPUT -p tcp --dport 80 -j DROP
```
**Giải thích:**
- `-D INPUT`: Xóa quy tắc khỏi chuỗi `INPUT`.
- `-p tcp --dport 80`: Quy tắc chặn cổng 80 (HTTP).

---

### 9. **Lưu Quy Tắc iptables**
Sau khi cấu hình các quy tắc, bạn cần lưu lại để chúng không bị mất khi hệ thống khởi động lại. Bạn có thể lưu các quy tắc với lệnh sau:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```
Hoặc sử dụng công cụ `iptables-persistent` để lưu lại quy tắc tự động sau mỗi lần khởi động.

---

### 10. **Kiểm tra các Quy Tắc iptables**

Để kiểm tra các quy tắc hiện tại trong `iptables`, sử dụng lệnh:

```bash
sudo iptables -L -n -v
```
**Giải thích:**
- `-L`: Liệt kê tất cả các quy tắc.
- `-n`: Hiển thị địa chỉ IP và cổng dưới dạng số, không phân giải tên.
- `-v`: Hiển thị chi tiết về số lượng gói tin và byte bị tác động.

------------------------------------

### **Chặn hết chỉ mở 1 port**

Để **chặn tất cả các kết nối** đến hệ thống của bạn và **chỉ mở một cổng duy nhất**, bạn có thể làm theo các bước dưới đây. Sau đó, tôi cũng sẽ hướng dẫn cách **mở lại các cổng đã chặn** khi cần thiết.

### 1. **Chặn tất cả các kết nối chỉ mở một cổng duy nhất**

Giả sử bạn muốn **chặn tất cả các kết nối** và chỉ mở cổng 80 (HTTP). Dưới đây là các lệnh cụ thể:

#### 1.1. **Chặn tất cả các kết nối đến hệ thống**

Lệnh này sẽ chặn tất cả các kết nối đến hệ thống của bạn:

```bash
sudo iptables -A INPUT -j DROP
```

- `-A INPUT`: Thêm quy tắc vào chuỗi `INPUT`, có nghĩa là xử lý các gói tin đến hệ thống.
- `-j DROP`: Từ chối tất cả các gói tin, tức là không cho phép kết nối nào.

#### 1.2. **Mở một cổng duy nhất (ví dụ cổng 80 - HTTP)**

Tiếp theo, bạn mở cổng 80 để cho phép các kết nối đến dịch vụ HTTP:

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

- `-p tcp`: Giao thức TCP.
- `--dport 80`: Cổng đích là 80 (HTTP).
- `-j ACCEPT`: Cho phép các gói tin đến cổng 80.

#### 1.3. **Mở thêm cổng khác nếu cần (Tùy chọn)**

Nếu bạn muốn mở thêm các cổng khác (ví dụ như cổng 443 cho HTTPS), bạn có thể thực hiện thêm lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

#### 1.4. **Lưu quy tắc iptables**

Để lưu các quy tắc này và đảm bảo chúng không bị mất sau khi khởi động lại hệ thống, bạn cần sử dụng lệnh sau (tùy vào hệ thống của bạn):

- Trên Ubuntu/Debian:
  ```bash
  sudo iptables-save > /etc/iptables/rules.v4
  ```
  
- Hoặc sử dụng `iptables-persistent`:
  ```bash
  sudo apt-get install iptables-persistent
  sudo netfilter-persistent save
  ```

#### 1.5. **Kiểm tra các quy tắc**

Để kiểm tra các quy tắc hiện tại, bạn có thể dùng lệnh:

```bash
sudo iptables -L -n -v
```

### 2. **Cách mở lại tất cả các cổng đã chặn**

Nếu bạn muốn **mở lại tất cả các cổng** (đặt lại cấu hình để không chặn nữa), bạn có thể thực hiện các bước sau:

#### 2.1. **Xóa tất cả các quy tắc iptables**

Để **xóa tất cả các quy tắc** trong iptables (kể cả quy tắc chặn và quy tắc mở cổng), bạn có thể sử dụng lệnh:

```bash
sudo iptables -F
```

- `-F`: Xóa tất cả các quy tắc trong iptables.

#### 2.2. **Thiết lập lại chính sách mặc định**

Sau khi xóa quy tắc, bạn có thể thiết lập lại **chính sách mặc định** của iptables để cho phép tất cả các kết nối (mở hết các cổng):

```bash
sudo iptables -P INPUT ACCEPT
sudo iptables -P FORWARD ACCEPT
sudo iptables -P OUTPUT ACCEPT
```

- `-P INPUT ACCEPT`: Cho phép tất cả các kết nối đến (INPUT).
- `-P FORWARD ACCEPT`: Cho phép tất cả các kết nối chuyển tiếp (FORWARD).
- `-P OUTPUT ACCEPT`: Cho phép tất cả các kết nối đi ra (OUTPUT).

#### 2.3. **Lưu lại cấu hình mới**

Sau khi mở lại tất cả các cổng và thay đổi chính sách, bạn cần **lưu lại** cấu hình để nó không bị mất khi khởi động lại:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```

-------------------------------------

Để **chặn kết nối SSH** từ các địa chỉ IP cụ thể sử dụng `iptables`, bạn có thể làm theo các bước sau:

### 1. **Chặn kết nối SSH từ một địa chỉ IP cụ thể**

Giả sử bạn muốn chặn kết nối SSH (cổng 22) từ một địa chỉ IP cụ thể (ví dụ `192.168.1.100`), bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.100 -j DROP
```

**Giải thích:**
- `-A INPUT`: Thêm quy tắc vào chuỗi `INPUT`, tức là xử lý các gói tin đến hệ thống.
- `-p tcp`: Chỉ định giao thức TCP (SSH sử dụng TCP).
- `--dport 22`: Cổng đích là 22 (cổng SSH).
- `-s 192.168.1.100`: Địa chỉ IP nguồn là `192.168.1.100` (IP bạn muốn chặn).
- `-j DROP`: Từ chối kết nối từ IP `192.168.1.100` đến cổng 22.

### 2. **Chặn tất cả kết nối SSH từ một dải địa chỉ IP**

Nếu bạn muốn chặn tất cả các kết nối SSH từ một dải IP cụ thể (ví dụ dải `192.168.1.0/24`), bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j DROP
```

**Giải thích:**
- `-s 192.168.1.0/24`: Dải địa chỉ IP từ `192.168.1.0` đến `192.168.1.255`.

### 3. **Chặn kết nối SSH từ tất cả các địa chỉ IP ngoại trừ một địa chỉ IP cụ thể**

Giả sử bạn muốn **chặn tất cả các kết nối SSH từ mọi địa chỉ IP**, nhưng chỉ cho phép một địa chỉ IP cụ thể (ví dụ `192.168.1.10`), bạn có thể thực hiện như sau:

#### 3.1. **Chặn tất cả các kết nối SSH**
```bash
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```

#### 3.2. **Cho phép kết nối SSH từ địa chỉ IP cụ thể**
```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.10 -j ACCEPT
```

**Giải thích:**
- Quy tắc đầu tiên sẽ chặn tất cả các kết nối SSH.
- Quy tắc thứ hai sẽ cho phép kết nối từ `192.168.1.10`.

### 4. **Chặn kết nối SSH từ tất cả các địa chỉ IP (Hoàn toàn ngừng dịch vụ SSH)**

Nếu bạn muốn **chặn hoàn toàn dịch vụ SSH**, tức là không cho phép bất kỳ kết nối SSH nào từ bất kỳ địa chỉ IP nào, sử dụng lệnh sau:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```

**Giải thích:**
- Quy tắc này sẽ từ chối tất cả các kết nối đến cổng 22 (SSH).

### 5. **Xóa các quy tắc đã thêm**

Nếu bạn muốn **xóa** một quy tắc đã thêm vào iptables (ví dụ quy tắc chặn SSH từ `192.168.1.100`), bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -D INPUT -p tcp --dport 22 -s 192.168.1.100 -j DROP
```

**Giải thích:**
- `-D INPUT`: Xóa quy tắc từ chuỗi `INPUT`.

### 6. **Lưu quy tắc iptables**

Sau khi đã cấu hình xong các quy tắc iptables, để quy tắc có hiệu lực sau khi khởi động lại hệ thống, bạn cần lưu lại:

- Trên Ubuntu/Debian, bạn có thể sử dụng lệnh sau:
  ```bash
  sudo iptables-save > /etc/iptables/rules.v4
  ```

- Hoặc sử dụng `iptables-persistent` để lưu quy tắc tự động:
  ```bash
  sudo apt-get install iptables-persistent
  sudo netfilter-persistent save
  ```

### 7. **Kiểm tra các quy tắc iptables**

Để kiểm tra các quy tắc đã thiết lập, bạn có thể sử dụng lệnh:

```bash
sudo iptables -L -n -v
```

------------------------------------------------------------------------

Để **mở SSH** chỉ từ một số địa chỉ IP cụ thể và **chặn tất cả các kết nối SSH** từ các địa chỉ khác, bạn có thể thực hiện như sau:

Giả sử bạn chỉ muốn **cho phép kết nối SSH từ các địa chỉ IP cụ thể** (ví dụ: `192.168.1.10`, `192.168.1.20`, và `192.168.1.30`), và **chặn tất cả các kết nối SSH từ các địa chỉ IP khác**.

### 1. **Chặn tất cả các kết nối SSH**

Trước tiên, bạn cần **chặn tất cả các kết nối SSH** (cổng 22) để đảm bảo rằng các kết nối từ IP không được phép sẽ bị từ chối:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j DROP
```

**Giải thích:**
- `-A INPUT`: Thêm quy tắc vào chuỗi `INPUT`, tức là xử lý các gói tin đến hệ thống.
- `-p tcp`: Chỉ định giao thức TCP.
- `--dport 22`: Cổng đích là 22 (cổng SSH).
- `-j DROP`: Từ chối tất cả các kết nối đến cổng 22 (SSH).

### 2. **Cho phép kết nối SSH từ các địa chỉ IP cụ thể**

Tiếp theo, bạn cho phép kết nối SSH từ các địa chỉ IP cụ thể mà bạn muốn. Ví dụ, cho phép từ các IP `192.168.1.10`, `192.168.1.20`, và `192.168.1.30`:

```bash
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.10 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.20 -j ACCEPT
sudo iptables -A INPUT -p tcp --dport 22 -s 192.168.1.30 -j ACCEPT
```

**Giải thích:**
- `-s 192.168.1.10`: Địa chỉ IP nguồn mà bạn muốn cho phép kết nối.
- `-j ACCEPT`: Cho phép các kết nối từ địa chỉ IP này đến cổng 22.

### 3. **Lưu các quy tắc iptables**

Để đảm bảo các quy tắc vẫn được áp dụng sau khi hệ thống khởi động lại, bạn cần lưu các quy tắc iptables. Đối với Ubuntu/Debian, sử dụng lệnh sau:

```bash
sudo iptables-save > /etc/iptables/rules.v4
```

Hoặc bạn có thể sử dụng `iptables-persistent`:

```bash
sudo apt-get install iptables-persistent
sudo netfilter-persistent save
```

### 4. **Kiểm tra các quy tắc iptables**

Để kiểm tra các quy tắc đã thiết lập, bạn có thể sử dụng lệnh sau:

```bash
sudo iptables -L -n -v
```

### 5. **Xóa các quy tắc nếu cần**

Nếu bạn muốn xóa một quy tắc cụ thể (ví dụ, xóa quy tắc chặn SSH từ `192.168.1.10`), bạn có thể sử dụng lệnh:

```bash
sudo iptables -D INPUT -p tcp --dport 22 -s 192.168.1.10 -j ACCEPT
```


