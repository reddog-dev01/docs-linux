### **ip link**

Lệnh `ip link` trong Linux là một công cụ mạnh mẽ để quản lý các giao diện mạng trên hệ thống. Dưới đây là cách sử dụng `ip link` cùng các tuỳ chọn phổ biến trong Linux:

### Cấu trúc lệnh cơ bản:
```bash
ip link [OPTION] [INTERFACE]
```

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

---

