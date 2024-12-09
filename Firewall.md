### **`IPTABLES`**

- `iptables` là một công cụ dòng lệnh trong Linux dùng để cấu hình tường lửa (firewall) và lọc các gói tin trong hệ thống mạng. Nó cho phép bạn quản lý các quy tắc (rules) kiểm tra và điều khiển lưu lượng mạng, từ đó bảo vệ hệ thống của bạn khỏi các mối đe dọa từ bên ngoài và điều chỉnh cách dữ liệu được gửi qua mạng.

### **Các thành phần của `iptables`**
Các thành phần chính của `iptables` bao gồm:

1. **Bảng (Tables)**:
Mỗi bảng chứa các chuỗi và quy tắc xử lý gói tin. Các bảng chính trong `iptables` là:
- **filter**: Bảng mặc định dùng để lọc gói tin (cho phép hoặc từ chối). Đây là bảng chủ yếu khi bạn muốn kiểm tra và kiểm soát lưu lượng mạng.
- **nat (Network Address Translation)**: Dùng để thay đổi địa chỉ IP của các gói tin (thường dùng cho NAT, ví dụ chuyển tiếp gói tin qua router, hay chia sẻ kết nối internet).
- **mangle**: Dùng để thay đổi các thuộc tính của gói tin (như thay đổi TTL, QoS, v.v.).
- **raw**: Thực hiện xử lý gói tin trước khi chúng được xử lý bởi các bảng khác, thường dùng để bỏ qua kiểm tra trạng thái kết nối.
- **security**: Dùng trong SELinux (Security-Enhanced Linux) để áp dụng các chính sách bảo mật.

2. **Chuỗi (Chains)**:
Mỗi bảng có một hoặc nhiều chuỗi, mỗi chuỗi chứa các quy tắc để xử lý gói tin. Các chuỗi chính bao gồm:
- **INPUT**: Dùng để kiểm tra các gói tin đi vào máy chủ.
- **OUTPUT**: Dùng để kiểm tra các gói tin xuất phát từ máy chủ.
- **FORWARD**: Dùng để kiểm tra các gói tin được chuyển tiếp qua máy chủ (dùng trong các thiết lập routing).
- **PREROUTING**: Dùng trong bảng `nat` để xử lý gói tin ngay khi chúng vào hệ thống, trước khi được định tuyến.
- **POSTROUTING**: Dùng trong bảng `nat` để xử lý gói tin sau khi chúng đã được định tuyến, trước khi rời khỏi hệ thống.

3. **Quy tắc (Rules)**:
Mỗi quy tắc trong chuỗi kiểm tra một hoặc nhiều điều kiện của gói tin (như địa chỉ IP, cổng, giao thức, v.v.). Nếu gói tin khớp với quy tắc, hành động chỉ định sẽ được thực thi, ví dụ:
- **ACCEPT**: Cho phép gói tin tiếp tục.
- **DROP**: Từ chối gói tin mà không gửi thông báo.
- **REJECT**: Từ chối gói tin và gửi một thông báo lỗi.
- **LOG**: Ghi lại thông tin gói tin mà không thay đổi.

4. **Mô-đun (Modules)**:
`iptables` sử dụng các mô-đun để mở rộng khả năng lọc và xử lý gói tin. Các mô-đun này cho phép bạn kiểm tra các điều kiện bổ sung như địa chỉ IP, cổng, giao thức, trạng thái kết nối, v.v. Ví dụ:
- **state**: Kiểm tra trạng thái của kết nối (new, established, related).
- **tcp**: Kiểm tra các gói tin TCP, ví dụ như cổng hoặc flags của gói tin.
- **limit**: Giới hạn số lượng gói tin trong một khoảng thời gian nhất định.
  
5. **Hành động (Targets)**:
Mỗi quy tắc có thể có một hành động đi kèm, quyết định việc xử lý gói tin:
- **ACCEPT**: Cho phép gói tin tiếp tục.
- **DROP**: Từ chối gói tin mà không thông báo.
- **REJECT**: Từ chối gói tin và gửi thông báo lỗi.
- **LOG**: Ghi lại thông tin gói tin vào nhật ký.
- **SNAT/DNAT**: Chuyển đổi địa chỉ nguồn hoặc đích của gói tin trong bảng `nat`.
- **MASQUERADE**: Dùng trong NAT để tự động thay đổi địa chỉ nguồn của gói tin khi ra ngoài.

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

