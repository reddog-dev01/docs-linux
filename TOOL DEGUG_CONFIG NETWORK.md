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
   - `pfifo_fast` Là một `qdisc` FIFO (First In, First Out), các gói tin được xử lý theo thứ tự đến. Gói tin đến được xử lý theo hàng đợi và sẽ được truyền tải khi đến lượt.
   - `netem` Là một `qdisc` được sử dụng để mô phỏng các điều kiện mạng như mất gói, độ trễ, jitter, v.v. Có thể sử dụng để kiểm tra cách ứng dụng hoạt động dưới các điều kiện mạng không ổn định.

5. **Trạng Thái (State)**
   - **Ví dụ**: `state UP`
   - Chỉ trạng thái hoạt động của giao diện: `UP` nghĩa là giao diện đang hoạt động và `DOWN` nghĩa là giao diện không hoạt động. `UNKNOWN` nghĩa là hệ điều hành không thể xác định chính xác trạng thái kết nối của giao diện.
Điều này thường xảy ra khi giao diện không trực tiếp kết nối đến phần cứng vật lý (như cáp mạng Ethernet hoặc card mạng thực).

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
default via 192.168.21.2 dev ens33 proto dhcp src 192.168.21.131 metric 100
192.168.21.0/24 dev ens33 proto kernel scope link src 192.168.21.131 metric 100
192.168.21.2 dev ens33 proto dhcp scope link src 192.168.21.131 metric 100 
```

Giải thích từng dòng:

**1. Default Route:**
```
default via 192.168.21.2 dev ens33 proto dhcp src 192.168.21.131 metric 100
```
- **default**: Đây là **default route**, tức là route mặc định. Khi một gói tin không khớp với bất kỳ route cụ thể nào trong bảng định tuyến, nó sẽ được gửi tới **gateway** ở địa chỉ `192.168.21.2`.
- **via 192.168.21.2**: Gói tin sẽ đi qua gateway `192.168.21.2`.
- **dev ens33**: Giao diện mạng được sử dụng là `ens33`.
- **proto dhcp**: Đây là route được cấp phát thông qua **DHCP** (Dynamic Host Configuration Protocol), nghĩa là thông tin này được tự động cấu hình khi máy tính nhận IP từ server DHCP.
- **src 192.168.21.131**: Địa chỉ IP nguồn được sử dụng là `192.168.21.131`.
- **metric 100**: Chỉ số metric cho route này là `100`. **Metric** là giá trị ưu tiên của route. Route có **metric thấp hơn** sẽ được ưu tiên hơn khi có nhiều route đến cùng một đích.

**2. Route cho mạng con `192.168.21.0/24`:**
```
192.168.21.0/24 dev ens33 proto kernel scope link src 192.168.21.131 metric 100
```
- **192.168.21.0/24**: Đây là một **route tĩnh** cho mạng con `192.168.21.0/24`, có địa chỉ IP bắt đầu từ `192.168.21.0` và subnet mask `/24` (mạng con này bao gồm các địa chỉ từ `192.168.21.1` đến `192.168.21.254`).
- **dev ens33**: Giao diện mạng `ens33` được sử dụng cho route này.
- **proto kernel**: Đây là route được tự động cấu hình bởi hệ điều hành khi giao diện `ens33` được khởi tạo và có địa chỉ IP `192.168.21.131`.
- **scope link**: Route này chỉ áp dụng cho các địa chỉ trong mạng con cục bộ và không đi ra ngoài mạng nội bộ.
- **src 192.168.21.131**: Địa chỉ IP nguồn cho mạng này là `192.168.21.131`.
- **metric 100**: Chỉ số metric cho route này là `100`.

 **3. Route trực tiếp đến `192.168.21.2`:**
```
192.168.21.2 dev ens33 proto dhcp scope link src 192.168.21.131 metric 100
```
- **192.168.21.2**: Đây là một **route trực tiếp** đến địa chỉ IP `192.168.21.2`, tức là mạng `192.168.21.2/32` (mạng có một địa chỉ duy nhất).
- **dev ens33**: Giao diện mạng `ens33` được sử dụng.
- **proto dhcp**: Route này cũng được cấu hình thông qua DHCP, có thể là địa chỉ của **gateway DHCP** mà bạn nhận được khi thiết bị kết nối với DHCP server.
- **scope link**: Route này chỉ áp dụng cho mạng con cục bộ.
- **src 192.168.21.131**: Địa chỉ IP nguồn là `192.168.21.131`.
- **metric 100**: Chỉ số metric cho route này là `100`.



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
mtr -r google.com
```

**Kết quả có thể như sau:**

![image](https://github.com/user-attachments/assets/f88e09a9-2ca9-4268-b79a-3d40c1766aa0)

**Cấu Trúc Kết Quả `mtr`**
Mỗi dòng trong bảng này có các thành phần sau:
- **Số Thứ Tự**: Chỉ số của hop (ví dụ, "1", "2", "3", ...).
- **Địa Chỉ IP hoặc Tên Host**: Địa chỉ IP hoặc tên máy chủ của hop (ví dụ, `192.168.18.2`, `static.vnpt.vn`).
- **Loss%**: Tỷ lệ mất gói tin (Packet Loss). Nó thể hiện phần trăm gói tin bị mất trong quá trình gửi.
- **Snt**: Số gói tin đã gửi đến hop đó.
- **Last**: Thời gian phản hồi (Latency) của gói tin cuối cùng tại hop đó (đơn vị: ms).
- **Avg**: Thời gian phản hồi trung bình (Average Latency) cho tất cả các gói tin gửi đến hop đó.
- **Best**: Thời gian phản hồi nhanh nhất (Best Latency) cho các gói tin gửi đến hop đó.
- **Wrst**: Thời gian phản hồi chậm nhất (Worst Latency) cho các gói tin gửi đến hop đó.
- **StDev**: Độ lệch chuẩn (Standard Deviation) của các thời gian phản hồi, cho biết mức độ biến động của thời gian phản hồi từ gói tin này sang gói tin khác.

**Phân Tích Các Bước Mạng**

1. **Hop 1: `192.168.18.2`**  
   - **Loss% = 0.0%**: Không có gói tin bị mất.
   - **Last = 0.6 ms, Avg = 5.3 ms**: Thời gian phản hồi của gói tin cuối cùng là 0.6 ms, và thời gian trung bình là 5.3 ms. Thời gian phản hồi khá ổn định.
   - **Wrst = 36.0 ms**: Thời gian phản hồi chậm nhất tại hop này là 36 ms, điều này cho thấy sự biến động nhỏ nhưng vẫn trong mức bình thường.

2. **Hop 2: `10.0.1.2`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 0.4 ms, Avg = 0.4 ms**: Thời gian phản hồi rất ngắn và ổn định tại hop này, cho thấy đây là một thiết bị gần bạn trong mạng nội bộ.

3. **Hop 3: `192.168.4.3`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 0.7 ms, Avg = 0.9 ms**: Mức độ trễ vẫn khá thấp, cho thấy hop này là một thiết bị mạng gần như trong mạng nội bộ.

4. **Hop 4: `192.168.8.205`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 0.5 ms, Avg = 0.5 ms**: Thời gian phản hồi rất nhanh và ổn định.

5. **Hop 5: `static.vnpt.vn`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 0.8 ms, Avg = 0.9 ms**: Gói tin tiếp tục đi ra ngoài mạng nội bộ vào mạng của VNPT (một nhà cung cấp dịch vụ).

6. **Hop 6: `dynamic.vnpt.vn`**  
   - **Loss% = 20.0%**: 20% gói tin bị mất tại hop này, đây có thể là một dấu hiệu của sự cố hoặc nghẽn mạng tại nhà cung cấp dịch vụ.
   - **Last = 9.4 ms, Avg = 9.8 ms**: Mức độ trễ cao và không ổn định, có thể do vấn đề tại hop này hoặc tại mạng VNPT.

7. **Hop 7: `static.vnpt.vn`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 0.8 ms, Avg = 1.1 ms**: Trễ vẫn thấp, mặc dù có sự biến động nhỏ.

8. **Hop 8: `???`**  
   - **Loss% = 100.0%**: Tất cả các gói tin đều bị mất tại hop này.
   - Đây có thể là do router hoặc thiết bị mạng tại hop này đã bị cấu hình để từ chối hoặc không trả lời các yêu cầu ICMP (tác động của các tường lửa hoặc các cấu hình bảo mật).

9. **Hop 9: `static.vnpt.vn`**  
   - **Loss% = 0.0%**: Không mất gói tin.
   - **Last = 1.0 ms, Avg = 2.7 ms**: Trễ hơi cao hơn nhưng không có vấn đề mất gói tin.

10. **Hop 10: `static.vnpt.vn`**  
    - **Loss% = 0.0%**: Không mất gói tin.
    - **Last = 17.6 ms, Avg = 17.6 ms**: Trễ khá ổn định tại hop này, và thời gian phản hồi không có sự biến động lớn.

11. **Hop 11: `72.14.219.148`**  
    - **Loss% = 0.0%**: Không mất gói tin.
    - **Last = 17.2 ms, Avg = 17.3 ms**: Trễ thấp và ổn định.

12. **Hop 12: `142.251.67.15`**  
    - **Loss% = 0.0%**: Không mất gói tin.
    - **Last = 19.8 ms, Avg = 19.6 ms**: Trễ hơi cao một chút, nhưng vẫn ổn định.

13. **Hop 13: `66.249.95.171`**  
    - **Loss% = 0.0%**: Không mất gói tin.
    - **Last = 17.1 ms, Avg = 17.1 ms**: Thời gian phản hồi ổn định.

14. **Hop 14: `nchkgb-af-in-f14.1e100.ne`**  
    - **Loss% = 0.0%**: Không mất gói tin.
    - **Last = 17.7 ms, Avg = 17.8 ms**: Trễ ổn định, và có vẻ như gói tin đã đến gần đích (có thể là một máy chủ Google hoặc tương tự).

Khi **Hop 8** trong kết quả `mtr` hiển thị là `???` với tỷ lệ mất gói tin là **100.0%**, điều này có thể gây ra sự lo ngại về một số vấn đề mạng. Tuy nhiên, điều quan trọng là hiểu rằng sự mất gói tin này không nhất thiết phải có ảnh hưởng nghiêm trọng đến kết quả tổng thể của kết nối mạng của bạn. Đây là một số điều bạn cần lưu ý:

**Nguyên Nhân và Ý Nghĩa của Mất Gói Tin tại Hop 8**

1. **Cấu Hình Router hoặc Thiết Bị Mạng**:
   - **Không phản hồi ICMP**: Một số router hoặc thiết bị mạng có thể được cấu hình để **không phản hồi** các yêu cầu ICMP (ping/traceroute). Điều này có thể là do các **tường lửa** hoặc các biện pháp bảo mật khác nhằm ngăn chặn các cuộc tấn công từ bên ngoài, hoặc đơn giản là để giảm tải cho các thiết bị mạng.
   - **Bảo mật**: Một số nhà cung cấp dịch vụ hoặc tổ chức mạng có thể cấu hình các router của họ để không trả lời các yêu cầu ICMP, vì điều này không ảnh hưởng đến việc truyền tải dữ liệu thực sự trong mạng.

2. **Không ảnh hưởng đến kết nối thực tế**:
   - **Không ảnh hưởng đến kết nối cuối cùng**: Mặc dù bạn không nhận được phản hồi từ hop này, điều này không có nghĩa là kết nối mạng của bạn bị gián đoạn. Các gói tin vẫn có thể tiếp tục đến đích mà không gặp sự cố. Traceroute chỉ gửi gói tin ICMP để kiểm tra các hop trên đường đi, nhưng các giao thức dữ liệu thực tế (như TCP hoặc UDP) vẫn có thể hoạt động bình thường mà không bị ảnh hưởng.
   - **Dữ liệu vẫn đi qua mạng bình thường**: Nếu các hop tiếp theo vẫn có phản hồi bình thường và không có mất gói tin, thì kết nối mạng của bạn có thể vẫn ổn, ngay cả khi một số hop không phản hồi.

3. **Các Router hoặc Thiết Bị Trung Gian**:
   - **Không phải tất cả các hop đều trả lời**: Thực tế, có thể có nhiều lý do khiến một số router hoặc thiết bị mạng không trả lời yêu cầu ICMP. Điều này bao gồm việc chúng có thể **không tham gia vào quá trình phân phối gói tin** hoặc **được cấu hình để không phản hồi** với các gói ICMP để bảo vệ bản thân khỏi các cuộc tấn công DDoS hoặc đơn giản là không hỗ trợ ICMP.

**Ảnh Hưởng của Việc Mất Gói Tin 100% tại Hop 8**

1. **Nếu các hop sau vẫn bình thường**:
   - Nếu **các hop sau (hop 9, hop 10,...) vẫn phản hồi tốt** và không có sự mất gói tin, thì sự cố tại hop 8 không ảnh hưởng nghiêm trọng đến kết nối mạng của bạn. Bạn vẫn có thể truy cập các dịch vụ, website, và thực hiện các giao tiếp mạng bình thường mà không gặp vấn đề.

2. **Nếu mạng hoặc kết nối của bạn gặp vấn đề**:
   - Nếu bạn nhận thấy **mạng chậm hoặc gián đoạn** và việc mất gói tin tại hop 8 xảy ra cùng với các vấn đề này, thì có thể hop này đang gây ra một vấn đề tiềm ẩn trong việc định tuyến gói tin. Tuy nhiên, như đã đề cập trước, mất gói tin ICMP không luôn đồng nghĩa với mất gói tin thực tế trong giao tiếp dữ liệu.

**Khi Nào Bạn Cần Lo Ngại?**
Mất gói tin tại một hop không phải là một dấu hiệu chắc chắn của sự cố mạng. Tuy nhiên, nếu vấn đề này xảy ra thường xuyên và bạn gặp phải **mất kết nối** hoặc **truyền tải dữ liệu bị gián đoạn**, thì bạn có thể cần phải:

- **Kiểm tra lại kết nối mạng**: Đảm bảo không có vấn đề với các hop trước hoặc sau đó.
- **Liên hệ với nhà cung cấp dịch vụ mạng**: Nếu vấn đề liên quan đến một hop ngoài mạng của bạn (chẳng hạn như hop của nhà cung cấp dịch vụ Internet hoặc một thiết bị mạng bên ngoài), bạn có thể cần thông báo cho họ để họ kiểm tra và khắc phục sự cố.
- **Thử các công cụ khác**: Bạn có thể sử dụng các công cụ khác như **ping** hoặc **iperf** để kiểm tra thêm về độ trễ, mất gói tin, hoặc tốc độ mạng thực tế.

---------------------------------------

### **netstat**

`netstat` là một công cụ dòng lệnh rất hữu ích để hiển thị các kết nối mạng, bảng định tuyến, thống kê giao thức, và thông tin về các cổng đang mở trên hệ thống. Bạn có thể sử dụng `netstat` để kiểm tra tình trạng mạng và tìm hiểu về các kết nối đang hoạt động trên hệ thống của mình.

### **Công Dụng của `netstat`**

1. **Hiển thị các kết nối mạng đang hoạt động**: Bạn có thể xem các kết nối TCP, UDP hiện tại, trạng thái của chúng (ví dụ: LISTENING, ESTABLISHED), và các cổng mà chúng sử dụng.
2. **Hiển thị bảng định tuyến**: `netstat` có thể giúp bạn xem các tuyến đường mạng được cấu hình trên hệ thống.
3. **Thống kê giao thức**: Bạn có thể xem thống kê chi tiết về các giao thức như TCP, UDP, ICMP, v.v.
4. **Kiểm tra cổng và các dịch vụ mạng**: Bạn có thể xác định các cổng đang mở và các ứng dụng nào đang sử dụng chúng.

### **Các Tùy Chọn (`Options`) của `netstat`**

Dưới đây là một số tùy chọn phổ biến mà bạn có thể sử dụng với `netstat`:

----------------

#### 1. **`-a` (All)**
   - Hiển thị **tất cả các kết nối** và các cổng đang lắng nghe.
   - Cả kết nối TCP và UDP sẽ được liệt kê.
   - **Ví dụ**:
     ```bash
     netstat -a
     ```

Khi bạn chạy lệnh `netstat -a` trên hệ thống của mình, kết quả trả về sẽ hiển thị một danh sách các kết nối mạng và các cổng đang lắng nghe. Dưới đây là **giải thích ý nghĩa các cột** trong kết quả của `netstat -a`:

**Ví Dụ về Kết Quả `netstat -a`**
```bash
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 192.168.1.2:80         0.0.0.0:*               LISTEN
tcp        0      0 192.168.1.2:22         192.168.1.3:53372       ESTABLISHED
udp        0      0 192.168.1.2:123        0.0.0.0:*               LISTEN
```

**Các Cột trong Kết Quả `netstat -a`**

1. **Proto**: 
   - **Mô tả**: Cột này cho biết loại giao thức của kết nối mạng.
   - **Giá trị có thể xuất hiện**:
     - `tcp`: Giao thức TCP (Transmission Control Protocol).
     - `udp`: Giao thức UDP (User Datagram Protocol).
     - `unix`: Kết nối sử dụng socket UNIX (local inter-process communication).

2. **Recv-Q** (Receive Queue):
   - **Mô tả**: Đây là số lượng byte mà hệ thống đang chờ để đọc từ **bộ đệm nhận** (receive buffer) cho mỗi kết nối.
   - **Giải thích**: Nếu giá trị này lớn, điều đó có thể cho thấy hệ thống đang gặp khó khăn trong việc xử lý các gói tin đến và có thể ảnh hưởng đến hiệu suất của kết nối. Tuy nhiên, thông thường, giá trị này thường bằng `0` khi không có gói tin nào chờ xử lý.

3. **Send-Q** (Send Queue):
   - **Mô tả**: Đây là số byte mà hệ thống đang chờ để gửi đi qua kết nối này, tức là số dữ liệu chưa được truyền đi từ bộ đệm gửi (send buffer).
   - **Giải thích**: Nếu giá trị này lớn, có thể có vấn đề với băng thông mạng hoặc mạng bị quá tải, dẫn đến việc dữ liệu không thể gửi đi kịp thời.

4. **Local Address**:
   - **Mô tả**: Đây là địa chỉ IP và cổng của **hệ thống cục bộ** (local system), tức là hệ thống đang thực hiện lệnh `netstat`.
   - **Giải thích**: Địa chỉ này có thể là địa chỉ IP của hệ thống (ví dụ: `192.168.1.2`) và cổng mà ứng dụng hoặc dịch vụ trên máy của bạn đang lắng nghe (ví dụ: `:80`, `:22`).
     - Nếu địa chỉ là `0.0.0.0`, điều này có nghĩa là hệ thống lắng nghe trên **tất cả các địa chỉ IP** khả dụng của máy.
     - Nếu địa chỉ là `::` (IPv6), có nghĩa là hệ thống lắng nghe trên tất cả các địa chỉ IPv6 khả dụng.

5. **Foreign Address**:
   - **Mô tả**: Đây là địa chỉ IP và cổng của **hệ thống từ xa** (remote system) mà máy của bạn đang kết nối tới, hoặc là hệ thống mà bạn đang giao tiếp.
   - **Giải thích**: Nếu kết nối đang lắng nghe (ví dụ, đối với cổng HTTP - 80), thì cột này sẽ là `*`, có nghĩa là không có kết nối cụ thể nào, máy của bạn đang chờ các kết nối đến. Nếu kết nối đã được thiết lập, địa chỉ IP và cổng của hệ thống từ xa sẽ được hiển thị tại đây (ví dụ: `192.168.1.3:53372`).

6. **State**:
   - **Mô tả**: Cột này cho biết **trạng thái** hiện tại của kết nối TCP.
   - **Giải thích các trạng thái có thể xuất hiện**:
     - `LISTEN`: Cổng đang **lắng nghe** cho các kết nối đến từ bên ngoài. Dịch vụ đang chờ để chấp nhận kết nối (ví dụ: một server web đang chờ kết nối HTTP).
     - `ESTABLISHED`: Kết nối đã được thiết lập giữa hai hệ thống. Các gói tin có thể được truyền qua kết nối này.
     - `TIME_WAIT`: Kết nối đã đóng và đang đợi đủ thời gian để chắc chắn các gói tin đã được truyền hết. Sau thời gian này, kết nối sẽ được giải phóng.
     - `CLOSE_WAIT`: Hệ thống đã nhận được yêu cầu đóng kết nối từ phía đối tác, nhưng chưa đóng kết nối đó.
     - `SYN_SENT`: Hệ thống đã gửi yêu cầu kết nối (SYN) nhưng chưa nhận được phản hồi từ phía đối tác.
     - `SYN_RECV`: Hệ thống đã nhận yêu cầu kết nối (SYN) và đang chờ phản hồi từ phía đối tác.
     - `FIN_WAIT1` và `FIN_WAIT2`: Kết nối đang trong quá trình đóng.
     - `CLOSING`: Cả hai hệ thống đã gửi yêu cầu đóng kết nối và đang chờ phản hồi cuối cùng.
     - `LAST_ACK`: Hệ thống đã gửi yêu cầu đóng và đang chờ xác nhận từ phía đối tác.

**Ví Dụ về Kết Quả `netstat -a`**

```bash
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 192.168.1.2:80         0.0.0.0:*               LISTEN
tcp        0      0 192.168.1.2:22         192.168.1.3:53372       ESTABLISHED
udp        0      0 192.168.1.2:123        0.0.0.0:*               LISTEN
```

- **Dòng 1**:
  - Giao thức là `tcp`.
  - Cổng 80 trên địa chỉ IP cục bộ `192.168.1.2` đang **lắng nghe** (LISTEN) cho các kết nối HTTP từ hệ thống khác.
  - Không có địa chỉ từ xa (do đây là cổng lắng nghe).
  
- **Dòng 2**:
  - Giao thức là `tcp`.
  - Cổng 22 (SSH) trên `192.168.1.2` đang **kết nối** với `192.168.1.3:53372`.
  - Trạng thái của kết nối là `ESTABLISHED`, tức là kết nối SSH đã được thiết lập và đang hoạt động.

- **Dòng 3**:
  - Giao thức là `udp`.
  - Cổng 123 trên `192.168.1.2` đang **lắng nghe** (LISTEN) cho các kết nối NTP (Network Time Protocol).
 

----------------------

#### 2. **`-t` (TCP)**
   - Chỉ hiển thị các kết nối **TCP**.
   - **Ví dụ**:
     ```bash
     netstat -t
     ```



#### 3. **`-u` (UDP)**
   - Chỉ hiển thị các kết nối **UDP**.
   - **Ví dụ**:
     ```bash
     netstat -u
     ```

#### 4. **`-n` (Numerical)**
   - Hiển thị địa chỉ IP và số cổng dưới dạng **số** thay vì tên miền hoặc tên dịch vụ.
   - **Ví dụ**:
     ```bash
     netstat -n
     ```

#### 5. **`-l` (Listening)**
   - Chỉ hiển thị các **cổng đang lắng nghe** (đang chờ kết nối).
   - **Ví dụ**:
     ```bash
     netstat -l
     ```

#### 6. **`-p` (Program)**
   - Hiển thị **PID** và tên chương trình đang sử dụng cổng.
   - Bạn cần quyền root để sử dụng tùy chọn này.
   - **Ví dụ**:
     ```bash
     sudo netstat -p
     ```
---------------------------

#### 7. **`-r` (Routing Table)**
   - Hiển thị **bảng định tuyến mạng** của hệ thống.
   - **Ví dụ**:
     ```bash
     netstat -r
     ```

![image](https://github.com/user-attachments/assets/6f6a44c9-db31-4361-a0e0-eae8bea3f4d3)

**Giải Thích Các Cột trong Bảng Định Tuyến**

1. **Destination** (Đích):
   - **Mô tả**: Đây là địa chỉ IP hoặc mạng đích mà gói tin sẽ được gửi đến. 
   - **Ví dụ**: `default`, `172.16.1.0`, `192.168.18.0`, `192.168.168.0`.
   - - `default`: Đây là tuyến đường mặc định (default route), tức là tuyến đường được sử dụng khi không có tuyến đường cụ thể cho đích được tìm thấy.
  
2. **Gateway** (Cổng đích):
   - **Mô tả**: Đây là địa chỉ IP của cổng (gateway) hoặc thiết bị tiếp theo mà gói tin sẽ đi qua để đến đích.
   - **Ví dụ**: `_gateway`, `0.0.0.0`.
     - Nếu cổng là `0.0.0.0`, có nghĩa là không có cổng trung gian (directly reachable).
     - `_gateway`: Thường là địa chỉ của cổng mặc định mà hệ thống sẽ sử dụng để ra ngoài mạng hoặc đến các mạng khác.
   
3. **Genmask** (Netmask):
   - **Mô tả**: Địa chỉ subnet mask của mạng đích. Subnet mask xác định phần nào của địa chỉ IP là mạng và phần nào là địa chỉ máy.
   - **Ví dụ**: `255.255.255.0`.
     - Subnet mask `255.255.255.0` có nghĩa là hệ thống này có thể giao tiếp với tất cả các địa chỉ IP trong cùng mạng con có đầu 24 bit giống nhau.
   
4. **Flags**:
   - **Mô tả**: Các cờ trạng thái về tuyến đường. Một số giá trị phổ biến:
     - **U**: Tuyến đường này **hoạt động** (Up).
     - **G**: Tuyến đường này là một **tuyến đường qua cổng** (Gateway).
     - **H**: Tuyến đường này dùng cho **host-specific** (tuyến đường đến một máy tính cụ thể).
   
5. **MSS** (Maximum Segment Size):
   - **Mô tả**: Kích thước phân đoạn tối đa cho các gói TCP trong kết nối này. MSS không thường xuyên được sử dụng trong bảng định tuyến.
   - **Giải thích**: MSS có thể là `0` nếu không có giá trị cụ thể.

6. **Window**:
   - **Mô tả**: Đây là cửa sổ băng thông của kết nối mạng. Thường không có ý nghĩa trong bảng định tuyến cơ bản và thường được đặt là `0`.

7. **irtt** (Initial Round Trip Time):
   - **Mô tả**: Thời gian trễ (RTT) ban đầu ước tính cho tuyến đường này.
   - **Giải thích**: Đây là một giá trị độ trễ có thể được sử dụng trong một số giao thức định tuyến động để tính toán đường đi tối ưu. Tuy nhiên, giá trị này thường bằng `0` trong các bảng định tuyến mặc định.

8. **Iface** (Interface):
   - **Mô tả**: Giao diện mạng mà hệ thống sử dụng để gửi gói tin đến đích. Đây có thể là một cổng mạng vật lý hoặc mạng ảo.
   - **Ví dụ**: `eno1`, `vmnet8`, `vmnet1`.
     - **eno1**: Thường là tên của một giao diện Ethernet.
     - **vmnet8**: Là tên của một giao diện mạng ảo trong môi trường ảo hóa (VMware hoặc VirtualBox).
     - **vmnet1**: Một giao diện mạng ảo khác (thường liên quan đến mạng nội bộ trong máy ảo).

### **Giải Thích Các Dòng Kết Quả**

1. **Dòng 1**: 
   ```plaintext
   default         _gateway        0.0.0.0         UG        0 0          0 eno1
   ```
   - **Destination**: `default` (tuyến đường mặc định).
   - **Gateway**: `_gateway` (cổng mặc định, có thể là địa chỉ của router).
   - **Genmask**: `0.0.0.0` (mạng không xác định, áp dụng cho tất cả các địa chỉ IP).
   - **Flags**: `UG` (U: tuyến đường hoạt động, G: qua cổng - Gateway).
   - **Iface**: `eno1` (giao diện mạng cổng này kết nối tới).

2. **Dòng 2**:
   ```plaintext
   172.16.1.0      0.0.0.0         255.255.255.0   U         0 0          0 vmnet8
   ```
   - **Destination**: `172.16.1.0` (mạng con 172.16.1.0/24).
   - **Gateway**: `0.0.0.0` (địa chỉ này có thể được tiếp cận trực tiếp, không cần cổng trung gian).
   - **Genmask**: `255.255.255.0` (mạng con này có độ dài mạng là 24 bit).
   - **Flags**: `U` (tuyến đường hoạt động).
   - **Iface**: `vmnet8` (giao diện mạng ảo).

3. **Dòng 3**:
   ```plaintext
   192.168.18.0    0.0.0.0         255.255.255.0   U         0 0          0 eno1
   ```
   - **Destination**: `192.168.18.0` (mạng con 192.168.18.0/24).
   - **Gateway**: `0.0.0.0` (địa chỉ này có thể được tiếp cận trực tiếp).
   - **Genmask**: `255.255.255.0` (mạng con này có độ dài mạng là 24 bit).
   - **Flags**: `U` (tuyến đường hoạt động).
   - **Iface**: `eno1` (giao diện mạng vật lý).

4. **Dòng 4**:
   ```plaintext
   192.168.168.0   0.0.0.0         255.255.255.0   U         0 0          0 vmnet1
   ```
   - **Destination**: `192.168.168.0` (mạng con 192.168.168.0/24).
   - **Gateway**: `0.0.0.0` (địa chỉ này có thể được tiếp cận trực tiếp).
   - **Genmask**: `255.255.255.0` (mạng con này có độ dài mạng là 24 bit).
   - **Flags**: `U` (tuyến đường hoạt động).
   - **Iface**: `vmnet1` (giao diện mạng ảo).
  
------------------

#### 8. **`-i` (Interface)**
   - Hiển thị các thông tin mạng của **giao diện mạng** (interface) như eth0, wlan0, v.v.
   - **Ví dụ**:
     ```bash
     netstat -i
     ```

Kết quả của lệnh `netstat -i` sẽ hiển thị thông tin chi tiết về các **giao diện mạng** (network interfaces) trên hệ thống của bạn. Dưới đây là giải thích các cột trong kết quả này.

 **Ví Dụ về Kết Quả `netstat -i`**

```bash
Kernel Interface table
Iface    MTU   RX-OK  RX-ERR  RX-DRP  RX-OVR  TX-OK  TX-ERR  TX-DRP  TX-OVR  Flg
eth0    1500   12345      0      0       0    67890      0      0       0  BMRU
lo      65536  56789      0      0       0    56789      0      0       0  LRU
```

**Giải Thích Các Cột trong Kết Quả `netstat -i`**

1. **Iface**:
   - **Mô tả**: Đây là tên của **giao diện mạng** trên hệ thống.
   - **Ví dụ**: `eth0`, `lo`.
     - `eth0`: Thường là tên của giao diện Ethernet (mạng vật lý).
     - `lo`: Là giao diện loopback (mạng nội bộ, được sử dụng để giao tiếp với chính hệ thống).

2. **MTU (Maximum Transmission Unit)**:
   - **Mô tả**: Kích thước tối đa của một gói tin mà giao diện mạng này có thể truyền tải. 
   - **Giải thích**: MTU mặc định của Ethernet thường là 1500 byte. Giao diện loopback (`lo`) thường có MTU là 65536 byte, vì đây là giao diện chỉ sử dụng trong hệ thống nội bộ.

3. **RX-OK (Received OK)**:
   - **Mô tả**: Số lượng gói tin **nhận thành công** qua giao diện này.
   - **Giải thích**: Đây là số gói tin mà giao diện mạng đã nhận mà không có lỗi.

4. **RX-ERR (Received Errors)**:
   - **Mô tả**: Số lượng gói tin nhận được có **lỗi**.
   - **Giải thích**: Các lỗi nhận gói có thể là do các vấn đề như lỗi CRC, gói tin bị hỏng hoặc không hợp lệ.

5. **RX-DRP (Received Drops)**:
   - **Mô tả**: Số lượng gói tin bị **rớt** trong quá trình nhận.
   - **Giải thích**: Các gói tin có thể bị rớt do quá tải bộ đệm hoặc bộ đệm của giao diện mạng bị đầy.

6. **RX-OVR (Received Overruns)**:
   - **Mô tả**: Số lượng gói tin bị **tràn bộ đệm nhận**.
   - **Giải thích**: Tràn bộ đệm xảy ra khi các gói tin đến quá nhanh và hệ thống không thể xử lý kịp thời.

7. **TX-OK (Transmitted OK)**:
   - **Mô tả**: Số lượng gói tin **gửi thành công** qua giao diện này.
   - **Giải thích**: Đây là số gói tin mà giao diện mạng đã gửi mà không có lỗi.

8. **TX-ERR (Transmit Errors)**:
   - **Mô tả**: Số lượng gói tin gửi đi bị **lỗi**.
   - **Giải thích**: Lỗi truyền có thể xảy ra do sự cố phần cứng hoặc cấu hình không đúng.

9. **TX-DRP (Transmit Drops)**:
   - **Mô tả**: Số lượng gói tin bị **rớt** khi gửi.
   - **Giải thích**: Gói tin bị rớt khi bộ đệm truyền bị đầy hoặc có sự cố trong quá trình truyền.

10. **TX-OVR (Transmit Overruns)**:
   - **Mô tả**: Số lượng gói tin bị **tràn bộ đệm gửi**.
   - **Giải thích**: Khi bộ đệm gửi không thể xử lý các gói tin đến trong một khoảng thời gian ngắn, gói tin có thể bị tràn và mất.

11. **Flg (Flags)**:
   - **Mô tả**: Các **cờ trạng thái** của giao diện mạng, cho biết trạng thái và tính năng của giao diện.
   - **Giải thích**:
     - `B` – Bộ lọc (broadcast).
     - `M` – Được quản lý bởi một công cụ.
     - `R` – Giao diện đang chạy (running).
     - `U` – Giao diện đang **hoạt động** (up).
     - `L` – Giao diện loopback.
     - `A` – Giao diện đang nhận địa chỉ.
     - `P` – Được cấu hình cho **promiscuous mode** (chế độ nhận tất cả các gói tin).

**Ví Dụ Giải Thích**
Dưới đây là một ví dụ và giải thích chi tiết cho kết quả:

```bash
Iface    MTU   RX-OK  RX-ERR  RX-DRP  RX-OVR  TX-OK  TX-ERR  TX-DRP  TX-OVR  Flg
eth0    1500   12345      0      0       0    67890      0      0       0  BMRU
```

- **eth0**: Tên của giao diện mạng.
- **MTU**: Kích thước tối đa của gói tin là 1500 byte.
- **RX-OK**: Giao diện đã nhận thành công 12,345 gói tin.
- **RX-ERR**: Không có lỗi nhận gói tin (`0`).
- **RX-DRP**: Không có gói tin nào bị rớt khi nhận (`0`).
- **RX-OVR**: Không có sự cố tràn bộ đệm nhận (`0`).
- **TX-OK**: Giao diện đã gửi thành công 67,890 gói tin.
- **TX-ERR**: Không có lỗi khi gửi gói tin (`0`).
- **TX-DRP**: Không có gói tin nào bị rớt khi gửi (`0`).
- **TX-OVR**: Không có sự cố tràn bộ đệm gửi (`0`).
- **Flg**: Các cờ trạng thái là `BMRU`, nghĩa là:
  - `B` (broadcast).
  - `M` (managed).
  - `R` (running).
  - `U` (up).

-----------------------


#### 9. **`-s` (Statistics)**
   - Hiển thị các **thống kê chi tiết** về các giao thức mạng (TCP, UDP, ICMP, v.v.).
   - **Ví dụ**:
     ```bash
     netstat -s
     ```
Lệnh `netstat -s` được sử dụng để hiển thị các thống kê chi tiết về **giao thức mạng** trên hệ thống. Các thống kê này cung cấp cái nhìn sâu sắc về số lượng gói tin, lỗi, cảnh báo, và các chỉ số khác liên quan đến các giao thức mạng như TCP, UDP, ICMP, v.v.

**Giải Thích Các Thông Tin Hiện Ra khi Dùng `netstat -s`**

Kết quả của lệnh `netstat -s` sẽ hiển thị thống kê cho từng **giao thức mạng**. Dưới đây là các ví dụ và giải thích về các thống kê của một số giao thức phổ biến như TCP, UDP, ICMP.

**Ví Dụ về Kết Quả `netstat -s`**

```bash
Tcp:
    11539 segments received
    12345 segments send out
    5 segments retransmited
    0 bad segments received
    0 resets received
    0 connections established
    0 connections reset
    0 segments discarded for bad checksum
    0 segments dropped due to full queues
Udp:
    11539 packets received
    12345 packets sent
    5 packet receive errors
    0 packets dropped
Icmp:
    2345 ICMP messages received
    1234 ICMP messages sent
    10 ICMP input errors
    5 ICMP output errors
```

### **Giải Thích Các Cột và Dữ Liệu trong `netstat -s`**

#### **TCP (Transmission Control Protocol)**

1. **segments received**:
   - **Mô tả**: Số lượng **segements TCP** nhận được từ mạng.
   - **Giải thích**: Một segment TCP là một đơn vị dữ liệu của giao thức TCP.

2. **segments sent out**:
   - **Mô tả**: Số lượng **segment TCP** đã được gửi ra khỏi hệ thống.
   - **Giải thích**: Đây là số gói tin TCP mà hệ thống đã gửi.

3. **segments retransmited**:
   - **Mô tả**: Số lượng **segment TCP** bị **truyền lại** do lỗi (ví dụ, không nhận được ACK).
   - **Giải thích**: Khi một segment không nhận được phản hồi (ACK), hệ thống sẽ thử gửi lại.

4. **bad segments received**:
   - **Mô tả**: Số lượng **segment TCP** bị lỗi khi nhận.
   - **Giải thích**: Các lỗi này có thể liên quan đến vấn đề như lỗi checksum, không hợp lệ hoặc gói tin bị hỏng.

5. **resets received**:
   - **Mô tả**: Số lần hệ thống nhận **phản hồi RESET** từ kết nối TCP.
   - **Giải thích**: Phản hồi RESET xảy ra khi một kết nối TCP bị đóng đột ngột (reset).

6. **connections established**:
   - **Mô tả**: Số lượng **kết nối TCP** đã được thiết lập thành công.
   - **Giải thích**: Đây là số kết nối TCP mà hệ thống đã thiết lập thành công.

7. **connections reset**:
   - **Mô tả**: Số lượng **kết nối TCP** bị **đóng** hoặc reset.
   - **Giải thích**: Kết nối TCP có thể bị đóng khi có lỗi hoặc khi một bên đóng kết nối.

8. **segments discarded for bad checksum**:
   - **Mô tả**: Số lượng **segment TCP** bị **loại bỏ** do lỗi checksum.
   - **Giải thích**: Nếu checksum của một segment không hợp lệ, nó sẽ bị loại bỏ.

9. **segments dropped due to full queues**:
   - **Mô tả**: Số lượng **segment TCP** bị **rớt** do các hàng đợi đầy.
   - **Giải thích**: Khi bộ đệm đầy, các gói tin sẽ bị mất.

#### **UDP (User Datagram Protocol)**

1. **packets received**:
   - **Mô tả**: Số lượng **gói tin UDP** nhận được.
   - **Giải thích**: Đây là số gói tin UDP mà hệ thống đã nhận.

2. **packets sent**:
   - **Mô tả**: Số lượng **gói tin UDP** đã gửi đi.
   - **Giải thích**: Đây là số gói tin UDP mà hệ thống đã gửi.

3. **packet receive errors**:
   - **Mô tả**: Số lượng lỗi khi nhận **gói tin UDP**.
   - **Giải thích**: Các lỗi này có thể liên quan đến gói tin bị hỏng hoặc lỗi khi xử lý.

4. **packets dropped**:
   - **Mô tả**: Số lượng **gói tin UDP** bị **rớt**.
   - **Giải thích**: Gói tin có thể bị rớt do bộ đệm đầy hoặc các vấn đề khác.

#### **ICMP (Internet Control Message Protocol)**

1. **ICMP messages received**:
   - **Mô tả**: Số lượng **tin nhắn ICMP** nhận được.
   - **Giải thích**: Đây là số lượng thông điệp ICMP mà hệ thống nhận được, chẳng hạn như các thông điệp echo request và echo reply.

2. **ICMP messages sent**:
   - **Mô tả**: Số lượng **tin nhắn ICMP** đã gửi đi.
   - **Giải thích**: Đây là số lượng thông điệp ICMP mà hệ thống đã gửi, như các thông điệp echo request.

3. **ICMP input errors**:
   - **Mô tả**: Số lượng lỗi khi nhận **tin nhắn ICMP**.
   - **Giải thích**: Các lỗi này có thể xảy ra khi thông điệp ICMP không hợp lệ hoặc bị hỏng khi nhận.

4. **ICMP output errors**:
   - **Mô tả**: Số lượng lỗi khi gửi **tin nhắn ICMP**.
   - **Giải thích**: Lỗi này có thể xảy ra khi hệ thống không thể gửi một tin nhắn ICMP, ví dụ, khi không thể truy cập đích.

**Các Giao Thức Khác**
Bên cạnh TCP, UDP và ICMP, `netstat -s` còn cung cấp thống kê cho các giao thức khác như:

- **IPv4**: Số lượng gói tin IPv4 gửi và nhận.
- **IPv6**: Số lượng gói tin IPv6 gửi và nhận.
- **TCPv6**: Số lượng kết nối TCP qua IPv6.
- **UDPv6**: Thống kê về các gói UDP qua IPv6.



---------------------


#### 10. **`-c` (Continuous)**
   - Hiển thị các kết quả theo **chu kỳ** (mỗi vài giây cập nhật lại thông tin).
   - **Ví dụ**:
     ```bash
     netstat -c
     ```

#### 11. **`-e` (Extended)**
   - Hiển thị thông tin **mở rộng** về các giao thức, như số lượng gói tin đã truyền, lỗi, v.v.
   - **Ví dụ**:
     ```bash
     netstat -e
     ```

#### 12. **`-v` (Verbose)**
   - Hiển thị thông tin chi tiết hơn về kết nối, trạng thái, và các giao thức.
   - **Ví dụ**:
     ```bash
     netstat -v
     ```

#### 13. **`-g` (Multicast Group)**
   - Hiển thị thông tin về các **nhóm multicast** mà hệ thống đang tham gia.
   - **Ví dụ**:
     ```bash
     netstat -g
     ```

--------------------
     
Lệnh `netstat -g` được sử dụng để hiển thị các thông tin liên quan đến **địa chỉ nhóm đa phát (multicast group addresses)** mà hệ thống đang tham gia. Nhóm đa phát là một nhóm các địa chỉ IP mà nhiều máy tính có thể tham gia để nhận các gói tin cùng một lúc, giúp tiết kiệm băng thông khi truyền tải dữ liệu tới nhiều máy tính.

**Giải Thích Các Cột Khi Dùng Lệnh `netstat -g`**

Kết quả của lệnh `netstat -g` thường bao gồm các thông tin sau:

```bash
IPv4 Multicast Group Memberships
Interface   RefCnt   Group Address     Zone
eth0        2        224.0.0.1         0
eth0        3        224.0.0.251       0
lo          1        224.0.0.1         0

IPv6 Multicast Group Memberships
Interface   RefCnt   Group Address     Zone
eth0        2        ff02::1           0
eth0        3        ff02::fb          0
lo          1        ff02::1           0
```

**Giải Thích Các Cột và Thông Tin trong Kết Quả `netstat -g`**

1. **Interface**:
   - **Mô tả**: Tên của **giao diện mạng** (network interface) mà hệ thống tham gia vào nhóm đa phát.
   - **Ví dụ**: `eth0`, `lo`, v.v.
     - `eth0`: Giao diện Ethernet (giao diện mạng vật lý).
     - `lo`: Giao diện loopback (được sử dụng để giao tiếp với chính máy tính).

2. **RefCnt (Reference Count)**:
   - **Mô tả**: Số lượng các tiến trình hoặc ứng dụng đang tham gia vào nhóm đa phát này.
   - **Giải thích**: Nếu một địa chỉ nhóm đa phát có giá trị `RefCnt > 1`, điều này có nghĩa là có nhiều tiến trình đang sử dụng nhóm đa phát đó. Nếu giá trị là `1`, chỉ có một tiến trình tham gia.

3. **Group Address**:
   - **Mô tả**: Địa chỉ IP của nhóm đa phát mà hệ thống tham gia.
   - **Giải thích**: Đây là địa chỉ nhóm đa phát (multicast address) mà hệ thống đã tham gia. Các địa chỉ nhóm đa phát thường bắt đầu từ `224.0.0.0` đến `233.255.255.255` cho IPv4 và từ `ff00::` cho IPv6.

4. **Zone**:
   - **Mô tả**: Tên vùng (zone) của giao diện mạng (thường là `0` trong hầu hết các trường hợp).
   - **Giải thích**: Đây là thông tin liên quan đến phạm vi của nhóm đa phát. Trong đa số các trường hợp, zone sẽ là `0`, tức là phạm vi toàn cầu. 

**Ví Dụ Giải Thích**

Dưới đây là một ví dụ về kết quả của lệnh `netstat -g`:

```bash
IPv4 Multicast Group Memberships
Interface   RefCnt   Group Address     Zone
eth0        2        224.0.0.1         0
eth0        3        224.0.0.251       0
lo          1        224.0.0.1         0
```

- **eth0** tham gia vào 2 nhóm đa phát: `224.0.0.1` và `224.0.0.251`.
  - Địa chỉ `224.0.0.1` là nhóm đa phát dành cho tất cả các thiết bị trong mạng cục bộ (local network), được sử dụng trong nhiều ứng dụng như **ARP** (Address Resolution Protocol).
  - Địa chỉ `224.0.0.251` là nhóm đa phát dành cho **mDNS** (Multicast DNS).
- **lo** chỉ tham gia vào nhóm đa phát `224.0.0.1` (giao diện loopback).

----------------

#### 14. **`-a` và `-n` kết hợp**
   - Kết hợp các tùy chọn `-a` và `-n` để hiển thị tất cả các kết nối và địa chỉ dưới dạng số.
   - **Ví dụ**:
     ```bash
     netstat -an
     ```

### **Một Số Lệnh Thường Dùng**

1. **Hiển thị tất cả các kết nối TCP và UDP**:
   ```bash
   netstat -at
   netstat -au
   ```

2. **Hiển thị tất cả các cổng đang lắng nghe (Listening ports)**:
   ```bash
   netstat -l
   ```

3. **Hiển thị bảng định tuyến mạng**:
   ```bash
   netstat -r
   ```

4. **Hiển thị thống kê giao thức**:
   ```bash
   netstat -s
   ```

5. **Hiển thị các kết nối đang mở và chương trình sử dụng cổng**:
   ```bash
   sudo netstat -tulnp
   ```

6. **Xem các kết nối TCP đang ESTABLISHED**:
   ```bash
   netstat -t | grep ESTABLISHED
   ```

7. **Hiển thị các kết nối TCP đang chờ (LISTENING)**:
   ```bash
   netstat -tuln
   ```

------------------------------------------

### **tcpdump**

Lệnh `tcpdump` là một công cụ dòng lệnh mạnh mẽ dùng để **bắt gói tin** (packet capture) trên mạng. Nó giúp người dùng phân tích các gói tin đi qua mạng để chẩn đoán sự cố, kiểm tra bảo mật hoặc phân tích lưu lượng mạng. `tcpdump` hỗ trợ nhiều tùy chọn (option) cho phép lọc, ghi lại và phân tích các gói tin.

**Cấu Trúc Lệnh `tcpdump`**

```bash
tcpdump [options] [expression]
```

- **options**: Các tùy chọn cho lệnh (giúp kiểm soát cách `tcpdump` hoạt động).
- **expression**: Các biểu thức lọc (filters) giúp chọn các gói tin bạn muốn bắt.

**Các Tùy Chọn (Options) Thường Dùng trong `tcpdump`**

1. **`-i <interface>`**  
   Chỉ định giao diện mạng mà bạn muốn bắt gói tin.  
   Ví dụ: Bắt gói tin trên giao diện `eth0`:
   ```bash
   tcpdump -i eth0
   ```

2. **`-n`**  
   Hiển thị địa chỉ IP thay vì tên miền (DNS resolution).  
   Ví dụ:
   ```bash
   tcpdump -n
   ```

3. **`-v`, `-vv`, `-vvv`**  
   Độ chi tiết của thông tin. Sử dụng nhiều lần để tăng mức độ chi tiết.  
   - `-v`: Thông tin chi tiết về gói tin.
   - `-vv`: Chi tiết hơn.
   - `-vvv`: Thông tin đầy đủ nhất về gói tin.
   ```bash
   tcpdump -vv
   ```

4. **`-c <count>`**  
   Chỉ bắt một số lượng gói tin nhất định.  
   Ví dụ: Bắt 10 gói tin:
   ```bash
   tcpdump -c 10
   ```

5. **`-w <file>`**  
   Ghi gói tin vào một file (thay vì in ra màn hình). Dữ liệu sẽ được lưu dưới định dạng pcap.  
   Ví dụ: Ghi gói tin vào file `capture.pcap`:
   ```bash
   tcpdump -w capture.pcap
   ```

6. **`-r <file>`**  
   Đọc và phân tích các gói tin từ một file đã lưu (dưới định dạng pcap).  
   Ví dụ: Đọc file `capture.pcap`:
   ```bash
   tcpdump -r capture.pcap
   ```

7. **`-s <snaplen>`**  
   Xác định độ dài tối đa của mỗi gói tin được bắt (snap length). Giá trị mặc định là 262144 byte. Nếu bạn chỉ cần bắt đầu gói tin, có thể đặt giá trị này thấp hơn.  
   Ví dụ: Bắt 100 byte đầu của mỗi gói tin:
   ```bash
   tcpdump -s 100
   ```

8. **`-X`**  
   Hiển thị dữ liệu của gói tin ở dạng **hex và ASCII**.  
   Ví dụ:
   ```bash
   tcpdump -X
   ```

9. **`-A`**  
   Hiển thị nội dung của gói tin ở dạng **ASCII** (tương tự `-X`, nhưng không có dữ liệu hex).  
   Ví dụ:
   ```bash
   tcpdump -A
   ```

10. **`-q`**  
    Giảm thiểu thông tin chi tiết về gói tin. Hiển thị thông tin cơ bản như địa chỉ IP nguồn và đích, số hiệu giao thức, v.v.  
    Ví dụ:
    ```bash
    tcpdump -q
    ```

11. **`-e`**  
    Hiển thị địa chỉ MAC (thêm thông tin liên quan đến Ethernet header).  
    Ví dụ:
    ```bash
    tcpdump -e
    ```

12. **`-p`**  
    Tắt chế độ **promiscuous** (chế độ mà card mạng bắt mọi gói tin trên mạng, không chỉ những gói tin gửi đến địa chỉ của nó).  
    Ví dụ:
    ```bash
    tcpdump -p
    ```

13. **`-l`**  
    Làm cho `tcpdump` xuất thông tin ra **stdout** theo dòng, có thể dùng cho việc ghi log.  
    Ví dụ:
    ```bash
    tcpdump -l
    ```

14. **`-S`**  
    Hiển thị số thứ tự của gói tin TCP trong dạng **absolute sequence numbers** (thứ tự tuyệt đối), thay vì sử dụng các số thứ tự tương đối.  
    Ví dụ:
    ```bash
    tcpdump -S
    ```

**Các Biểu Thức Lọc (Filters)**

`tcpdump` hỗ trợ các biểu thức lọc mạnh mẽ để chọn các gói tin bạn muốn bắt. Dưới đây là một số ví dụ về biểu thức lọc:

1. **Lọc theo giao thức**
   - Lọc các gói TCP:
     ```bash
     tcpdump tcp
     ```
   - Lọc các gói UDP:
     ```bash
     tcpdump udp
     ```
   - Lọc các gói ICMP:
     ```bash
     tcpdump icmp
     ```

2. **Lọc theo địa chỉ IP**
   - Lọc các gói tin từ địa chỉ IP nguồn là `192.168.1.1`:
     ```bash
     tcpdump src 192.168.1.1
     ```
   - Lọc các gói tin đến địa chỉ IP đích là `192.168.1.2`:
     ```bash
     tcpdump dst 192.168.1.2
     ```
   - Lọc các gói tin giữa `192.168.1.1` và `192.168.1.2`:
     ```bash
     tcpdump host 192.168.1.1 and 192.168.1.2
     ```

3. **Lọc theo cổng**
   - Lọc các gói TCP có cổng nguồn là 80 (HTTP):
     ```bash
     tcpdump tcp src port 80
     ```
   - Lọc các gói UDP có cổng đích là 53 (DNS):
     ```bash
     tcpdump udp dst port 53
     ```

4. **Lọc theo giao thức và địa chỉ IP**
   - Lọc các gói tin UDP giữa `192.168.1.1` và `192.168.1.2`:
     ```bash
     tcpdump udp and host 192.168.1.1 and 192.168.1.2
     ```

5. **Lọc theo loại dịch vụ**
   - Lọc các gói tin TCP có cờ **SYN** (thường được dùng để bắt đầu một kết nối TCP):
     ```bash
     tcpdump 'tcp[tcpflags] & tcp-syn != 0'
     ```

**Ví Dụ Cụ Thể**

1. **Bắt gói tin trên giao diện `eth0` và hiển thị thông tin chi tiết**
   ```bash
   tcpdump -i eth0 -v
   ```

2. **Bắt 10 gói tin TCP từ địa chỉ IP `192.168.1.100`**
   ```bash
   tcpdump -i eth0 tcp and src host 192.168.1.100 -c 10
   ```

3. **Bắt gói tin UDP trên cổng 53 (DNS) và ghi vào file**
   ```bash
   tcpdump -i eth0 udp port 53 -w dns_traffic.pcap
   ```

4. **Bắt tất cả các gói tin ICMP (ping)**
   ```bash
   tcpdump icmp
   ```

---------------------

Khi sử dụng `tcpdump`, bạn sẽ thấy các thông tin liên quan đến gói tin (packet) đang được bắt, bao gồm các chi tiết về giao thức, địa chỉ IP, cổng, loại dữ liệu, và nhiều thông tin khác. Dưới đây là một số thông tin phổ biến bạn sẽ thấy trong kết quả của lệnh `tcpdump` và ý nghĩa của chúng.

**Cấu Trúc Một Dòng Kết Quả Của `tcpdump`**
Khi chạy `tcpdump`, một dòng kết quả sẽ chứa thông tin về gói tin bắt được, ví dụ như sau:

```bash
13:45:23.541647 IP 192.168.1.1.80 > 192.168.1.2.12345: Flags [S], seq 123456789, ack 0, win 65535, length 0
```

**Giải Thích Các Thành Phần Trong Một Dòng Kết Quả**

1. **Thời gian**:
   - **Mô tả**: Thời gian hiện tại khi gói tin được bắt. `tcpdump` sẽ hiển thị thời gian với định dạng `HH:MM:SS.ssssss` (giờ, phút, giây và phần thập phân của giây).
   - **Ví dụ**: `13:45:23.541647` — gói tin được bắt vào lúc 13 giờ 45 phút 23 giây và 541647 micro giây.

2. **Giao thức (Protocol)**:
   - **Mô tả**: Giao thức mạng của gói tin đang được phân tích, ví dụ: `IP`, `TCP`, `UDP`, `ARP`, `ICMP`, v.v.
   - **Ví dụ**: `IP` — gói tin này là một gói tin IP.

3. **Địa chỉ IP và cổng (Source and Destination IP & Port)**:
   - **Mô tả**: Địa chỉ IP và cổng (port) của máy nguồn và máy đích trong giao tiếp mạng.
   - **Cấu trúc**: `source_ip.source_port > destination_ip.destination_port`
     - `source_ip`: Địa chỉ IP của máy gửi.
     - `source_port`: Cổng của máy gửi (chỉ áp dụng với các giao thức như TCP/UDP).
     - `destination_ip`: Địa chỉ IP của máy nhận.
     - `destination_port`: Cổng của máy nhận (chỉ áp dụng với các giao thức như TCP/UDP).
   - **Ví dụ**: `192.168.1.1.80 > 192.168.1.2.12345` — Gói tin đi từ địa chỉ IP `192.168.1.1` với cổng `80` (HTTP) đến địa chỉ IP `192.168.1.2` với cổng `12345`.

4. **Flags**:
   - **Mô tả**: Cờ (flags) của gói tin, chủ yếu liên quan đến giao thức TCP. Các cờ phổ biến bao gồm:
     - **S**: SYN — dùng để bắt đầu một kết nối TCP.
     - **F**: FIN — yêu cầu kết thúc kết nối TCP.
     - **P**: PUSH — yêu cầu truyền ngay lập tức dữ liệu.
     - **R**: RST — yêu cầu thiết lập lại kết nối.
     - **A**: ACK — xác nhận gói tin trước đó.
   - **Ví dụ**: `Flags [S]` — Đây là một gói SYN, dùng để thiết lập kết nối.

5. **Số thứ tự (Sequence number) và xác nhận (Acknowledgment number)**:
   - **Mô tả**: Trong TCP, mỗi gói tin có một số thứ tự (sequence number) và số xác nhận (acknowledgment number) để đảm bảo tính toàn vẹn của dữ liệu và kiểm soát lưu lượng.
   - **Ví dụ**: `seq 123456789, ack 0` — Số thứ tự của gói tin là `123456789`, số xác nhận là `0` (chưa có gói tin nào được xác nhận).

6. **Cửa sổ (Window size)**:
   - **Mô tả**: Cửa sổ (window size) xác định số lượng byte mà máy nhận có thể tiếp nhận mà không cần xác nhận lại.
   - **Ví dụ**: `win 65535` — Cửa sổ của gói tin này có kích thước là `65535` byte.

7. **Chiều dài gói tin (Length)**:
   - **Mô tả**: Chiều dài của gói tin dữ liệu (được đo bằng byte).
   - **Ví dụ**: `length 0` — Gói tin này không chứa dữ liệu (chỉ là gói tin điều khiển như SYN).

**Ví Dụ Kết Quả Của Lệnh `tcpdump`**
Dưới đây là một ví dụ khác về kết quả của `tcpdump`:

```bash
13:45:23.541647 IP 192.168.1.1.80 > 192.168.1.2.12345: Flags [S], seq 123456789, ack 0, win 65535, length 0
13:45:23.541702 IP 192.168.1.2.12345 > 192.168.1.1.80: Flags [S.], seq 987654321, ack 123456790, win 65535, length 0
13:45:23.541715 IP 192.168.1.1.80 > 192.168.1.2.12345: Flags [P.], seq 123456790:123456800, ack 987654322, win 65535, length 10
```

1. **Gói tin SYN** từ `192.168.1.1` (cổng 80) đến `192.168.1.2` (cổng 12345).
2. **Gói tin SYN-ACK** từ `192.168.1.2` (cổng 12345) đến `192.168.1.1` (cổng 80), xác nhận gói SYN trước đó.
3. **Gói tin PUSH** từ `192.168.1.1` (cổng 80) đến `192.168.1.2` (cổng 12345), gửi dữ liệu 10 byte.

**Tóm Tắt Các Thành Phần Chính Của Một Dòng `tcpdump`:**
- **Thời gian**: Thời gian bắt gói tin.
- **Giao thức**: Giao thức sử dụng trong gói tin (IP, TCP, UDP, ICMP, v.v.).
- **Địa chỉ nguồn và đích**: Địa chỉ IP và cổng của máy gửi và nhận.
- **Flags**: Cờ (flags) trong giao thức (đặc biệt đối với TCP).
- **Số thứ tự và xác nhận**: Số thứ tự và số xác nhận của gói tin trong giao thức TCP.
- **Cửa sổ**: Kích thước cửa sổ nhận của TCP.
- **Chiều dài gói tin**: Kích thước dữ liệu của gói tin (hoặc `0` nếu là gói tin điều khiển).


