### **5. Managing Users and Groups**

5.1 `useradd`
Lệnh `useradd` trong Linux là một công cụ quan trọng được sử dụng để tạo một tài khoản người dùng mới. 

**Các Tùy Chọn Phổ Biến của `useradd`**

- **`-c, --comment COMMENT`**
  - Thiết lập trường GECOS, thường được sử dụng để lưu trữ thông tin bổ sung về người dùng, chẳng hạn như tên đầy đủ của người dùng.
  ```bash
  useradd -c "John Doe" username
  ```

- **`-d, --home HOME_DIR`**
  - Đặt thư mục home cho tài khoản mới. Nếu không được chỉ định, hệ thống sẽ tạo một thư mục mặc định theo quy tắc đặt trong `/etc/default/useradd` hoặc sử dụng `/home/username`.
  ```bash
  useradd -d /path/to/home username
  ```

- **`-e, --expiredate EXPIRE_DATE`**
  - Đặt ngày hết hạn cho tài khoản người dùng, theo định dạng YYYY-MM-DD.
  ```bash
  useradd -e 2024-12-31 username
  ```

- **`-f, --inactive INACTIVE`**
  - Đặt số ngày sau khi mật khẩu hết hạn mà tài khoản sẽ bị vô hiệu hóa. Nếu được đặt thành 0, tài khoản sẽ bị vô hiệu hóa ngay sau khi mật khẩu hết hạn.
  ```bash
  useradd -f 30 username
  ```

- **`-g, --gid GROUP`**
  - Đặt nhóm chính (GID) cho tài khoản người dùng. Bạn có thể chỉ định một nhóm bằng tên hoặc số.
  ```bash
  useradd -g users username
  ```

- **`-G, --groups GROUPS`**
  - Thêm người dùng vào các nhóm bổ sung. Danh sách các nhóm được phân tách bởi dấu phẩy.
  ```bash
  useradd -G wheel,admin username
  ```

- **`-m, --create-home`**
  - Tự động tạo thư mục home cho tài khoản mới.
  ```bash
  useradd -m username
  ```

- **`-M`**
  - Không tạo thư mục home, ngay cả khi có chỉ thị khác trong cấu hình mặc định.
  ```bash
  useradd -M username
  ```

- **`-s, --shell SHELL`**
  - Đặt shell đăng nhập cho tài khoản này.
  ```bash
  useradd -s /bin/zsh username
  ```

- **`-u, --uid UID`**
  - Đặt ID người dùng (UID) cho tài khoản. Điều này hữu ích cho việc thiết lập tương quan UID giữa các máy trong một môi trường mạng.
  ```bash
  useradd -u 1101 username
  ```
  
Khi tạo người dùng mới, bạn cần chú ý đến việc thiết lập mật khẩu cho người dùng mới đó ngay sau khi tạo tài khoản, sử dụng lệnh `passwd` để thiết lập mật khẩu:
```bash
sudo passwd username
```

**5.2 `groupadd`**

Lệnh `groupadd` trong Linux là một công cụ dùng để tạo mới một nhóm người dùng. Việc tạo nhóm cho phép bạn quản lý quyền truy cập cho một nhóm người dùng, giúp việc phân quyền trở nên đơn giản và dễ dàng hơn.

Cú pháp Cơ Bản của `groupadd`
```bash
groupadd [options] groupname
```

**Các Tùy Chọn Phổ Biến**

- **`-g, --gid GID`**: Đặt số ID nhóm (GID) cụ thể khi tạo nhóm. GID phải là một số không âm. Việc chỉ định GID giúp đảm bảo tính nhất quán trong hệ thống hoặc trong một môi trường mạng.
  ```bash
  groupadd -g 1001 groupname
  ```

- **`-o, --non-unique`**: Cho phép tạo nhóm với một GID đã được sử dụng (không độc nhất).
  ```bash
  groupadd -o -g 1001 groupname
  ```

- **`-r, --system`**: Tạo một nhóm hệ thống. Nhóm hệ thống thường có GID trong một khoảng định trước. Tùy chọn này thường được sử dụng cho các nhóm được tạo tự động bởi các gói phần mềm cài đặt trên hệ thống.
  ```bash
  groupadd -r groupname
  ```

- **`-f, --force`**: Nếu nhóm đã tồn tại, lệnh sẽ kết thúc mà không có lỗi nếu tùy chọn này được sử dụng. Đồng thời, nếu tùy chọn `-g` được sử dụng và GID đã tồn tại, tùy chọn này sẽ cũng sẽ kết thúc mà không có lỗi.
  ```bash
  groupadd -f groupname
  ```

**5.3 `usermod`**

 công cụ dùng để sửa đổi các cài đặt của tài khoản người dùng đã tồn tại.

Cú pháp Cơ Bản của `usermod`

```bash
usermod [options] username
```

**Các Tùy Chọn Phổ Biến của `usermod`**

- **`-d, --home HOME_DIR`**: Thay đổi thư mục nhà của người dùng. Sử dụng tùy chọn `-m` để di chuyển nội dung của thư mục nhà cũ vào thư mục mới.
  ```bash
  usermod -d /new/home/dir -m username
  ```

- **`-l, --login NEW_LOGIN`**: Thay đổi tên đăng nhập của người dùng.
  ```bash
  usermod -l newusername username
  ```

- **`-s, --shell SHELL`**: Thay đổi shell mặc định của người dùng.
  ```bash
  usermod -s /bin/zsh username
  ```

- **`-g, --gid GROUP`**: Thay đổi nhóm chính (GID) của người dùng.
  ```bash
  usermod -g newgroup username
  ```

- **`-G, --groups GROUPS`**: Thêm người dùng vào các nhóm bổ sung. Danh sách nhóm phân cách bằng dấu phẩy và không có khoảng trắng.
  ```bash
  usermod -G group1,group2 username
  ```

- **`-a, --append`**: Khi sử dụng với tùy chọn `-G`, thêm người dùng vào các nhóm liệt kê mà không xóa người dùng khỏi các nhóm khác.
  ```bash
  usermod -aG group1,group2 username
  ```

- **`-L, --lock`**: Khóa mật khẩu của người dùng, làm cho tài khoản không thể đăng nhập.
  ```bash
  usermod -L username
  ```

- **`-U, --unlock`**: Mở khóa mật khẩu của người dùng, cho phép đăng nhập trở lại.
  ```bash
  usermod -U username
  ```

- **`-c, --comment COMMENT`**: Thay đổi trường GECOS của người dùng, thường được sử dụng để lưu trữ thông tin như tên đầy đủ.
  ```bash
  usermod -c "New User GECOS" username
  ```

**5.4 `groupmod`**

sử dụng để sửa đổi các thuộc tính của nhóm đã tồn tại. Bạn có thể thay đổi tên nhóm hoặc số nhóm (GID) bằng lệnh này

Cú pháp Cơ Bản của `groupmod`

```bash
groupmod [options] groupname
```

**Các Tùy Chọn Phổ Biến của `groupmod`**

- **`-n, --new-name NEW_GROUP_NAME`**: Sử dụng tùy chọn này để thay đổi tên của nhóm. Đây là tùy chọn thông dụng khi bạn muốn đổi tên nhóm để phản ánh chức năng hoặc vai trò mới của nhóm.
  
  ```bash
  sudo groupmod -n newgroupname oldgroupname
  ```

- **`-g, --gid GID`**: Thay đổi số nhận dạng nhóm (GID). Việc thay đổi GID có thể ảnh hưởng đến các file hoặc thư mục được gán cho nhóm đó, vì các file này liên kết với GID.
  
  ```bash
  sudo groupmod -g 1002 groupname
  ```

- **`-o, --non-unique`**: Cho phép bạn đặt một GID không duy nhất, điều này có nghĩa là bạn có thể đặt GID mà đã được sử dụng bởi một nhóm khác.
  
  ```bash
  sudo groupmod -o -g existing_gid groupname
  ```
  
**5.5 `passwd`**

Cú pháp Cơ Bản của `passwd`

```bash
passwd [options] [user]
```

Nếu không có tên người dùng được chỉ định, lệnh `passwd` sẽ thay đổi mật khẩu của người dùng hiện tại. Nếu là quản trị viên (root), bạn có thể thay đổi mật khẩu cho bất kỳ người dùng nào.

**Các Tùy Chọn Phổ Biến của `passwd`**

- **`-l, --lock`**: Khóa mật khẩu của người dùng. Điều này ngăn không cho người dùng đăng nhập sử dụng mật khẩu (họ có thể đăng nhập bằng các phương pháp khác, như SSH key).
  
  ```bash
  sudo passwd -l username
  ```

- **`-u, --unlock`**: Mở khóa mật khẩu của người dùng, cho phép họ đăng nhập lại bằng mật khẩu của họ.
  
  ```bash
  sudo passwd -u username
  ```

- **`-d, --delete`**: Xóa mật khẩu của người dùng, làm cho tài khoản không có mật khẩu.
  
  ```bash
  sudo passwd -d username
  ```

- **`-e, --expire`**: Ngay lập tức đặt mật khẩu của người dùng để hết hạn, buộc người dùng phải thay đổi mật khẩu lần tiếp theo khi đăng nhập.
  
  ```bash
  sudo passwd -e username
  ```

- **`-n, --mindays DAYS`**: Đặt số ngày tối thiểu trước khi mật khẩu có thể được thay đổi.
  
  ```bash
  sudo passwd -n 7 username
  ```

- **`-x, --maxdays DAYS`**: Đặt số ngày tối đa mà mật khẩu vẫn còn hợp lệ trước khi phải thay đổi.
  
  ```bash
  sudo passwd -x 90 username
  ```

- **`-w, --warndays DAYS`**: Đặt số ngày trước khi mật khẩu hết hạn mà người dùng sẽ bắt đầu nhận được cảnh báo để thay đổi mật khẩu.
  
  ```bash
  sudo passwd -w 10 username
  ```

**5.6 `userdel`** 

Lệnh `userdel` trong Linux được sử dụng để xóa người dùng khỏi hệ thống. Lệnh này thực hiện bằng cách xóa các mục liên quan đến người dùng từ các tệp như `/etc/passwd`, `/etc/shadow`, và các tệp khác có thông tin người dùng.

Cú pháp Cơ Bản của `userdel`

```bash
userdel [options] USERNAME
```

**Các Tùy Chọn Phổ Biến của `userdel`**

- **`-r, --remove`**: Tùy chọn này sẽ xóa không chỉ mục nhập người dùng khỏi các tệp cấu hình hệ thống, mà còn xóa thư mục home của người dùng và các file thư tín khác trên hệ thống.
  
  ```bash
  sudo userdel -r username
  ```

- **`-f, --force`**: Tùy chọn này buộc xóa người dùng, ngay cả khi người dùng vẫn đang đăng nhập hoặc nếu không thể cập nhật các tệp mật khẩu. Tùy chọn này nên được sử dụng cẩn thận vì nó có thể để lại một số tệp không được xóa sạch.

  ```bash
  sudo userdel -f username
  ```

- **`--backup`**: Tạo bản sao lưu của các tệp được xóa do xóa người dùng. Điều này hữu ích nếu bạn muốn đảm bảo có thể khôi phục dữ liệu sau khi xóa người dùng.
  
  ```bash
  sudo userdel --backup username
  ```

**5.7 `groupdel`**

Cú pháp Cơ Bản của `groupdel`

```bash
groupdel groupname
```

### **6. Using System Log Files: syslogd, rotating log files**

### **7. Running Job in the Future: `cron`, `at`**
