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

