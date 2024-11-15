### **5. Managing Users and Groups**

5.1 `useradd`
Lệnh `useradd` trong Linux là một công cụ quan trọng được sử dụng để tạo một tài khoản người dùng mới. Lệnh này có nhiều tùy chọn cho phép bạn tùy chỉnh tài khoản người dùng ngay từ khi tạo. Dưới đây là các tùy chọn phổ biến và hữu ích mà bạn có thể sử dụng với lệnh `useradd`:

### Các Tùy Chọn Phổ Biến của `useradd`

- **-c, --comment COMMENT**
  - Thiết lập trường GECOS, thường được sử dụng để lưu trữ thông tin bổ sung về người dùng, chẳng hạn như tên đầy đủ của người dùng.
  ```bash
  useradd -c "John Doe" username
  ```

- **-d, --home HOME_DIR**
  - Đặt thư mục home cho tài khoản mới. Nếu không được chỉ định, hệ thống sẽ tạo một thư mục mặc định theo quy tắc đặt trong `/etc/default/useradd` hoặc sử dụng `/home/username`.
  ```bash
  useradd -d /path/to/home username
  ```

- **-e, --expiredate EXPIRE_DATE**
  - Đặt ngày hết hạn cho tài khoản người dùng, theo định dạng YYYY-MM-DD.
  ```bash
  useradd -e 2024-12-31 username
  ```

- **-f, --inactive INACTIVE**
  - Đặt số ngày sau khi mật khẩu hết hạn mà tài khoản sẽ bị vô hiệu hóa. Nếu được đặt thành 0, tài khoản sẽ bị vô hiệu hóa ngay sau khi mật khẩu hết hạn.
  ```bash
  useradd -f 30 username
  ```

- **-g, --gid GROUP**
  - Đặt nhóm chính (GID) cho tài khoản người dùng. Bạn có thể chỉ định một nhóm bằng tên hoặc số.
  ```bash
  useradd -g users username
  ```

- **-G, --groups GROUPS**
  - Thêm người dùng vào các nhóm bổ sung. Danh sách các nhóm được phân tách bởi dấu phẩy.
  ```bash
  useradd -G wheel,admin username
  ```

- **-m, --create-home**
  - Tự động tạo thư mục home cho tài khoản mới.
  ```bash
  useradd -m username
  ```

- **-M**
  - Không tạo thư mục home, ngay cả khi có chỉ thị khác trong cấu hình mặc định.
  ```bash
  useradd -M username
  ```

- **-s, --shell SHELL**
  - Đặt shell đăng nhập cho tài khoản này.
  ```bash
  useradd -s /bin/zsh username
  ```

- **-u, --uid UID**
  - Đặt ID người dùng (UID) cho tài khoản. Điều này hữu ích cho việc thiết lập tương quan UID giữa các máy trong một môi trường mạng.
  ```bash
  useradd -u 1101 username
  ```

### Lưu Ý
Khi tạo người dùng mới, bạn cần chú ý đến việc thiết lập mật khẩu cho người dùng mới đó ngay sau khi tạo tài khoản, sử dụng lệnh `passwd` để thiết lập mật khẩu:
```bash
sudo passwd username
```

Ngoài ra, nếu không có các tùy chọn tương ứng, một số thiết lập như thư mục home, shell, và nhóm sẽ được áp dụng dựa trên các cài đặt mặc định được định nghĩa trong các file cấu hình như `/etc/default/useradd` hoặc `/etc/login.defs`.

5.2 

Lệnh `groupadd` trong Linux là một công cụ dùng để tạo mới một nhóm người dùng. Việc tạo nhóm cho phép bạn quản lý quyền truy cập cho một nhóm người dùng, giúp việc phân quyền trở nên đơn giản và dễ dàng hơn. Đây là cách để áp dụng các chính sách an ninh và quản lý người dùng hiệu quả.

### Cú pháp Cơ Bản của `groupadd`
```bash
groupadd [options] groupname
```

### Các Tùy Chọn Phổ Biến

- **-g, --gid GID**: Đặt số ID nhóm (GID) cụ thể khi tạo nhóm. GID phải là một số không âm. Việc chỉ định GID giúp đảm bảo tính nhất quán trong hệ thống hoặc trong một môi trường mạng.
  ```bash
  groupadd -g 1001 groupname
  ```

- **-o, --non-unique**: Cho phép tạo nhóm với một GID đã được sử dụng (không độc nhất).
  ```bash
  groupadd -o -g 1001 groupname
  ```

- **-r, --system**: Tạo một nhóm hệ thống. Nhóm hệ thống thường có GID trong một khoảng định trước. Tùy chọn này thường được sử dụng cho các nhóm được tạo tự động bởi các gói phần mềm cài đặt trên hệ thống.
  ```bash
  groupadd -r groupname
  ```

- **-f, --force**: Nếu nhóm đã tồn tại, lệnh sẽ kết thúc mà không có lỗi nếu tùy chọn này được sử dụng. Đồng thời, nếu tùy chọn `-g` được sử dụng và GID đã tồn tại, tùy chọn này sẽ cũng sẽ kết thúc mà không có lỗi.
  ```bash
  groupadd -f groupname
  ```

### Ví dụ
1. **Tạo Nhóm Mới**
   ```bash
   sudo groupadd mynewgroup
   ```
   Lệnh này tạo một nhóm mới có tên là `mynewgroup`.

2. **Tạo Nhóm với GID Xác Định**
   ```bash
   sudo groupadd -g 9999 customgroup
   ```
   Lệnh này tạo một nhóm mới có tên là `customgroup` với GID là `9999`.

### Lưu Ý
- Bạn cần quyền quản trị (root) để thực hiện hầu hết các thao tác với `groupadd`.
- Các tùy chọn và cách sử dụng `groupadd` có thể khác nhau một chút tùy vào từng bản phân phối Linux. Luôn tham khảo trang man (`man groupadd`) trên hệ thống của bạn để biết thông tin chính xác nhất.
- Khi tạo nhóm, cần phải đảm bảo không trùng lặp GID với nhóm khác, trừ khi bạn có mục đích rõ ràng và sử dụng tùy chọn `-o`.

`groupadd` là một công cụ cơ bản nhưng cần thiết cho quản trị viên hệ thống để quản lý nhóm người dùng một cách hiệu quả, đặc biệt là trong môi trường có nhiều người dùng và các chính sách bảo mật nghiêm ngặt.

5.3 

Lệnh `usermod` trong Linux là công cụ dùng để sửa đổi các cài đặt của tài khoản người dùng đã tồn tại. Lệnh này cho phép bạn thay đổi các thuộc tính như tên người dùng, thư mục nhà, shell mặc định, nhóm, và các thông tin khác.

### Cú pháp Cơ Bản của `usermod`

```bash
usermod [options] username
```

### Các Tùy Chọn Phổ Biến của `usermod`

- **-d, --home HOME_DIR**: Thay đổi thư mục nhà của người dùng. Sử dụng tùy chọn `-m` để di chuyển nội dung của thư mục nhà cũ vào thư mục mới.
  ```bash
  usermod -d /new/home/dir -m username
  ```

- **-l, --login NEW_LOGIN**: Thay đổi tên đăng nhập của người dùng.
  ```bash
  usermod -l newusername username
  ```

- **-s, --shell SHELL**: Thay đổi shell mặc định của người dùng.
  ```bash
  usermod -s /bin/zsh username
  ```

- **-g, --gid GROUP**: Thay đổi nhóm chính (GID) của người dùng.
  ```bash
  usermod -g newgroup username
  ```

- **-G, --groups GROUPS**: Thêm người dùng vào các nhóm bổ sung. Danh sách nhóm phân cách bằng dấu phẩy và không có khoảng trắng.
  ```bash
  usermod -G group1,group2 username
  ```

- **-a, --append**: Khi sử dụng với tùy chọn `-G`, thêm người dùng vào các nhóm liệt kê mà không xóa người dùng khỏi các nhóm khác.
  ```bash
  usermod -aG group1,group2 username
  ```

- **-L, --lock**: Khóa mật khẩu của người dùng, làm cho tài khoản không thể đăng nhập.
  ```bash
  usermod -L username
  ```

- **-U, --unlock**: Mở khóa mật khẩu của người dùng, cho phép đăng nhập trở lại.
  ```bash
  usermod -U username
  ```

- **-c, --comment COMMENT**: Thay đổi trường GECOS của người dùng, thường được sử dụng để lưu trữ thông tin như tên đầy đủ.
  ```bash
  usermod -c "New User GECOS" username
  ```

### Lưu Ý Khi Sử Dụng `usermod`

- Bạn cần có quyền quản trị (root) để thực hiện các thay đổi với lệnh `usermod`.
- Hãy cẩn thận khi sửa đổi các thuộc tính như tên người dùng hoặc thư mục nhà, vì điều này có thể ảnh hưởng đến khả năng truy cập và quyền của tài khoản đó.
- Đảm bảo rằng nhóm mới hoặc shell mà bạn gán cho người dùng thực sự tồn tại trên hệ thống.
- Thay đổi tên đăng nhập có thể ảnh hưởng đến quyền truy cập đến các tài nguyên mà được cấu hình cho tên người dùng cũ.

`usermod` là công cụ linh hoạt giúp quản trị viên có thể dễ dàng điều chỉnh cấu hình tài khoản người dùng để phù hợp với các yêu cầu bảo mật hoặc tổ chức, đảm bảo tài khoản được cấu hình đúng đắn theo thời gian.

5.4 

Lệnh `groupmod` trong Linux được sử dụng để sửa đổi các thuộc tính của nhóm đã tồn tại. Bạn có thể thay đổi tên nhóm hoặc số nhóm (GID) bằng lệnh này. Đây là một công cụ quan trọng trong quản lý người dùng và nhóm, cho phép bạn bảo trì cấu hình nhóm một cách hiệu quả.

### Cú pháp Cơ Bản của `groupmod`

```bash
groupmod [options] groupname
```

### Các Tùy Chọn Phổ Biến của `groupmod`

- **-n, --new-name NEW_GROUP_NAME**: Sử dụng tùy chọn này để thay đổi tên của nhóm. Đây là tùy chọn thông dụng khi bạn muốn đổi tên nhóm để phản ánh chức năng hoặc vai trò mới của nhóm.
  
  ```bash
  sudo groupmod -n newgroupname oldgroupname
  ```

- **-g, --gid GID**: Thay đổi số nhận dạng nhóm (GID). Việc thay đổi GID có thể ảnh hưởng đến các file hoặc thư mục được gán cho nhóm đó, vì các file này liên kết với GID.
  
  ```bash
  sudo groupmod -g 1002 groupname
  ```

- **-o, --non-unique**: Cho phép bạn đặt một GID không duy nhất, điều này có nghĩa là bạn có thể đặt GID mà đã được sử dụng bởi một nhóm khác.
  
  ```bash
  sudo groupmod -o -g existing_gid groupname
  ```

### Lưu Ý Khi Sử Dụng `groupmod`

- **Quyền truy cập**: Bạn cần có quyền quản trị (root) để sử dụng `groupmod` để thay đổi thuộc tính của nhóm.
- **Ảnh hưởng đến File Hệ Thống**: Thay đổi GID của nhóm có thể dẫn đến việc không truy cập được các file mà nhóm đã có quyền, vì các quyền truy cập trong Linux phần lớn dựa trên GID. Bạn cần cập nhật GID trên các file liên quan để đảm bảo quyền truy cập không bị ảnh hưởng.
- **Cẩn thận khi đổi tên nhóm**: Đổi tên nhóm có thể gây nhầm lẫn hoặc các vấn đề về quyền truy cập nếu các script hoặc dịch vụ dựa vào tên nhóm đó để kiểm soát truy cập.

`groupmod` là một công cụ quản lý nhóm linh hoạt, giúp đảm bảo cấu trúc và quyền của nhóm trong hệ thống luôn phù hợp với yêu cầu tổ chức và bảo mật.

5.5

Lệnh `passwd` trong Linux là công cụ được sử dụng để thay đổi mật khẩu của người dùng. Lệnh này quan trọng trong quản lý tài khoản, cho phép người dùng hoặc quản trị viên cập nhật mật khẩu an toàn cho các tài khoản.

### Cú pháp Cơ Bản của `passwd`

```bash
passwd [options] [user]
```

Nếu không có tên người dùng được chỉ định, lệnh `passwd` sẽ thay đổi mật khẩu của người dùng hiện tại. Nếu là quản trị viên (root), bạn có thể thay đổi mật khẩu cho bất kỳ người dùng nào.

### Các Tùy Chọn Phổ Biến của `passwd`

- **-l, --lock**: Khóa mật khẩu của người dùng. Điều này ngăn không cho người dùng đăng nhập sử dụng mật khẩu (họ có thể đăng nhập bằng các phương pháp khác, như SSH key).
  
  ```bash
  sudo passwd -l username
  ```

- **-u, --unlock**: Mở khóa mật khẩu của người dùng, cho phép họ đăng nhập lại bằng mật khẩu của họ.
  
  ```bash
  sudo passwd -u username
  ```

- **-d, --delete**: Xóa mật khẩu của người dùng, làm cho tài khoản không có mật khẩu.
  
  ```bash
  sudo passwd -d username
  ```

- **-e, --expire**: Ngay lập tức đặt mật khẩu của người dùng để hết hạn, buộc người dùng phải thay đổi mật khẩu lần tiếp theo khi đăng nhập.
  
  ```bash
  sudo passwd -e username
  ```

- **-n, --mindays DAYS**: Đặt số ngày tối thiểu trước khi mật khẩu có thể được thay đổi.
  
  ```bash
  sudo passwd -n 7 username
  ```

- **-x, --maxdays DAYS**: Đặt số ngày tối đa mà mật khẩu vẫn còn hợp lệ trước khi phải thay đổi.
  
  ```bash
  sudo passwd -x 90 username
  ```

- **-w, --warndays DAYS**: Đặt số ngày trước khi mật khẩu hết hạn mà người dùng sẽ bắt đầu nhận được cảnh báo để thay đổi mật khẩu.
  
  ```bash
  sudo passwd -w 10 username
  ```

### Ví dụ Sử Dụng `passwd`

1. **Thay Đổi Mật Khẩu của Người Dùng Hiện Tại:**
   ```bash
   passwd
   ```
   Người dùng sẽ được yêu cầu nhập mật khẩu hiện tại, sau đó là mật khẩu mới.

2. **Thay Đổi Mật Khẩu cho Người Dùng Khác (Yêu cầu Quyền Root):**
   ```bash
   sudo passwd anotheruser
   ```
   Bạn sẽ không cần nhập mật khẩu cũ của người dùng khác, chỉ cần nhập mật khẩu mới hai lần.

3. **Khóa và Mở Khóa Tài Khoản Người Dùng:**
   ```bash
   sudo passwd -l anotheruser
   sudo passwd -u anotheruser
   ```

### Lưu Ý

- Khi thay đổi mật khẩu, đảm bảo rằng mật khẩu mới mạnh và khó đoán. Bạn nên sử dụng sự kết hợp của chữ cái, số và ký tự đặc biệt.
- Hãy cẩn thận khi sử dụng các tùy chọn khóa và xóa mật khẩu, vì chúng có thể ảnh hưởng đến khả năng truy cập của người dùng vào hệ thống.
- Lệnh `passwd` cũng cập nhật thông tin về thời gian thay đổi mật khẩu trong `/etc/shadow`, giúp hệ thống theo dõi chính sách mật khẩu hiệu quả.

5.6 

Lệnh `userdel` trong Linux được sử dụng để xóa người dùng khỏi hệ thống. Lệnh này thực hiện bằng cách xóa các mục liên quan đến người dùng từ các tệp như `/etc/passwd`, `/etc/shadow`, và các tệp khác có thông tin người dùng. Việc xóa người dùng nên được tiến hành cẩn thận để đảm bảo không ảnh hưởng đến tính toàn vẹn của hệ thống.

### Cú pháp Cơ Bản của `userdel`

```bash
userdel [options] USERNAME
```

### Các Tùy Chọn Phổ Biến của `userdel`

- **-r, --remove**: Tùy chọn này sẽ xóa không chỉ mục nhập người dùng khỏi các tệp cấu hình hệ thống, mà còn xóa thư mục home của người dùng và các file thư tín khác trên hệ thống.
  
  ```bash
  sudo userdel -r username
  ```

- **-f, --force**: Tùy chọn này buộc xóa người dùng, ngay cả khi người dùng vẫn đang đăng nhập hoặc nếu không thể cập nhật các tệp mật khẩu. Tùy chọn này nên được sử dụng cẩn thận vì nó có thể để lại một số tệp không được xóa sạch.

  ```bash
  sudo userdel -f username
  ```

- **--backup**: Tạo bản sao lưu của các tệp được xóa do xóa người dùng. Điều này hữu ích nếu bạn muốn đảm bảo có thể khôi phục dữ liệu sau khi xóa người dùng.
  
  ```bash
  sudo userdel --backup username
  ```

### Ví dụ Sử Dụng `userdel`

1. **Xóa Người Dùng Không Xóa Thư Mục Home:**
   ```bash
   sudo userdel username
   ```
   Lệnh này sẽ xóa người dùng khỏi các tệp cấu hình hệ thống nhưng để lại thư mục home và mail spool.

2. **Xóa Người Dùng và Thư Mục Home của Họ:**
   ```bash
   sudo userdel -r username
   ```
   Lệnh này sẽ xóa người dùng và tất cả các file liên quan đến người dùng trên hệ thống, bao gồm thư mục home và mail spool.

### Lưu Ý Khi Sử Dụng `userdel`

- Đảm bảo rằng không còn tiến trình nào của người dùng đang chạy trước khi xóa người dùng. Người dùng có thể có các tiến trình nền đang chạy, và việc xóa người dùng khi các tiến trình này còn tồn tại có thể dẫn đến hệ thống không ổn định.
- Nếu bạn không sử dụng tùy chọn `-r`, các file cá nhân của người dùng sẽ không bị xóa, điều này có thể chiếm dụng dung lượng đĩa và để lại dữ liệu cá nhân.
- Hãy cân nhắc tác động của việc xóa người dùng, bởi vì các file và tài liệu quan trọng có thể không còn truy cập được sau khi người dùng bị xóa.

Sử dụng `userdel` là một phần của quản lý người dùng hiệu quả và là một công cụ quan trọng trong việc duy trì an ninh và tổ chức trong môi trường hệ thống Linux.

5.7

Lệnh `groupdel` trong Linux là một công cụ được sử dụng để xóa nhóm người dùng khỏi hệ thống. Việc xóa nhóm phải được tiến hành một cách thận trọng để đảm bảo rằng không ảnh hưởng đến các người dùng hoặc quyền truy cập tệp và thư mục của hệ thống.

### Cú pháp Cơ Bản của `groupdel`

```bash
groupdel groupname
```

### Sử Dụng `groupdel`

Để xóa một nhóm, bạn chỉ cần cung cấp tên nhóm bạn muốn xóa. Ví dụ, để xóa nhóm có tên là "mygroup", bạn sẽ sử dụng lệnh sau:

```bash
sudo groupdel mygroup
```

### Lưu Ý Khi Sử Dụng `groupdel`

- **Quyền truy cập**: Bạn cần quyền quản trị (root) để xóa nhóm. Điều này đảm bảo rằng chỉ người dùng có quyền thích hợp mới có thể thay đổi cấu trúc người dùng và nhóm trên hệ thống.
- **Kiểm tra nhóm**: Trước khi xóa một nhóm, bạn nên kiểm tra xem có người dùng nào đang thuộc nhóm đó không. Nếu còn người dùng trong nhóm, bạn có thể muốn chuyển họ sang nhóm khác hoặc xóa họ khỏi nhóm trước khi xóa nhóm. Bạn có thể sử dụng lệnh `getent group groupname` để liệt kê tất cả các thành viên của nhóm.
- **Các tệp và quyền**: Xóa nhóm không tự động xóa các quyền truy cập mà nhóm đã được cấp cho các tệp và thư mục. Nếu nhóm được gán quyền truy cập đặc biệt đến tài nguyên nào đó, việc xóa nhóm có thể ảnh hưởng đến khả năng truy cập của các tài nguyên đó.

### Thực tiễn tốt nhất

Trước khi xóa nhóm, nên kiểm tra kỹ lưỡng để xác định tác động tiềm tàng đến hệ thống và dữ liệu. Đảm bảo rằng không còn tài nguyên hoặc dịch vụ nào phụ thuộc vào nhóm đó để tránh bất kỳ gián đoạn hoạt động nào. Đây là một thực tiễn tốt nhất nhằm bảo vệ dữ liệu và cấu hình hệ thống của bạn.

`groupdel` là một công cụ quan trọng trong việc quản lý nhóm và bảo mật trong Linux, giúp quản trị viên có thể dễ dàng điều chỉnh cấu trúc nhóm trên hệ thống theo nhu cầu thay đổi của tổ chức.

### **6. Using System Log Files: syslogd, rotating log files**

### **7. Running Job in the Future: `cron`, `at`**
