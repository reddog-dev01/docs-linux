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

