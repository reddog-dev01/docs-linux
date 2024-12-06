### **ip link**

Lệnh `ip link` trong Linux là một công cụ mạnh mẽ để quản lý các giao diện mạng trên hệ thống. Dưới đây là cách sử dụng `ip link` cùng các tuỳ chọn phổ biến trong Linux:

**Cấu trúc lệnh cơ bản:**
```bash
ip link [OPTION] [INTERFACE]
```

1. **Index và Tên Giao Diện**
   - **Ví dụ**: `2: eth0:`
   - **Index (Chỉ số)**: Là số định danh duy nhất cho mỗi giao diện mạng trên hệ thống.
   - **Tên Giao Diện**: Tên gán cho giao diện mạng, ví dụ như `eth0` cho Ethernet, `wlan0` cho Wi-Fi.

2. **Trạng thái Giao Diện**
   - **Ví dụ**: `<BROADCAST,MULTICAST,UP,LOWER_UP>`
   - **BROADCAST**: Cho phép giao diện thực hiện gửi thông tin tới tất cả các máy trong một mạng.
   - **MULTICAST**: Cho phép giao diện gửi thông tin đến một nhóm các địa chỉ.
   - **UP**: Giao diện đang hoạt động (kích hoạt).
   - **LOWER_UP**: Có kết nối vật lý và sẵn sàng giao tiếp (chỉ ra rằng lớp dưới (phần cứng) của giao diện đang hoạt động).

3. **MTU (Maximum Transmission Unit)**
   - **Ví dụ**: `mtu 1500`
   - MTU là kích thước tối đa của một gói tin mà giao diện này có thể gửi hoặc nhận, tính bằng byte.

4. **Discipline xếp hàng đợi (qdisc)**
   - **Ví dụ**: `qdisc fq_codel`
   - Là thuật toán điều khiển hàng đợi được sử dụng để quản lý cách các gói dữ liệu được xử lý và gửi đi trên giao diện. `fq_codel` là một trong những thuật toán nhằm giảm độ trễ và tránh tắc nghẽn mạng.

5. **Trạng Thái (State)**
   - **Ví dụ**: `state UP`
   - Chỉ trạng thái hoạt động của giao diện: `UP` nghĩa là giao diện đang hoạt động và `DOWN` nghĩa là giao diện không hoạt động.

6. **Địa Chỉ MAC (Media Access Control)**
   - **Ví dụ**: `link/ether 00:0c:29:5b:3d:94`
   - Là địa chỉ vật lý duy nhất được gán cho mỗi giao diện mạng, dùng để nhận diện trên mạng LAN.

7. **Địa chỉ Broadcast**
   - **Ví dụ**: `brd ff:ff:ff:ff:ff:ff`
   - Đây là địa chỉ dùng để gửi gói tin đến tất cả các thiết bị trong một mạng hoặc một phân đoạn mạng.

8. **Độ dài hàng đợi (QLen)**
   - **Ví dụ**: `qlen 1000`
   - Là số lượng gói tin tối đa mà hàng đợi của giao diện có thể chứa trước khi xử lý. Giá trị này có ảnh hưởng đến việc xử lý tắc nghẽn mạng.


### Các tuỳ chọn phổ biến của `ip link`:

1. **Hiển thị danh sách tất cả các giao diện mạng:**
   ```bash
   ip link
   ```
   Lệnh này hiển thị tất cả các giao diện mạng, bao gồm thông tin về trạng thái (UP/DOWN), địa chỉ MAC, giao thức, và các thông tin liên quan.

2. **Hiển thị chi tiết một giao diện mạng:**
   ```bash
   ip link show [interface]
   ```
   Ví dụ: Xem thông tin chi tiết của giao diện `ens33`:
   ```bash
   ip link show ens33
   ```

3. **Bật giao diện mạng (UP):**
   ```bash
   sudo ip link set [interface] up
   ```
   Ví dụ: Để bật giao diện `ens33`:
   ```bash
   sudo ip link set ens33 up
   ```

4. **Tắt giao diện mạng (DOWN):**
   ```bash
   sudo ip link set [interface] down
   ```
   Ví dụ: Để tắt giao diện `ens33`:
   ```bash
   sudo ip link set ens33 down
   ```

5. **Đổi tên giao diện mạng:**
   ```bash
   sudo ip link set [old_interface] name [new_interface]
   ```
   Ví dụ: Đổi tên giao diện `ens33` thành `eth0`:
   ```bash
   sudo ip link set ens33 name eth0
   ```

6. **Đổi địa chỉ MAC của giao diện mạng:**
   ```bash
   sudo ip link set [interface] address [new_mac_address]
   ```
   Ví dụ: Đặt địa chỉ MAC cho giao diện `ens33`:
   ```bash
   sudo ip link set ens33 address 00:11:22:33:44:55
   ```

7. **Hiển thị địa chỉ MAC của giao diện mạng:**
   ```bash
   ip link show [interface]
   ```
   Lệnh này sẽ hiển thị địa chỉ MAC của giao diện mạng.

8. **Chuyển giao diện sang chế độ promiscuous (chế độ chấp nhận mọi gói tin):**
   ```bash
   sudo ip link set [interface] promisc on
   ```
   Để bật chế độ promiscuous cho giao diện `ens33`:
   ```bash
   sudo ip link set ens33 promisc on
   ```

9. **Tắt chế độ promiscuous của giao diện:**
   ```bash
   sudo ip link set [interface] promisc off
   ```
   Để tắt chế độ promiscuous cho giao diện `ens33`:
   ```bash
   sudo ip link set ens33 promisc off
   ```

10. **Kiểm tra trạng thái của giao diện mạng:**
    - Để xem thông tin cơ bản, bao gồm trạng thái (UP/DOWN):
      ```bash
      ip link show
      ```
    - Để xem thông tin chi tiết về giao diện mạng:
      ```bash
      ip addr show [interface]
      ```

11. **Chỉ hiển thị trạng thái của giao diện (UP/DOWN):**
    ```bash
    ip link show [interface] | grep -i "state"
    ```
    Ví dụ: Kiểm tra trạng thái giao diện `ens33`:
    ```bash
    ip link show ens33 | grep -i "state"
    ```

Ví dụ:

1. **Hiển thị thông tin tất cả các giao diện mạng:**
   ```bash
   ip link
   ```

2. **Hiển thị chi tiết giao diện `ens33`:**
   ```bash
   ip link show ens33
   ```

3. **Bật giao diện `ens33`:**
   ```bash
   sudo ip link set ens33 up
   ```

4. **Tắt giao diện `ens33`:**
   ```bash
   sudo ip link set ens33 down
   ```

5. **Đổi tên giao diện từ `ens33` thành `eth0`:**
   ```bash
   sudo ip link set ens33 name eth0
   ```

6. **Đặt địa chỉ MAC mới cho giao diện `ens33`:**
   ```bash
   sudo ip link set ens33 address 00:11:22:33:44:55
   ```

7. **Kiểm tra trạng thái của giao diện `ens33`:**
   ```bash
   ip link show ens33
   ```

--------------------------------------------------------------------------------

### **ip route**

Lệnh `ip route` được sử dụng để **xem và quản lý bảng định tuyến (routing table)** trong Linux. Bảng định tuyến chứa thông tin về các tuyến đường mà hệ thống sử dụng để định hướng lưu lượng mạng tới đích. Đây là một phần quan trọng trong việc quản lý mạng trên các hệ thống Linux.

**Cấu trúc cơ bản của lệnh `ip route`:**

```bash
ip route
```

Khi chạy lệnh này, bạn sẽ thấy bảng định tuyến hiện tại của hệ thống.

**Các thành phần trong kết quả của lệnh `ip route`:**

1. **Destination (Đích)**
- **Mô tả**: Đây là địa chỉ mạng hoặc mạng con mà tuyến đường này áp dụng. 
- **Định dạng**: Địa chỉ IP hoặc mạng con, có thể có phần subnet mask.
  - Ví dụ: `192.168.1.0/24` (mạng con) hoặc `default` (địa chỉ mặc định).
  
2. **Gateway (Cổng)**
- **Mô tả**: Đây là địa chỉ IP của thiết bị tiếp theo (gateway) mà hệ thống sẽ gửi gói dữ liệu tới nếu không có tuyến đường trực tiếp tới đích.
- **Định dạng**: Địa chỉ IP của cổng (gateway).
  - Ví dụ: `via 192.168.1.1`.

3. **Interface (Giao diện)**
- **Mô tả**: Đây là tên của giao diện mạng mà hệ thống sẽ sử dụng để gửi các gói dữ liệu đến đích.
- **Định dạng**: Tên của giao diện mạng, như `eth0`, `wlan0`, `ens33`, v.v.
  - Ví dụ: `dev eth0`.

4. **Metric**
- **Mô tả**: Đây là giá trị ưu tiên của tuyến đường. Nếu có nhiều tuyến đường tới cùng một đích, hệ thống sẽ chọn tuyến đường có **metric** thấp nhất. Giá trị này giúp quyết định tuyến đường nào sẽ được ưu tiên nếu có nhiều tuyến đường có sẵn.
- **Định dạng**: Một số nguyên, ví dụ: `metric 100`.
  
5. **Scope**
- **Mô tả**: Thông tin về phạm vi của tuyến đường. Phạm vi này giúp xác định phạm vi áp dụng của tuyến đường.
  - **`link`**: Tuyến đường chỉ áp dụng cho mạng cục bộ (local network) và không được chuyển tiếp ra ngoài (chỉ áp dụng trên cùng một mạng).
  - **`global`**: Tuyến đường có thể được chuyển tiếp tới các hệ thống mạng khác.
  - **`site`**: Tuyến đường có thể áp dụng cho các mạng ở phạm vi site hoặc địa phương.
  
6. **Src (Source)**
- **Mô tả**: Đây là địa chỉ IP nguồn (source IP) mà hệ thống sẽ sử dụng khi gửi gói dữ liệu tới đích. Điều này đặc biệt quan trọng trong các trường hợp nhiều địa chỉ IP hoặc giao diện mạng.
- **Định dạng**: Địa chỉ IP của nguồn (source IP).
  - Ví dụ: `src 192.168.1.100`.

7. **Proto (Protocol)**
- **Mô tả**: Phương thức hoặc giao thức được sử dụng để tạo ra tuyến đường đó. Nó có thể là:
  - `static`: Được cấu hình thủ công.
  - `dhcp`: Được cấp phát tự động qua DHCP.
  - `kernel`: Được hệ điều hành tự động tạo ra.

8. **Flags**
- **Mô tả**: Các cờ (flags) giúp mô tả các thuộc tính của tuyến đường, ví dụ như:
  - **`U`**: Tuyến đường đang sử dụng (Up).
  - **`H`**: Tuyến đường tới một host (chỉ có một địa chỉ IP cụ thể).
  - **`G`**: Tuyến đường đi qua gateway.

**Ví dụ kết quả của `ip route` và giải thích:**

```bash
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 scope link src 192.168.1.100
10.0.0.0/8 via 192.168.2.1 dev eth1
```

Giải thích từng dòng:

1. **`default via 192.168.1.1 dev eth0`**:
   - **default**: Đây là tuyến đường mặc định (default route).
   - **via 192.168.1.1**: Gói dữ liệu sẽ được gửi đến cổng 192.168.1.1 nếu không có tuyến đường cụ thể nào cho đích.
   - **dev eth0**: Tuyến đường này sẽ được sử dụng qua giao diện `eth0`.

2. **`192.168.1.0/24 dev eth0 scope link src 192.168.1.100`**:
   - **192.168.1.0/24**: Mạng đích là `192.168.1.0/24`.
   - **dev eth0**: Tuyến đường này được áp dụng qua giao diện `eth0`.
   - **scope link**: Tuyến đường này chỉ áp dụng cho mạng cục bộ (local network).
   - **src 192.168.1.100**: Địa chỉ IP nguồn sẽ là `192.168.1.100` khi gửi gói tới mạng này.

3. **`10.0.0.0/8 via 192.168.2.1 dev eth1`**:
   - **10.0.0.0/8**: Mạng đích là `10.0.0.0/8`.
   - **via 192.168.2.1**: Các gói dữ liệu sẽ đi qua gateway `192.168.2.1`.
   - **dev eth1**: Tuyến đường này sẽ được sử dụng qua giao diện `eth1`.

### Các tùy chọn phổ biến với `ip route`:

1. **Hiển thị bảng định tuyến chi tiết:**
   ```bash
   ip route show
   ```

2. **Thêm một tuyến đường (route):**
   ```bash
   sudo ip route add <network> via <gateway> dev <interface>
   ```
   Ví dụ:
   ```bash
   sudo ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
   ```

3. **Xóa một tuyến đường:**
   ```bash
   sudo ip route del <network> via <gateway> dev <interface>
   ```
   Ví dụ:
   ```bash
   sudo ip route del 192.168.2.0/24 via 192.168.1.1 dev eth0
   ```

4. **Đặt một tuyến đường mặc định (default route):**
   ```bash
   sudo ip route add default via <gateway>
   ```

5. **Thêm tuyến đường với metric (ưu tiên tuyến đường):**
   ```bash
   sudo ip route add <network> via <gateway> dev <interface> metric <value>
   ```

6. **Đổi gateway mặc định:**
   ```bash
   sudo ip route change default via <new-gateway>
   ```

---------------------------------------------------

### **ip address**

Lệnh `ip address show` là công cụ để hiển thị thông tin về các địa chỉ IP của các giao diện mạng trên hệ thống. Khi sử dụng lệnh này, bạn sẽ nhận được một số thông tin chi tiết về các giao diện mạng và các địa chỉ IP được gán cho chúng.

1. **Ý nghĩa các thông tin khi dùng `ip address show`**


Ví dụ:
```bash
2: eth0: <BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:feea:5e29/64 scope link 
       valid_lft forever preferred_lft forever
```

Giải thích các thành phần trong kết quả:
- **`2:`**: Đây là chỉ số của giao diện mạng trong hệ thống.
- **`eth0:`**: Tên của giao diện mạng (ở đây là `eth0`).
- **`<BROADCAST,MULTICAST,UP>`**: Các thuộc tính của giao diện:
  - **BROADCAST**: Giao diện hỗ trợ broadcast (phát sóng).
  - **MULTICAST**: Giao diện hỗ trợ multicast (phát nhiều địa chỉ).
  - **UP**: Giao diện mạng đang hoạt động.
- **`mtu 1500`**: Maximum Transmission Unit (MTU) là kích thước tối đa của gói dữ liệu có thể truyền qua giao diện mạng, ở đây là 1500 byte.
- **`qdisc pfifo_fast`**: Quản lý hàng đợi (queue discipline) cho giao diện, ở đây là `pfifo_fast` (FIFO - First In, First Out).
- **`state UP`**: Trạng thái của giao diện mạng, cho thấy giao diện đang hoạt động.
- **`group default`**: Nhóm giao diện mặc định.
- **`qlen 1000`**: Độ dài hàng đợi của giao diện mạng, chỉ số gói dữ liệu có thể xếp chờ.
  
Địa chỉ IP:
- **`inet 192.168.1.100/24`**: Địa chỉ IPv4 `192.168.1.100` được gán cho giao diện `eth0`, với subnet mask `/24` (tương đương `255.255.255.0`).
  - **`inet`**: Địa chỉ IPv4.
  - **`192.168.1.100`**: Địa chỉ IP của giao diện.
  - **`/24`**: Subnet mask, cho biết phần mạng của địa chỉ IP.
  
- **`brd 192.168.1.255`**: Địa chỉ broadcast cho mạng con.
  - **`brd`**: Địa chỉ broadcast.
  
- **`scope global`**: Phạm vi của địa chỉ IP, ở đây là **global**, có nghĩa là địa chỉ IP có thể truy cập từ toàn cầu.
  
- **`valid_lft forever preferred_lft forever`**: Thời gian sống của địa chỉ IP.
  - **`valid_lft`**: Thời gian mà địa chỉ IP có thể sử dụng.
  - **`preferred_lft`**: Thời gian ưu tiên của địa chỉ IP (khi hết thời gian này, địa chỉ IP có thể bị thay đổi).

Địa chỉ IPv6:
- **`inet6 fe80::a00:27ff:feea:5e29/64`**: Địa chỉ IPv6 liên kết (`link-local`), bắt đầu với `fe80::` và có subnet mask `/64`.
  - **`inet6`**: Địa chỉ IPv6.
  - **`fe80::a00:27ff:feea:5e29`**: Địa chỉ IPv6.
  - **`/64`**: Subnet mask IPv6.
  
- **`scope link`**: Phạm vi của địa chỉ IPv6, ở đây là **link-local**, có nghĩa là địa chỉ này chỉ có thể giao tiếp trong cùng một mạng con (local link).
  
- **`valid_lft forever preferred_lft forever`**: Thời gian sống của địa chỉ IPv6.

2. **Các option của lệnh `ip address`**

Lệnh `ip address` có một số option quan trọng để bạn có thể quản lý các địa chỉ IP của giao diện mạng:

a. **`show`**
Hiển thị thông tin về địa chỉ IP của tất cả các giao diện mạng hoặc một giao diện cụ thể.

- **Cú pháp**: 
  ```bash
  ip address show
  ```
  Hoặc:
  ```bash
  ip addr show
  ```
  
  Để hiển thị thông tin của một giao diện cụ thể:
  ```bash
  ip address show dev <interface>
  ```

b. **`add`**
Thêm một địa chỉ IP vào giao diện mạng.

- **Cú pháp**:
  ```bash
  ip address add <ip-address>/<netmask> dev <interface>
  ```
  Ví dụ:
  ```bash
  sudo ip address add 192.168.2.100/24 dev eth0
  ```

c. **`del`**
Xóa một địa chỉ IP khỏi giao diện mạng.

- **Cú pháp**:
  ```bash
  ip address del <ip-address>/<netmask> dev <interface>
  ```
  Ví dụ:
  ```bash
  sudo ip address del 192.168.2.100/24 dev eth0
  ```

d. **`flush`**
Xóa tất cả các địa chỉ IP khỏi một giao diện mạng.

- **Cú pháp**:
  ```bash
  sudo ip address flush dev <interface>
  ```
  Ví dụ:
  ```bash
  sudo ip address flush dev eth0
  ```

e. **`label`**
Đặt tên (label) cho giao diện mạng khi thêm hoặc sửa địa chỉ IP.

- **Cú pháp**:
  ```bash
  ip address add <ip-address>/<netmask> dev <interface> label <label-name>
  ```

f. **`primary`**
Đặt địa chỉ IP này là địa chỉ chính cho giao diện.

- **Cú pháp**:
  ```bash
  ip address add <ip-address>/<netmask> dev <interface> primary
  ```

3. **Các thành phần trong kết quả lệnh `ip address show`**

- **Giao diện mạng (`eth0`, `wlan0`, `lo`, ...)**
  - Tên của giao diện mạng.
- **`inet` (IPv4) và `inet6` (IPv6)**
  - Loại địa chỉ IP.
- **`scope`**
  - Phạm vi của địa chỉ IP (global, link-local, ...).
- **Địa chỉ IP**
  - Địa chỉ IP cụ thể gán cho giao diện mạng.
- **Subnet mask (`/24`, `/64`, ...)**
  - Định dạng subnet mask, cho biết phần mạng của địa chỉ.
- **Broadcast address**
  - Địa chỉ broadcast (chỉ dành cho IPv4).

4. **Các ví dụ**

- **Hiển thị thông tin địa chỉ IP của tất cả các giao diện mạng**:
  ```bash
  ip address show
  ```

- **Hiển thị thông tin địa chỉ IP của giao diện `eth0`**:
  ```bash
  ip address show dev eth0
  ```

- **Thêm địa chỉ IP mới vào giao diện `eth0`**:
  ```bash
  sudo ip address add 192.168.2.200/24 dev eth0
  ```

- **Xóa địa chỉ IP khỏi giao diện `eth0`**:
  ```bash
  sudo ip address del 192.168.2.200/24 dev eth0
  ```

-------------------------------------------

### **arp**

Lệnh `arp` (Address Resolution Protocol) là một công cụ trong Linux và các hệ điều hành khác để quản lý và hiển thị bảng ARP, nơi lưu trữ ánh xạ giữa địa chỉ IP và địa chỉ MAC của các thiết bị trong mạng cục bộ.

**1. Cú pháp cơ bản của lệnh `arp`:**
```bash
arp [options] [hostname]
```

**2. Các option của lệnh `arp`**

- **`-a`**: Hiển thị toàn bộ bảng ARP của hệ thống.
  - **Cú pháp**: 
    ```bash
    arp -a
    ```
    Lệnh này hiển thị tất cả các mục trong bảng ARP của hệ thống, bao gồm các địa chỉ IP và địa chỉ MAC.

- **`-n`**: Hiển thị địa chỉ IP và MAC mà không giải quyết tên máy chủ.
  - **Cú pháp**: 
    ```bash
    arp -n
    ```
    Lệnh này sẽ hiển thị địa chỉ IP và địa chỉ MAC mà không giải quyết thành tên máy chủ.

- **`-d`**: Xóa một mục ARP.
  - **Cú pháp**: 
    ```bash
    arp -d <ip-address>
    ```
    Lệnh này sẽ xóa mục ánh xạ địa chỉ IP từ bảng ARP. Ví dụ:
    ```bash
    arp -d 192.168.1.100
    ```

- **`-s`**: Thêm một ánh xạ IP-MAC vào bảng ARP.
  - **Cú pháp**:
    ```bash
    arp -s <ip-address> <mac-address>
    ```
    Lệnh này cho phép bạn thêm một mục vào bảng ARP, ánh xạ một địa chỉ IP với một địa chỉ MAC cụ thể. Ví dụ:
    ```bash
    arp -s 192.168.1.200 00:14:22:01:23:45
    ```

- **`-i`**: Chỉ định giao diện mạng.
  - **Cú pháp**: 
    ```bash
    arp -i <interface> -a
    ```
    Lệnh này sẽ hiển thị bảng ARP của một giao diện mạng cụ thể, ví dụ:
    ```bash
    arp -i eth0 -a
    ```
    Điều này sẽ chỉ hiển thị bảng ARP cho giao diện `eth0`.

- **`-v`**: Hiển thị thông tin chi tiết hơn.
  - **Cú pháp**:
    ```bash
    arp -v
    ```
    Lệnh này sẽ hiển thị thêm thông tin chi tiết về các mục trong bảng ARP.

- **`-V`**: Hiển thị phiên bản của lệnh `arp`.
  - **Cú pháp**:
    ```bash
    arp -V
    ```
    Lệnh này sẽ hiển thị thông tin về phiên bản của công cụ ARP đang được sử dụng.

**3. Các ví dụ sử dụng lệnh `arp`**

- **Hiển thị toàn bộ bảng ARP**:
  ```bash
  arp -a
  ```
  Kết quả:
  ```bash
  ? (192.168.1.1) at 00:14:22:01:23:45 [ether] on eth0
  ? (192.168.1.100) at 00:25:96:67:6f:ac [ether] on eth0
  ```

- **Hiển thị bảng ARP cho giao diện `eth0`**:
  ```bash
  arp -i eth0 -a
  ```

- **Thêm ánh xạ IP và MAC vào bảng ARP**:
  ```bash
  sudo arp -s 192.168.1.200 00:14:22:01:23:45
  ```

- **Xóa ánh xạ ARP cho một địa chỉ IP**:
  ```bash
  sudo arp -d 192.168.1.200
  ```

- **Hiển thị thông tin chi tiết về bảng ARP**:
  ```bash
  arp -v
  ```

- **Hiển thị phiên bản của `arp`**:
  ```bash
  arp -V
  ```

**4. Cách bảng ARP hoạt động**
- Bảng ARP lưu trữ ánh xạ giữa địa chỉ IP và địa chỉ MAC của các thiết bị trong mạng cục bộ.
- Khi một thiết bị muốn giao tiếp với một thiết bị khác trong mạng cục bộ nhưng chỉ biết địa chỉ IP, nó sẽ gửi một yêu cầu ARP (ARP Request) để tìm kiếm địa chỉ MAC tương ứng.
- Các thiết bị trong cùng một mạng cục bộ sẽ lưu trữ các ánh xạ này trong bảng ARP để giảm thiểu số lần gửi yêu cầu ARP.

**5. Tóm tắt các option của `arp`**

| Option       | Mô tả                                                        |
|--------------|--------------------------------------------------------------|
| `-a`         | Hiển thị toàn bộ bảng ARP.                                    |
| `-n`         | Hiển thị địa chỉ IP và MAC mà không giải quyết tên.           |
| `-d`         | Xóa mục ánh xạ ARP cho một địa chỉ IP cụ thể.                 |
| `-s`         | Thêm ánh xạ IP và MAC vào bảng ARP.                           |
| `-i`         | Chỉ định giao diện mạng để hiển thị bảng ARP của giao diện đó.|
| `-v`         | Hiển thị thông tin chi tiết hơn.                              |
| `-V`         | Hiển thị phiên bản của lệnh `arp`.                             |


-------------------------

### **Telnet**

Lệnh `telnet` là một công cụ mạng được sử dụng để kết nối với các dịch vụ mạng từ xa qua giao thức Telnet (TCP port 23). Mặc dù Telnet không mã hóa dữ liệu truyền tải và có thể gặp rủi ro bảo mật, nhưng nó vẫn được sử dụng trong một số trường hợp, như quản lý thiết bị mạng cũ hoặc khi việc mã hóa không cần thiết.

Dưới đây là các thông tin chi tiết về lệnh `telnet` và các option của nó:

**1. Cú pháp cơ bản của lệnh `telnet`**

```bash
telnet [hostname] [port]
```

- **`hostname`**: Địa chỉ IP hoặc tên miền của máy chủ bạn muốn kết nối.
- **`port`**: Cổng dịch vụ mà bạn muốn kết nối (mặc định là 23 đối với Telnet, nhưng bạn có thể thay đổi cổng nếu cần).

**2. Các option của lệnh `telnet`**

Lệnh `telnet` có một số option giúp bạn tùy chỉnh kết nối và kiểm soát phiên Telnet.

- **`-l <username>`**: Đặt tên người dùng khi kết nối đến một máy chủ Telnet.
  - **Ví dụ**:
    ```bash
    telnet -l user1 192.168.1.10
    ```
    Lệnh này sẽ kết nối đến địa chỉ IP `192.168.1.10` và sử dụng `user1` làm tên người dùng.

- **`-e <character>`**: Chỉ định ký tự để gửi lệnh từ xa, thay vì sử dụng "Ctrl-]". Thường dùng để thoát khỏi phiên Telnet.
  - **Ví dụ**:
    ```bash
    telnet -e q 192.168.1.10
    ```
    Lệnh này sử dụng ký tự `q` để thoát khỏi phiên Telnet thay vì `Ctrl-]`.

- **`-n <filename>`**: Ghi lại phiên Telnet vào một tệp tin.
  - **Ví dụ**:
    ```bash
    telnet -n session.log 192.168.1.10
    ```
    Lệnh này ghi lại tất cả các lệnh và phản hồi của phiên Telnet vào tệp `session.log`.

- **`-8`**: Sử dụng chế độ 8-bit, giúp làm việc với các ký tự 8-bit.
  - **Ví dụ**:
    ```bash
    telnet -8 192.168.1.10
    ```
    Lệnh này bật chế độ 8-bit khi kết nối tới máy chủ Telnet.

- **`-d`**: Bật chế độ debug để hiển thị thông tin chi tiết về kết nối.
  - **Ví dụ**:
    ```bash
    telnet -d 192.168.1.10
    ```
    Lệnh này sẽ in ra thông tin debug chi tiết về quá trình kết nối và giao tiếp với máy chủ.

- **`-f`**: Kết nối và ghi lại phiên làm việc vào tệp nhật ký (log).
  - **Ví dụ**:
    ```bash
    telnet -f mylog.txt 192.168.1.10
    ```
    Lệnh này sẽ ghi lại toàn bộ phiên Telnet vào tệp `mylog.txt`.

- **`-x`**: Bật chế độ "hex" để hiển thị các dữ liệu truyền tải ở dạng mã hex.
  - **Ví dụ**:
    ```bash
    telnet -x 192.168.1.10
    ```
    Lệnh này sẽ hiển thị các dữ liệu giao tiếp dưới dạng mã hex.

**3. Các lệnh cơ bản trong phiên `telnet`**

Khi bạn đã kết nối thành công với máy chủ qua Telnet, bạn có thể sử dụng một số lệnh bên trong phiên Telnet:

- **`Ctrl-]`**: Thoát khỏi chế độ Telnet và quay lại dòng lệnh.
- **`quit`** hoặc **`exit`**: Đóng phiên Telnet.
- **`status`**: Hiển thị thông tin trạng thái kết nối hiện tại.
- **`close`**: Đóng kết nối hiện tại mà không thoát khỏi lệnh Telnet.
- **`open <hostname> [port]`**: Kết nối lại đến một máy chủ hoặc cổng khác.

**4. Ví dụ sử dụng `telnet`**

- **Kết nối đến máy chủ Telnet mặc định (cổng 23)**:
  ```bash
  telnet 192.168.1.10
  ```

- **Kết nối đến một máy chủ và chỉ định cổng**:
  ```bash
  telnet 192.168.1.10 8080
  ```

- **Kết nối với tên người dùng cụ thể**:
  ```bash
  telnet -l admin 192.168.1.10
  ```

- **Ghi lại phiên Telnet vào tệp tin**:
  ```bash
  telnet -n session.log 192.168.1.10
  ```

- **Kết nối với máy chủ và sử dụng chế độ debug**:
  ```bash
  telnet -d 192.168.1.10
  ```

**5. Telnet và bảo mật**

Mặc dù Telnet có thể hữu ích trong việc kết nối đến các thiết bị mạng hoặc máy chủ, nhưng **Telnet không mã hóa** dữ liệu được truyền tải, bao gồm cả thông tin đăng nhập (username và password). Điều này làm cho Telnet không an toàn trong các môi trường mạng công cộng.

- **Sử dụng Telnet chỉ nên áp dụng trong các mạng riêng (LAN) hoặc khi bạn biết rõ môi trường kết nối.**
- **Sử dụng SSH thay thế**: Do Telnet không bảo mật, các hệ thống hiện đại thường sử dụng **SSH (Secure Shell)** để thay thế, vì SSH mã hóa dữ liệu và cung cấp bảo mật mạnh mẽ hơn.

**6. Tóm tắt các option của `telnet`**

| Option       | Mô tả                                                        |
|--------------|--------------------------------------------------------------|
| `-l <username>` | Chỉ định tên người dùng khi kết nối với máy chủ.               |
| `-e <character>` | Xác định ký tự để thoát khỏi phiên Telnet (mặc định là `Ctrl-]`). |
| `-n <filename>` | Ghi lại phiên Telnet vào tệp tin.                              |
| `-8`          | Sử dụng chế độ 8-bit cho các ký tự.                            |
| `-d`          | Bật chế độ debug để hiển thị thông tin chi tiết về kết nối.    |
| `-f`          | Ghi lại phiên Telnet vào tệp nhật ký.                         |
| `-x`          | Hiển thị dữ liệu giao tiếp dưới dạng mã hex.                  |


--------------

------------------------------------------

### **ping**

Lệnh `ping` là một công cụ mạng cơ bản và rất phổ biến dùng để kiểm tra khả năng kết nối mạng giữa hai thiết bị. `ping` hoạt động bằng cách gửi các gói ICMP (Internet Control Message Protocol) Echo Request đến một địa chỉ IP và đợi phản hồi Echo Reply. Đây là cách đơn giản để kiểm tra xem một thiết bị có thể kết nối đến một thiết bị khác trên mạng hay không.

### **Cú pháp cơ bản của lệnh `ping`**
```bash
ping [options] <hostname|IP_address>
```
- **`hostname`**: Tên miền hoặc địa chỉ IP của thiết bị mà bạn muốn kiểm tra kết nối.
- **`options`**: Các tùy chọn bổ sung để điều chỉnh hành vi của lệnh ping.

**Các Option của lệnh `ping`**

- **`-c <count>`**: Chỉ định số lần gửi gói ping (số gói ICMP Echo Request).
  - **Ví dụ**:
    ```bash
    ping -c 5 192.168.1.1
    ```
    Lệnh này sẽ gửi 5 gói ping đến địa chỉ IP `192.168.1.1` và dừng lại sau khi nhận đủ 5 phản hồi.

- **`-i <interval>`**: Thiết lập khoảng thời gian giữa các lần gửi gói ping. Mặc định là 1 giây.
  - **Ví dụ**:
    ```bash
    ping -i 2 192.168.1.1
    ```
    Lệnh này sẽ gửi gói ping đến `192.168.1.1` mỗi 2 giây.

- **`-t <ttl>`**: Xác định giá trị TTL (Time to Live) cho mỗi gói ping. TTL quyết định số bước nhảy tối đa mà gói tin có thể đi qua các router.
  - **Ví dụ**:
    ```bash
    ping -t 64 192.168.1.1
    ```
    Lệnh này sẽ thiết lập TTL là 64 cho các gói ping gửi đi.

- **`-s <size>`**: Thiết lập kích thước của mỗi gói ping (tính bằng byte).
  - **Ví dụ**:
    ```bash
    ping -s 1500 192.168.1.1
    ```
    Lệnh này sẽ gửi gói ping có kích thước 1500 byte tới `192.168.1.1`.

- **`-W <timeout>`**: Đặt thời gian chờ tối đa (tính bằng giây) để nhận phản hồi từ đích. Nếu hết thời gian chờ mà không nhận được phản hồi, lệnh sẽ kết thúc.
  - **Ví dụ**:
    ```bash
    ping -W 3 192.168.1.1
    ```
    Lệnh này sẽ chờ tối đa 3 giây để nhận phản hồi từ `192.168.1.1`.

- **`-q`**: Chỉ hiển thị kết quả tóm tắt, không hiển thị các gói ping chi tiết.
  - **Ví dụ**:
    ```bash
    ping -q 192.168.1.1
    ```
    Lệnh này chỉ hiển thị tóm tắt về các gói ping mà không hiển thị các thông tin chi tiết về mỗi gói.

- **`-a`**: Làm cho máy phát âm thanh khi nhận được phản hồi từ mục tiêu. Lựa chọn này có thể hữu ích khi kiểm tra kết nối trong môi trường không nhìn thấy màn hình.
  - **Ví dụ**:
    ```bash
    ping -a 192.168.1.1
    ```

- **`-f`**: Gửi các gói ping một cách liên tục và không dừng lại cho đến khi bạn dừng lệnh bằng cách nhấn `Ctrl+C`. Lệnh này thường được sử dụng để kiểm tra khả năng tải mạng.
  - **Ví dụ**:
    ```bash
    ping -f 192.168.1.1
    ```
    Lệnh này sẽ gửi các gói ping liên tục và hiển thị thông tin về tốc độ và độ trễ của mạng.

- **`-v`**: Bật chế độ verbose, hiển thị chi tiết thông tin về mỗi gói ping.
  - **Ví dụ**:
    ```bash
    ping -v 192.168.1.1
    ```

- **`-R`**: Gửi các gói ICMP Echo Request với đường đi phản hồi (Record Route). Chỉ hoạt động nếu người nhận hỗ trợ ghi lại các router đã đi qua.
  - **Ví dụ**:
    ```bash
    ping -R 192.168.1.1
    ```

**Ví dụ sử dụng lệnh `ping`**

1. **Ping một địa chỉ IP đơn giản**:
   ```bash
   ping 192.168.1.1
   ```
   Gửi các gói ping tới địa chỉ IP `192.168.1.1` và hiển thị thời gian phản hồi của mỗi gói.

2. **Ping đến một tên miền (ví dụ: `google.com`)**:
   ```bash
   ping google.com
   ```

3. **Ping với giới hạn số gói**:
   ```bash
   ping -c 4 192.168.1.1
   ```
   Gửi 4 gói ping tới `192.168.1.1` và sau đó dừng lại.

4. **Ping với khoảng thời gian giữa các gói**:
   ```bash
   ping -i 2 192.168.1.1
   ```
   Gửi gói ping đến `192.168.1.1` mỗi 2 giây.

5. **Ping với kích thước gói lớn**:
   ```bash
   ping -s 1000 192.168.1.1
   ```
   Gửi gói ping có kích thước 1000 byte đến `192.168.1.1`.

6. **Ping với chế độ tóm tắt**:
   ```bash
   ping -q 192.168.1.1
   ```
   Hiển thị kết quả tóm tắt mà không hiển thị thông tin chi tiết của mỗi gói ping.

7. **Ping liên tục (đến khi nhấn `Ctrl+C` để dừng)**:
   ```bash
   ping -f 192.168.1.1
   ```

**Giải thích các thông tin trong kết quả lệnh `ping`**

Kết quả khi sử dụng `ping` sẽ hiển thị các thông tin như:

1. **Thời gian phản hồi**: Thời gian mà gói ping đi từ máy của bạn đến máy đích và quay lại (tính bằng mili giây). Ví dụ:
   ```
   64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.045 ms
   ```

   - **64 bytes**: Kích thước của gói ICMP.
   - **from 192.168.1.1**: Địa chỉ IP của máy đích.
   - **icmp_seq=1**: Số thứ tự của gói ping.
   - **ttl=64**: Giá trị TTL (Time to Live), cho biết số lần gói ping có thể đi qua các router trước khi bị loại bỏ.
   - **time=0.045 ms**: Thời gian trễ (round-trip time), thời gian từ khi gói ping được gửi đi đến khi nhận được phản hồi.

2. **Tóm tắt kết quả sau khi dừng**:
   Sau khi bạn dừng lệnh `ping` (ví dụ, sử dụng `Ctrl+C`), nó sẽ hiển thị một tóm tắt về số lượng gói gửi đi, nhận lại và tỷ lệ mất gói, như sau:
   ```
   --- 192.168.1.1 ping statistics ---
   4 packets transmitted, 4 received, 0% packet loss, time 3002ms
   rtt min/avg/max/mdev = 0.045/0.058/0.071/0.010 ms
   ```

   - **4 packets transmitted, 4 received**: Gửi đi 4 gói và nhận lại 4 gói.
   - **0% packet loss**: Không mất gói nào.
   - **min/avg/max/mdev**: Thời gian trễ tối thiểu, trung bình, tối đa và độ lệch chuẩn.

-----------------------------


### **Công cụ `traceroute` và các Option**

`traceroute` là công cụ mạnh mẽ dùng để xác định tuyến đường (path) mà gói tin đi qua từ máy tính của bạn đến một máy chủ đích trên mạng. Công cụ này sẽ gửi các gói tin ICMP hoặc UDP (tùy thuộc vào cấu hình) và cho bạn biết từng hop (bước) mà gói tin đi qua, giúp bạn chẩn đoán các vấn đề mạng.

Dưới đây là một số tùy chọn (`options`) phổ biến của `traceroute` mà bạn có thể sử dụng để điều chỉnh cách thức hoạt động của công cụ này.

---

**1. Cấu trúc cơ bản của lệnh `traceroute`**

Cấu trúc cơ bản để sử dụng `traceroute` là:

```bash
traceroute [options] <địa chỉ đích>
```

Ví dụ đơn giản:
```bash
traceroute google.com
```

---

**2. Các Tùy Chọn (Options) Của `traceroute`**

Dưới đây là các tùy chọn phổ biến và cách sử dụng chúng:

#### **`-n`**: Hiển thị Địa chỉ IP thay vì tên miền

Khi bạn không muốn `traceroute` giải mã tên miền (DNS lookup) cho mỗi hop, bạn có thể sử dụng tùy chọn `-n`. Điều này giúp rút ngắn thời gian trả về.

```bash
traceroute -n google.com
```

**Kết quả:**
- Hiển thị địa chỉ IP của các hop thay vì tên miền.

---

#### **`-m <hop_count>`**: Giới hạn Số Lượng Hop (Bước)

Sử dụng tùy chọn `-m` để giới hạn số lượng hop mà `traceroute` sẽ kiểm tra. Mặc định, số hop tối đa là 30. Ví dụ, nếu bạn chỉ muốn kiểm tra tối đa 10 hop:

```bash
traceroute -m 10 google.com
```

**Kết quả:**
- `traceroute` sẽ dừng lại sau 10 hop, thay vì tiếp tục cho đến khi đến đích hoặc vượt quá số hop mặc định (30).

---

#### **`-w <timeout>`**: Đặt Thời Gian Chờ (Timeout) cho mỗi Hop

Tùy chọn `-w` cho phép bạn chỉ định thời gian chờ (timeout) cho mỗi gói tin được gửi. Mặc định là 5 giây. Nếu bạn muốn giảm thời gian chờ (ví dụ 3 giây):

```bash
traceroute -w 3 google.com
```

**Kết quả:**
- Nếu không nhận được phản hồi trong 3 giây từ một hop, `traceroute` sẽ hiển thị dấu `*`.

---

#### **`-I`**: Sử dụng ICMP Echo Request thay vì UDP

Mặc định, `traceroute` sử dụng các gói UDP để thực hiện việc định tuyến. Tuy nhiên, bạn có thể sử dụng ICMP Echo Request (giống như `ping`) bằng tùy chọn `-I`. Điều này có thể hữu ích khi các gói UDP bị tường lửa (firewall) hoặc router chặn.

```bash
traceroute -I google.com
```

**Kết quả:**
- `traceroute` sẽ sử dụng ICMP Echo Request (ping) thay vì gói UDP để truy tìm các hop.

---

#### **`-T`**: Sử dụng TCP SYN Packets

Tùy chọn `-T` cho phép bạn sử dụng TCP SYN packets thay vì UDP hoặc ICMP. Điều này có thể hữu ích khi các gói UDP hoặc ICMP bị chặn trong mạng của bạn, nhưng các gói TCP thì không bị ảnh hưởng.

```bash
traceroute -T google.com
```

**Kết quả:**
- Gửi gói SYN TCP để kiểm tra các hop trong mạng.

---

#### **`-p <port>`**: Xác Định Cổng TCP khi Sử Dụng `-T`

Khi sử dụng tùy chọn `-T` (gửi gói TCP), bạn có thể xác định cổng TCP mà gói SYN sẽ được gửi đến. Ví dụ, gửi một gói SYN đến cổng HTTP (80):

```bash
traceroute -T -p 80 google.com
```

**Kết quả:**
- Gửi gói SYN tới cổng TCP 80 (HTTP).

---

#### **`-q <queries>`**: Đặt Số Lượng Gói Tin Gửi đến mỗi Hop

Tùy chọn `-q` cho phép bạn chỉ định số lượng gói tin (queries) được gửi đến mỗi hop. Mặc định là 3 gói tin. Ví dụ, nếu bạn muốn gửi 5 gói tin đến mỗi hop:

```bash
traceroute -q 5 google.com
```

**Kết quả:**
- Mỗi hop sẽ nhận được 5 gói tin thay vì 3 gói tin mặc định.

---

#### **`-f <first_ttl>`**: Đặt Thời Gian Sống (TTL) Bắt Đầu

Tùy chọn `-f` cho phép bạn bắt đầu gửi gói tin từ một TTL (Time-To-Live) cụ thể. Điều này hữu ích khi bạn muốn bắt đầu từ một hop cụ thể trong chuỗi định tuyến. 

Ví dụ, để bắt đầu từ TTL 10 (hoặc hop thứ 10):

```bash
traceroute -f 10 google.com
```

**Kết quả:**
- Gói tin sẽ được gửi từ hop thứ 10 trở đi, bỏ qua các hop trước đó.

---

#### **`-z <wait_time>`**: Đặt Thời Gian Giữa Các Gói Tin

Tùy chọn `-z` cho phép bạn thiết lập thời gian chờ giữa các gói tin. Điều này có thể hữu ích khi bạn muốn tránh gởi quá nhanh các gói tin, điều này có thể gây ra quá tải cho mạng.

```bash
traceroute -z 0.5 google.com
```

**Kết quả:**
- Thời gian chờ giữa các gói tin sẽ là 0.5 giây.

---

#### **`-v`**: Chế Độ Chi Tiết (Verbose Mode)

Sử dụng tùy chọn `-v` để hiển thị thông tin chi tiết hơn về quá trình `traceroute`, chẳng hạn như số lượng gói tin đã gửi, thời gian chờ, và những thông tin kỹ thuật khác.

```bash
traceroute -v google.com
```

**Kết quả:**
- Hiển thị thêm thông tin chi tiết về quá trình gửi gói tin và nhận phản hồi.

---

#### **`-h`**: Hiển Thị Trợ Giúp

Nếu bạn cần trợ giúp hoặc muốn biết thêm thông tin về tất cả các tùy chọn có sẵn của `traceroute`, bạn có thể sử dụng tùy chọn `-h`:

```bash
traceroute -h
```

**Kết quả:**
- Hiển thị danh sách đầy đủ các tùy chọn của `traceroute` cùng với mô tả ngắn gọn.

---

**Ví Dụ về Sử Dụng Các Tùy Chọn `traceroute`**

1. **Truy tìm tuyến đường tới google.com với 5 gói tin mỗi hop và sử dụng ICMP Echo Request:**

   ```bash
   traceroute -I -q 5 google.com
   ```

2. **Truy tìm tuyến đường tới google.com, giới hạn ở 10 hop và thời gian chờ 3 giây:**

   ```bash
   traceroute -m 10 -w 3 google.com
   ```

3. **Truy tìm tuyến đường tới google.com, sử dụng gói TCP SYN và gửi tới cổng 80:**

   ```bash
   traceroute -T -p 80 google.com
   ```

4. **Truy tìm tuyến đường tới google.com, bắt đầu từ hop thứ 5 và gửi gói tin với thời gian giữa các gói là 1 giây:**

   ```bash
   traceroute -f 5 -z 1 google.com
   ```
-------

### **Các Thông Tin Hiển Thị khi Sử Dụng `traceroute`**

Khi bạn chạy lệnh `traceroute`, công cụ sẽ hiển thị thông tin chi tiết về các hop (bước nhảy) mà gói tin đi qua trên đường đi từ máy tính của bạn đến đích (máy chủ hoặc địa chỉ IP). Dưới đây là các thông tin mà bạn sẽ thấy trong kết quả của `traceroute`.


**Cấu Trúc Kết Quả `traceroute`**

Một kết quả `traceroute` điển hình có dạng như sau:

```bash
traceroute to google.com (142.250.72.14), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  0.389 ms  0.358 ms  0.325 ms
 2  10.10.10.1 (10.10.10.1)  10.457 ms  10.432 ms  10.392 ms
 3  * * *
 4  142.250.72.14 (142.250.72.14)  20.119 ms  20.105 ms  20.091 ms
```

**Các Thành Phần Của Kết Quả `traceroute`**

1. **Thông Tin Đích (Destination Information)**

   Dòng đầu tiên cung cấp thông tin về địa chỉ đích mà bạn đang traceroute tới. Nó bao gồm:
   - **Tên miền đích** (ví dụ: `google.com`)
   - **Địa chỉ IP đích** (ví dụ: `142.250.72.14`)
   - **Số lượng hop tối đa** (ví dụ: `30 hops max`), đây là số lượng hop tối đa mà gói tin có thể đi qua.
   - **Kích thước gói tin** (ví dụ: `60 byte packets`), tức là kích thước của các gói tin được gửi trong quá trình traceroute.

2. **Các Hop (Hops)**

   Mỗi dòng tiếp theo đại diện cho một hop trong quá trình đi từ máy bạn đến đích. Một hop thường là một router hoặc thiết bị mạng khác mà gói tin phải đi qua. Cấu trúc mỗi dòng hop gồm:
   
   - **Số thứ tự hop**: Đây là số thứ tự của hop trong chuỗi. Ví dụ: `1`, `2`, `3`, ...
   
   - **Địa chỉ IP hoặc Tên Miền của Router**: Địa chỉ IP hoặc tên miền của router hoặc thiết bị mạng mà gói tin đi qua. Ví dụ: `192.168.1.1` hoặc `google.com`.

   - **Thời gian (Latency) của các Gói Tin**: Thời gian để gói tin đến và nhận phản hồi từ mỗi hop, được đo bằng mili giây (ms). Thời gian này được hiển thị ba lần (ba giá trị tương ứng với ba gói tin được gửi đến mỗi hop):
     - **Ví dụ**: `0.389 ms  0.358 ms  0.325 ms`

     Mỗi giá trị tương ứng với thời gian phản hồi của một gói tin. Thời gian thấp cho thấy mạng hoạt động nhanh và ít độ trễ.

   - **Dấu `*` (nếu có)**: Nếu không có phản hồi từ hop nào trong thời gian chờ, bạn sẽ thấy dấu `*`. Điều này có thể xảy ra vì:
     - Router hoặc thiết bị mạng không trả lời yêu cầu ICMP (hoặc UDP, tùy thuộc vào cấu hình).
     - Mạng quá tải hoặc có firewall chặn các gói ICMP hoặc UDP.
     - Thời gian chờ (timeout) đã vượt quá giới hạn.

**Giải Thích Các Dòng trong Kết Quả `traceroute`**

**Ví dụ:**

```bash
traceroute to google.com (142.250.72.14), 30 hops max, 60 byte packets
 1  192.168.1.1 (192.168.1.1)  0.389 ms  0.358 ms  0.325 ms
 2  10.10.10.1 (10.10.10.1)  10.457 ms  10.432 ms  10.392 ms
 3  * * *
 4  142.250.72.14 (142.250.72.14)  20.119 ms  20.105 ms  20.091 ms
```

1. **Dòng đầu tiên**: 
   - **traceroute to google.com (142.250.72.14)**: Công cụ đang truy vết tới máy chủ `google.com` với địa chỉ IP là `142.250.72.14`.
   - **30 hops max**: Gói tin có thể đi qua tối đa 30 hop.
   - **60 byte packets**: Kích thước của mỗi gói tin là 60 byte.

2. **Dòng 1 (Hop 1)**:
   - **192.168.1.1**: Địa chỉ IP của router trong mạng nội bộ của bạn (hoặc gateway).
   - **0.389 ms  0.358 ms  0.325 ms**: Thời gian phản hồi cho ba gói tin gửi đi từ máy của bạn đến router này.

3. **Dòng 2 (Hop 2)**:
   - **10.10.10.1**: Địa chỉ IP của một router hoặc thiết bị mạng khác trên tuyến đường.
   - **10.457 ms  10.432 ms  10.392 ms**: Thời gian phản hồi của ba gói tin gửi đến router này.
   
4. **Dòng 3 (Hop 3)**:
   - **`* * *`**: Không nhận được phản hồi từ hop này trong thời gian chờ. Điều này có thể do firewall hoặc router không trả lời yêu cầu ICMP hoặc gói tin bị chặn.

5. **Dòng 4 (Hop 4)**:
   - **142.250.72.14**: Địa chỉ IP của máy chủ đích (hoặc router gần máy chủ đích).
   - **20.119 ms  20.105 ms  20.091 ms**: Thời gian phản hồi từ hop này (máy chủ đích).

**Tại sao `traceroute` Hiển Thị Ba Giá Trị Thời Gian Phản Hồi Cho Mỗi Hop?**

**Phân Tích Độ Tin Cậy:** Ba giá trị thời gian phản hồi giúp xác định độ tin cậy và sự ổn định của mỗi hop. Nếu ba giá trị có sự chênh lệch lớn, điều này có thể chỉ ra sự không ổn định hoặc các vấn đề về hiệu suất tại hop đó.

**Đánh Giá Chất Lượng Mạng:** Cung cấp ba lần đo cho mỗi hop cho phép bạn đánh giá chất lượng đường truyền tại mỗi điểm. Ví dụ, nếu một trong ba gói tin cho thấy thời gian phản hồi cao bất thường hoặc thất bại (hiển thị dấu *), có thể có sự cố tạm thời hoặc lỗi trên mạng.

**Trung Bình Giá Trị:** Ba giá trị cung cấp cơ sở để tính toán trung bình, cho phép nhận diện xu hướng chung của thời gian phản hồi thay vì dựa trên một mẫu đơn lẻ, giúp giảm thiểu ảnh hưởng của bất kỳ sự bất thường nào trong từng gói tin cụ thể.

**Các Trường Hợp Thông Tin Mất hoặc Không Hiển Thị**

1. **Dấu `*`**: Nếu bạn thấy dấu `*`, điều này có thể có một số nguyên nhân:
   - **Firewall hoặc Router không trả lời**: Một số router hoặc firewall có thể được cấu hình để không trả lời các gói ICMP (hoặc UDP), vì vậy bạn sẽ không thấy thời gian phản hồi cho hop đó.
   - **Mạng quá tải**: Mạng quá tải có thể gây ra mất mát gói tin.
   - **Thời gian chờ (timeout)**: Nếu thời gian chờ quá lâu, bạn sẽ thấy dấu `*`.

2. **Không có kết quả**: Nếu bạn không nhận được bất kỳ kết quả nào, có thể là do:
   - **Lỗi kết nối mạng**: Đảm bảo bạn có kết nối mạng và kiểm tra lại cài đặt mạng của bạn.
   - **Tường lửa hoặc Router không cho phép traceroute**: Một số hệ thống hoặc mạng có thể ngăn chặn các yêu cầu `traceroute` vì lý do bảo mật.


**Các Thông Tin Đặc Biệt trong Kết Quả `traceroute`**

- **Địa chỉ IP hoặc Tên Miền của Router**: Khi `traceroute` hiển thị tên miền, bạn có thể xác định được tên của router hoặc thiết bị mạng (nếu có thể phân giải DNS).
  
- **Thời Gian Phản Hồi (Latency)**: Các giá trị thời gian phản hồi (được đo bằng mili giây, ms) giúp bạn đánh giá độ trễ của các hop. Thời gian càng thấp thì mạng càng nhanh.

---------------------

### **mtr**

**MTR (My Traceroute) và Các Option**

`MTR` (My Traceroute) là một công cụ kết hợp giữa `ping` và `traceroute`, giúp bạn kiểm tra và phân tích tuyến đường mạng, đồng thời đo lường độ trễ và tỷ lệ mất gói tin (packet loss) cho mỗi hop trong suốt quá trình đi từ máy tính của bạn đến đích. `MTR` cung cấp thông tin chi tiết hơn so với `traceroute` vì nó liên tục gửi các gói tin đến mỗi hop và cập nhật kết quả trong thời gian thực.

**Cấu Trúc Lệnh `mtr`**

```bash
mtr [options] <destination>
```

Ví dụ:
```bash
mtr google.com
```

---

**Các Tùy Chọn (Options) Của `mtr`**

Dưới đây là các tùy chọn phổ biến của `mtr` cùng cách sử dụng:

#### **1. `-r`**: Chế Độ Báo Cáo (Report Mode)

Khi sử dụng tùy chọn `-r`, `mtr` sẽ chạy một lần duy nhất, gửi gói tin đến các hop, thu thập thông tin và xuất kết quả dưới dạng báo cáo thay vì chạy liên tục như mặc định.

```bash
mtr -r google.com
```

**Kết quả**:
- Chế độ này sẽ xuất ra kết quả thống kê sau một số gói tin được gửi đến mỗi hop, bao gồm thông tin về độ trễ và tỷ lệ mất gói.

---

#### **2. `-c <count>`**: Số Lượng Gói Tin

Tùy chọn `-c` cho phép bạn chỉ định số lượng gói tin tối đa mà `mtr` sẽ gửi đến mỗi hop. Mặc định là 10 gói tin.

```bash
mtr -c 20 google.com
```

**Kết quả**:
- Gửi 20 gói tin đến mỗi hop thay vì số gói tin mặc định.

---

#### **3. `-p <port>`**: Xác Định Cổng TCP

MTR có thể sử dụng giao thức TCP thay vì ICMP (được sử dụng mặc định trong `traceroute`). Nếu bạn muốn gửi các gói TCP đến một cổng cụ thể (ví dụ, cổng HTTP là 80), bạn có thể sử dụng tùy chọn `-p`.

```bash
mtr -p 80 google.com
```

**Kết quả**:
- Sử dụng TCP và gửi các gói tin đến cổng 80 của `google.com`.

---

#### **4. `-i <interval>`**: Thời Gian Giữa Các Gói Tin

Tùy chọn `-i` cho phép bạn chỉ định thời gian (tính bằng giây) giữa các gói tin được gửi đi. Mặc định là 1 giây.

```bash
mtr -i 2 google.com
```

**Kết quả**:
- Thời gian giữa mỗi gói tin sẽ là 2 giây thay vì mặc định 1 giây.

---

#### **5. `-w`**: Chế Độ Tĩnh (Non-Interactive Mode)

Tùy chọn `-w` cho phép bạn chạy `mtr` trong chế độ không tương tác, có nghĩa là chương trình sẽ không hiển thị bản đồ trực quan hoặc yêu cầu đầu vào từ người dùng.

```bash
mtr -w google.com
```

**Kết quả**:
- Chạy `mtr` trong chế độ báo cáo mà không có giao diện đồ họa.

---

#### **6. `-n`**: Hiển Thị Địa Chỉ IP Thay Vì Tên Miền

Tùy chọn `-n` yêu cầu `mtr` hiển thị địa chỉ IP thay vì tên miền (hostname) của các hop. Điều này giúp rút ngắn thời gian và không cần phải thực hiện phân giải DNS.

```bash
mtr -n google.com
```

**Kết quả**:
- Hiển thị chỉ địa chỉ IP thay vì tên miền cho các hop.

---

#### **7. `-v`**: Chế Độ Chi Tiết (Verbose Mode)

Tùy chọn `-v` hiển thị thêm thông tin chi tiết về kết quả của `mtr`. Đây có thể là thông tin hữu ích cho việc phân tích các hop và tình trạng mạng.

```bash
mtr -v google.com
```

**Kết quả**:
- Hiển thị thông tin chi tiết hơn về mỗi hop trong suốt quá trình traceroute.

---

#### **8. `-t`**: Chế Độ Thời Gian Chờ (Timeout)

Tùy chọn `-t` cho phép bạn chỉ định thời gian tối đa để đợi một phản hồi từ mỗi hop. Điều này hữu ích khi các hop có độ trễ cao hoặc khi bạn muốn kiểm tra các tuyến đường với thời gian chờ ngắn hơn.

```bash
mtr -t 500 google.com
```

**Kết quả**:
- Đặt thời gian chờ tối đa cho mỗi hop là 500 ms.

---

#### **9. `-h`**: Hiển Thị Trợ Giúp

Để xem tất cả các tùy chọn và cách sử dụng của `mtr`, bạn có thể sử dụng tùy chọn `-h`.

```bash
mtr -h
```

**Kết quả**:
- Hiển thị danh sách đầy đủ các tùy chọn và giải thích.

---

**Giải Thích Kết Quả `mtr`**

Kết quả của `mtr` cung cấp thông tin về mỗi hop (router hoặc thiết bị mạng) mà gói tin đi qua, kèm theo các chỉ số về độ trễ (latency) và tỷ lệ mất gói tin (packet loss).

Dưới đây là một ví dụ kết quả từ `mtr`:

```plaintext
Start: 2024-12-06T12:00:00+0000
HOST: localhost                       Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 192.168.1.1                    0.0%     10    0.3   0.4   0.2   0.6   0.1
  2.|-- 10.10.10.1                     0.0%     10    1.2   1.3   1.1   1.5   0.1
  3.|-- 142.250.72.14                  0.0%     10   15.4  15.6  15.3  15.8   0.1
```

**Các Thành Phần Của Kết Quả `mtr`:**
- **Số Thứ Tự**: Chỉ số của hop (1, 2, 3,...).
- **Địa Chỉ IP**: Địa chỉ của router hoặc thiết bị mạng mà gói tin đi qua.
- **Loss%**: Tỷ lệ mất gói tin tại hop đó. Một giá trị `0.0%` có nghĩa là không có gói tin bị mất.
- **Snt**: Số lượng gói tin được gửi đến hop đó.
- **Last**: Thời gian phản hồi (latency) của gói tin cuối cùng gửi đi tại hop đó.
- **Avg**: Thời gian phản hồi trung bình (average latency) của tất cả các gói tin gửi đến hop đó.
- **Best**: Thời gian phản hồi tốt nhất (best latency) trong quá trình gửi gói tin.
- **Wrst**: Thời gian phản hồi tệ nhất (worst latency) trong quá trình gửi gói tin.
- **StDev**: Độ lệch chuẩn (standard deviation) của các giá trị thời gian phản hồi, cho biết sự biến động của các thời gian phản hồi.

**Ví Dụ Thực Tế về `mtr`**

Giả sử bạn muốn kiểm tra tuyến đường đến `google.com` và muốn gửi 30 gói tin. Bạn có thể sử dụng lệnh sau:

```bash
mtr -r -c 30 google.com
```

**Kết quả có thể như sau:**

```plaintext
HOST: localhost                       Loss%   Snt   Last   Avg  Best  Wrst StDev
  1.|-- 192.168.1.1                    0.0%     30    0.3   0.4   0.2   0.6   0.1
  2.|-- 10.10.10.1                     0.0%     30    1.2   1.3   1.1   1.5   0.1
  3.|-- 142.250.72.14                  0.0%     30   15.4  15.6  15.3  15.8   0.1
```

**Giải Thích**:
- **Snt = 30**: Đã gửi 30 gói tin đến mỗi hop.
- **Loss% = 0.0%**: Không có gói tin bị mất trong suốt quá trình.
- **Last**: Thời gian phản hồi của gói tin cuối cùng tại mỗi hop.
- **Avg**: Thời gian phản hồi trung bình cho các gói tin gửi đến hop.
- **StDev**: Độ lệch chuẩn của thời gian phản hồi, cho biết sự biến động của thời gian phản hồi qua các gói tin.

