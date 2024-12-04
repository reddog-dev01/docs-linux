### Cơ Chế Hoạt Động của Iptables

**Iptables** là một công cụ quản lý tường lửa trên hệ thống Linux, giúp kiểm soát lưu lượng mạng đi qua hệ thống dựa trên các quy tắc mà bạn định nghĩa. Cơ chế hoạt động của iptables có thể được mô tả như sau:

#### **1. Các Bảng (Tables) trong Iptables**
Iptables sử dụng **bảng** để phân loại các quy tắc. Mỗi bảng có mục đích khác nhau:

- **Filter Table**: Đây là bảng mặc định, được dùng để kiểm soát truy cập mạng. Nó quản lý các chuỗi `INPUT`, `OUTPUT`, và `FORWARD`:
  - `INPUT`: Quy tắc này áp dụng cho các gói tin đến máy tính (máy chủ).
  - `OUTPUT`: Quy tắc này áp dụng cho các gói tin đi ra khỏi máy tính (máy chủ).
  - `FORWARD`: Quy tắc này áp dụng cho các gói tin được chuyển tiếp qua máy tính (máy chủ) tới một máy tính khác.
  
- **NAT Table**: Dùng để thực hiện NAT (Network Address Translation), thường được dùng để thay đổi địa chỉ IP trong các gói tin khi chuyển tiếp qua router hoặc gateway.
  - Các chuỗi trong NAT: `PREROUTING`, `POSTROUTING`, và `OUTPUT`.
  
- **Mangle Table**: Dùng để thay đổi các thuộc tính của gói tin, như TTL (Time To Live), TOS (Type of Service), hoặc các trường khác trong gói tin.

- **Raw Table**: Được sử dụng để miễn trừ các gói tin khỏi việc theo dõi (connection tracking).

#### **2. Các Chuỗi (Chains) trong Iptables**
Mỗi bảng chứa các chuỗi, các chuỗi này là nơi lưu trữ các quy tắc lọc gói tin. Mỗi chuỗi có một mục đích cụ thể:

- **INPUT**: Quy tắc dành cho các gói tin đến máy chủ.
- **OUTPUT**: Quy tắc dành cho các gói tin đi từ máy chủ.
- **FORWARD**: Quy tắc dành cho các gói tin chuyển tiếp qua máy chủ.
- **PREROUTING** và **POSTROUTING** (chỉ có trong NAT và Mangle): Dùng để thay đổi hoặc điều hướng các gói tin khi chúng đi qua máy chủ.

#### **3. Các Quy Tắc trong Iptables**
Mỗi quy tắc trong iptables là một điều kiện mà gói tin phải thỏa mãn, để quyết định xem nó có được phép đi qua hay không. Các quy tắc được cấu hình để chấp nhận (ACCEPT), từ chối (DROP), hay tiếp tục kiểm tra các quy tắc khác (RETURN).

#### **4. Các Quy Tắc Lọc Gói Tin**
Khi một gói tin đến hệ thống, iptables sẽ kiểm tra chuỗi của bảng filter (mặc định) để quyết định xem gói tin đó có được phép đi qua không. Dưới đây là các hành động mà bạn có thể cấu hình trong iptables:
- **ACCEPT**: Chấp nhận gói tin và cho phép nó tiếp tục.
- **DROP**: Từ chối gói tin và không gửi thông báo về việc từ chối.
- **REJECT**: Từ chối gói tin và gửi thông báo về việc từ chối.
- **LOG**: Ghi lại gói tin (nếu bạn muốn theo dõi).
- **RETURN**: Dừng kiểm tra trong chuỗi và chuyển sang chuỗi khác.

### Cách Cấu Hình Iptables

Để cấu hình iptables, bạn cần quyền root (quản trị viên). Dưới đây là hướng dẫn chi tiết về cách thêm, xem, và xóa các quy tắc trong iptables.

#### **1. Xem Các Quy Tắc Hiện Tại**
Để liệt kê các quy tắc iptables đang hoạt động:
```bash
sudo iptables -L -n -v
```
- `-L`: Liệt kê các quy tắc.
- `-n`: Hiển thị địa chỉ IP và cổng bằng số, không chuyển thành tên.
- `-v`: Hiển thị thêm chi tiết.

#### **2. Thêm Quy Tắc**
Bạn có thể thêm quy tắc vào các chuỗi khác nhau tùy theo mục đích sử dụng.

##### **Ví dụ 1: Chặn IP**
Nếu bạn muốn chặn địa chỉ IP `192.168.1.100` gửi yêu cầu đến máy tính của mình, bạn có thể sử dụng quy tắc sau:
```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
- `-A INPUT`: Thêm quy tắc vào chuỗi INPUT.
- `-s 192.168.1.100`: Quy tắc áp dụng cho gói tin có địa chỉ nguồn là `192.168.1.100`.
- `-j DROP`: Từ chối (DROP) các gói tin này.

##### **Ví dụ 2: Cho phép kết nối SSH**
Để cho phép kết nối SSH từ các máy tính khác, bạn có thể thêm quy tắc sau:
```bash
sudo iptables -A INPUT -p tcp --dport 22 -m conntrack --ctstate NEW,ESTABLISHED -j ACCEPT
```
- `-A INPUT`: Thêm quy tắc vào chuỗi INPUT.
- `-p tcp`: Sử dụng giao thức TCP.
- `--dport 22`: Chỉ định cổng đích là cổng 22 (cổng mặc định của SSH).
- `-m conntrack --ctstate NEW,ESTABLISHED`: Sử dụng module conntrack để cho phép các kết nối mới và đã thiết lập.
- `-j ACCEPT`: Cho phép các gói tin này.

##### **Ví dụ 3: Cho phép Ping**
Để cho phép các gói tin ICMP (Ping), bạn có thể thêm quy tắc sau:
```bash
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT
```
- `-p icmp`: Chỉ định giao thức ICMP.
- `--icmp-type echo-request`: Cho phép loại gói tin `echo-request` (gói tin Ping).
- `-j ACCEPT`: Cho phép gói tin này.

#### **3. Xóa Quy Tắc**
Để xóa một quy tắc, bạn có thể sử dụng lệnh `-D` thay vì `-A`:
```bash
sudo iptables -D INPUT -s 192.168.1.100 -j DROP
```
Điều này sẽ xóa quy tắc chặn IP `192.168.1.100` mà bạn đã thêm trước đó.

#### **4. Lưu Quy Tắc**
Khi bạn cấu hình iptables, các quy tắc này sẽ bị mất khi hệ thống khởi động lại. Để lưu các quy tắc, bạn có thể sử dụng công cụ `iptables-persistent`.

Cài đặt `iptables-persistent` để tự động lưu cấu hình khi hệ thống khởi động lại:
```bash
sudo apt-get install iptables-persistent
```
Khi bạn cài đặt, hệ thống sẽ yêu cầu bạn có muốn lưu các quy tắc hiện tại không, chọn **Yes** để lưu.

#### **5. Thiết Lập Chính Sách Mặc Định**
Nếu bạn muốn cấu hình chính sách mặc định cho các chuỗi như `INPUT`, `OUTPUT`, hoặc `FORWARD`, bạn có thể thay đổi chính sách mặc định để từ chối hoặc chấp nhận tất cả các gói tin.

- **Chính sách mặc định là từ chối tất cả**:
  ```bash
  sudo iptables -P INPUT DROP
  sudo iptables -P FORWARD DROP
  sudo iptables -P OUTPUT ACCEPT
  ```

  Điều này có nghĩa là mặc định tất cả các gói tin đến (INPUT) và chuyển tiếp (FORWARD) đều bị từ chối, chỉ các gói tin đi ra (OUTPUT) mới được phép.

#### **6. Reset Iptables**
Nếu bạn muốn xóa tất cả các quy tắc và trở về trạng thái ban đầu:
```bash
sudo iptables -F
```
- `-F`: Xóa tất cả các quy tắc.

### Tóm Lại:
Iptables là công cụ quản lý tường lửa mạnh mẽ trên hệ thống Linux, cho phép bạn kiểm soát lưu lượng mạng đi vào và đi ra qua các quy tắc linh hoạt. Việc hiểu rõ cơ chế hoạt động của các bảng và chuỗi trong iptables giúp bạn cấu hình và quản lý các quy tắc bảo mật một cách hiệu quả, bảo vệ hệ thống khỏi các mối đe dọa từ mạng bên ngoài.
