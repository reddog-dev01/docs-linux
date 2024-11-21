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

- **`-d, --home HOME_DIR`**: Thay đổi thư mục home của người dùng. Sử dụng tùy chọn `-m` để di chuyển nội dung của thư mục home cũ vào thư mục mới.
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

**6.1 `syslogd`**

`syslogd` là một daemon (dịch vụ nền) trong hệ điều hành Linux, chịu trách nhiệm thu thập, xử lý và lưu trữ các thông điệp nhật ký từ các phần mềm ứng dụng, hệ thống và thiết bị phần cứng. Nó là một phần của gói `syslog`, một tiện ích tiêu chuẩn trong hầu hết các hệ điều hành dựa trên UNIX và Linux, được thiết kế để giúp quản lý log trong một hệ thống phức tạp.

**Chức năng chính của `syslogd` bao gồm:***

1. **Thu Thập Thông điệp Nhật ký**: `syslogd` nhận thông điệp từ các ứng dụng, hệ thống và thiết bị. Các nguồn này gửi thông điệp đến `syslogd` thông qua giao thức `syslog`, một tiêu chuẩn công nghiệp cho giao tiếp giữa các tiến trình.

2. **Phân loại và Lọc**: `syslogd` phân loại các thông điệp nhật ký dựa trên "facility" (thể loại nguồn gửi, như `auth`, `daemon`, `kernel`, v.v.) và "severity" (mức độ nghiêm trọng của thông điệp, như `info`, `error`, `crit`, v.v.). Nó cho phép lọc và xử lý thông điệp dựa trên các tiêu chí này.

3. **Định tuyến và Lưu Trữ**: Sau khi thu thập và phân loại, `syslogd` định tuyến các thông điệp đến các đích xử lý thích hợp. Thông thường, các thông điệp này được ghi vào các tệp nhật ký trong thư mục `/var/log`. Ví dụ, thông điệp liên quan đến xác thực có thể được ghi vào `/var/log/auth.log`.

4. **Chuyển tiếp Thông điệp**: Ngoài việc lưu trữ thông điệp nhật ký trên hệ thống địa phương, `syslogd` còn có thể cấu hình để chuyển tiếp các thông điệp đến một máy chủ `syslog` trung tâm hoặc các hệ thống quản lý và giám sát nhật ký, giúp tập trung hóa quản lý nhật ký cho nhiều hệ thống.

5. **Hỗ trợ Đa nguồn**: `syslogd` có khả năng nhận và xử lý thông điệp từ nhiều nguồn khác nhau, làm cho nó trở thành một giải pháp mạnh mẽ cho việc quản lý nhật ký trong môi trường IT đa dạng và phức tạp.

- Log files được lưu trữ trong thư mục `/var/log`.
Trong hệ điều hành Ubuntu, các file log hệ thống được lưu trữ chủ yếu trong thư mục `/var/log`, giống như hầu hết các hệ thống dựa trên Linux. Dưới đây là danh sách các file log phổ biến và mục đích của chúng trong môi trường Ubuntu:

### Các File Log Chính trong Ubuntu

 1. **/var/log/syslog**
- file log chính cho hầu hết các thông báo của hệ thống, ngoại trừ các thông điệp được lọc ra để ghi vào các file log chuyên biệt khác. `syslog` chứa đa dạng các thông tin từ thông báo hệ thống cho tới cảnh báo và lỗi.

 2. **/var/log/auth.log**
- Ghi lại tất cả các hoạt động liên quan đến xác thực, bao gồm đăng nhập của người dùng, sử dụng sudo và các hoạt động xác thực khác.

 3. **/var/log/kern.log**
- Chứa thông tin chi tiết liên quan đến kernel của Linux. vấn đề về phần cứng hoặc driver.

 4. **/var/log/dpkg.log**
- Theo dõi tất cả các hoạt động liên quan đến hệ thống quản lý gói dpkg, bao gồm cài đặt và gỡ bỏ phần mềm.

 5. **/var/log/boot.log**
- Chứa thông tin về quá trình khởi động, giúp phân tích các vấn đề khởi động của máy.

 6. **/var/log/apache2/ (thư mục)**
- cài đặt và chạy máy chủ web Apache, các file log của Apache sẽ nằm ở đây, bao gồm `access.log` và `error.log`, theo dõi yêu cầu đến và các lỗi của máy chủ web.

 7. **/var/log/mysql/ (thư mục)**
- chạy máy chủ cơ sở dữ liệu MySQL, sẽ tìm thấy các file log liên quan trong thư mục này, giúp giám sát hoạt động của MySQL.

 8. **/var/log/faillog**
- Ghi lại các lần đăng nhập thất bại, có thể hữu ích để phát hiện các nỗ lực truy cập không được phép.

 9. **/var/log/ufw.log**
- Nếu sử dụng Uncomplicated Firewall (UFW), các hoạt động của tường lửa này sẽ được ghi lại ở đây.

 10. **/var/log/mail.log**
- Nếu chạy một máy chủ thư, các thông tin liên quan đến gửi và nhận thư sẽ được ghi lại trong file này.


### Quản Lý và Giám Sát File Nhật Ký

- Ubuntu sử dụng `logrotate` để quản lý các file nhật ký, tự động xoay, nén và xóa các file nhật ký cũ. Cấu hình của `logrotate` cho các file nhật ký này thường được định nghĩa trong `/etc/logrotate.conf` và `/etc/logrotate.d/`.

- Việc giám sát và phân tích nhật ký là một phần quan trọng trong việc quản lý hệ thống để đảm bảo an toàn, hiệu suất và phản ứng kịp thời đối với các sự kiện quan trọng.

Các file nhật ký này là công cụ không thể thiếu cho quản trị viên hệ thống trong việc theo dõi và duy trì sự ổn định và an toàn của hệ thống. Việc hiểu biết về nơi lưu trữ và cách xử lý các file nhật ký này sẽ giúp quản lý hệ thống một cách hiệu quả.

**6.2 `rotating log files`**

- `Rotate log` là quá trình tự động lưu trữ, nén hoặc xóa các file nhật ký cũ để ngăn chặn chúng trở nên quá lớn và chiếm dụng quá nhiều không gian đĩa. Quá trình này giúp quản lý không gian lưu trữ hiệu quả, đồng thời đảm bảo rằng các file nhật ký mới có thể tiếp tục ghi thông tin mà không bị gián đoạn hay chậm chạp do kích thước file quá lớn.

**Lý do phải rotate log**

Việc xoay (rotate) file nhật ký là một phần thiết yếu trong việc quản lý hệ thống hiệu quả, đặc biệt là trong môi trường vận hành máy chủ. Dưới đây là các lý do chính đằng sau nhu cầu xoay file nhật ký:

*1. Quản lý không gian đĩa*
- File nhật ký có thể phát triển rất nhanh, đặc biệt là trên các hệ thống có lượng truy cập cao hoặc những hệ thống mà log rất nhiều sự kiện. Nếu không được quản lý, file nhật ký có thể chiếm hết không gian đĩa, dẫn đến tình trạng hệ thống không thể ghi thêm dữ liệu mới hoặc thậm chí gây ra sự cố hệ thống. Xoay file nhật ký giúp hạn chế kích thước của chúng, đảm bảo không gian đĩa luôn được giải phóng một cách thường xuyên.

 *2. Cải thiện hiệu suất hệ thống*
- Việc xử lý và tìm kiếm trong một file nhật ký lớn có thể tốn kém về mặt hiệu suất. Các công cụ giám sát và phân tích log phải mất nhiều thời gian hơn để xử lý dữ liệu. Bằng cách xoay file nhật ký, bạn giảm kích thước của từng file, làm cho việc xử lý nhanh hơn và hiệu quả hơn.

*3. Đơn giản hóa việc bảo trì và quản lý*
- File nhật ký nhỏ hơn dễ quản lý và phân tích hơn. Xoay file nhật ký cũng giúp tổ chức thông tin theo cách có cấu trúc, làm cho việc truy xuất và phục hồi dữ liệu từ các file nhật ký lịch sử trở nên dễ dàng hơn.

*4. Đảm bảo tuân thủ và bảo mật*
- Trong nhiều ngành, việc lưu trữ nhật ký trong một khoảng thời gian xác định là yêu cầu pháp lý. Xoay file nhật ký giúp đảm bảo rằng dữ liệu nhật ký được lưu giữ và xóa đúng cách theo các tiêu chuẩn tuân thủ. Ngoài ra, việc lưu trữ các file nhật ký cũ ở dạng nén giúp bảo mật thông tin nhạy cảm khỏi bị truy cập trái phép.

*5. Phục hồi sau sự cố*
- Trong trường hợp xảy ra sự cố, việc có các file nhật ký được quản lý tốt có thể hỗ trợ đáng kể trong việc phân tích nguyên nhân và khôi phục hệ thống. File nhật ký được xoay định kỳ cung cấp bản ghi lịch sử chi tiết mà không bị quá tải bởi thông tin quá cũ hoặc không liên quan.

**6.3 Cách cấu hình rotate log cho /var/log/syslog**

Trong cấu hình `logrotate`, bạn có thể sử dụng nhiều tham số để kiểm soát cách thức xoay vòng và xử lý các file log. Dưới đây là một số tham số phổ biến và giải thích về chúng:

1. **rotate**: Định nghĩa số lượng file log cũ mà bạn muốn giữ lại. Sau khi đạt đến số này, file log cũ nhất sẽ bị xóa.
   ```
   rotate 4
   ```

2. **daily/weekly/monthly/yearly**: Xác định chu kỳ xoay vòng log.
   ```
   daily
   ```

3. **size**: Xoay vòng file log khi nó đạt đến một kích thước nhất định.
   ```
   size 100M
   ```

4. **missingok**: Nếu file log không tồn tại, logrotate sẽ không hiển thị lỗi.
   ```
   missingok
   ```

5. **notifempty**: Không xoay vòng file nếu file đó trống.
   ```
   notifempty
   ```

6. **compress**: Nén file log xoay vòng để tiết kiệm không gian đĩa.
   ```
   compress
   ```

7. **nocompress**: Không nén file log, ngay cả khi có chỉ thị nén khác.
   ```
   nocompress
   ```

8. **delaycompress**: Hoãn việc nén cho đến xoay vòng lần kế tiếp, thường được sử dụng cùng với `compress`.
   ```
   delaycompress
   ```

9. **create**: Tạo file log mới sau khi xoay vòng, với các quyền và chủ sở hữu nhất định.
   ```
   create 0644 root adm
   ```

10. **copytruncate**: Sao chép nội dung file log vào file mới và cắt ngắn file log ban đầu thay vì xóa file log cũ.
    ```
    copytruncate
    ```

11. **dateext**: Thêm ngày tháng vào tên file log xoay vòng.
    ```
    dateext
    ```

12. **olddir**: Di chuyển các file log xoay vòng vào một thư mục khác.
    ```
    olddir /var/log/old_logs
    ```

13. **include**: Đưa các file cấu hình khác vào cấu hình hiện tại.
    ```
    include /etc/logrotate.d/
    ```

14. **postrotate/endscript**: Khối lệnh thực hiện sau khi xoay vòng log. Mọi lệnh giữa `postrotate` và `endscript` sẽ được thực thi sau mỗi lần xoay vòng.
    ```
    postrotate
        /usr/lib/rsyslog/rsyslog-rotate
    endscript
    ```

15. **prerotate/preremove**: Tương tự như `postrotate`, nhưng các lệnh được thực thi trước khi xoay vòng hoặc trước khi xoá file log cuối cùng.

16. **sharedscripts**: Chạy script một lần cho tất cả các file log thay vì cho mỗi file.
    ```
    sharedscripts
    ```

Sử dụng những tham số này, bạn có thể tùy chỉnh quá trình quản lý log của mình một cách linh hoạt, phù hợp với yêu cầu cụ thể của hệ thống.

**VD**

Để cấu hình việc xoay vòng (`rotate`) cho file log `/var/log/syslog` trong hệ thống Linux, bạn thường sử dụng công cụ `logrotate`. `Logrotate` cho phép tự động xoay, nén và xóa các file log để không gian lưu trữ được quản lý hiệu quả hơn.

### Bước 1: Kiểm tra cấu hình hiện tại

Hầu hết các hệ thống Linux đã có cấu hình `logrotate` cho `/var/log/syslog` sẵn trong file `/etc/logrotate.d/rsyslog`. Bạn nên kiểm tra trước:

```bash
cat /etc/logrotate.d/rsyslog
```

Nội dung thường như sau:

```bash
/var/log/syslog
{
    rotate 7
    daily
    missingok
    notifempty
    delaycompress
    compress
    postrotate
        invoke-rc.d rsyslog rotate > /dev/null
    endscript
}
```

### Giải thích cấu hình

- `rotate 7`: Giữ 7 bản sao của file log sau khi xoay.
- `daily`: Xoay file log hàng ngày.
- `missingok`: Không báo lỗi nếu file không tồn tại.
- `notifempty`: Không xoay file nếu file đó trống.
- `delaycompress`: Hoãn nén cho đến xoay lần kế tiếp.
- `compress`: Nén file log cũ để tiết kiệm không gian.
- `postrotate` và `endscript`: Chạy lệnh trong khối này sau khi xoay log xong. Ở đây là khởi động lại dịch vụ rsyslog để nó nhận file log mới.

### Bước 2: Chỉnh sửa hoặc thêm cấu hình

Nếu bạn muốn thay đổi cách xoay vòng file log này, bạn có thể chỉnh sửa file `/etc/logrotate.d/rsyslog`:

1. **Mở file cấu hình**:
   ```bash
   sudo nano /etc/logrotate.d/rsyslog
   ```

2. **Chỉnh sửa theo nhu cầu của bạn**, ví dụ:
   - Thay đổi số lượng bản sao lưu.
   - Thay đổi chu kỳ xoay vòng từ `daily` sang `weekly` hoặc `monthly`.
   - Thêm tùy chọn `dateext` để thêm ngày tháng vào tên file sau khi xoay.

3. **Lưu và đóng file**:
   - Lưu thay đổi và thoát khỏi nano (`Ctrl+O`, `Enter`, `Ctrl+X`).

### Bước 3: Kiểm tra cấu hình

Để đảm bảo rằng cấu hình `logrotate` của bạn không có lỗi và hoạt động như mong đợi, bạn có thể chạy một test:

```bash
sudo logrotate --debug /etc/logrotate.conf
```

Lệnh này sẽ không xoay vòng log thực sự mà chỉ kiểm tra toàn bộ cấu hình và báo cáo bất kỳ lỗi nào.

Việc cấu hình xoay vòng log hiệu quả sẽ giúp quản lý không gian đĩa và giữ cho hệ thống của bạn hoạt động trơn tru. Đảm bảo rằng bạn có các bản sao lưu thích hợp để tránh mất dữ liệu quan trọng trong quá trình xoay vòng log.

### **7. Running Job in the Future: `cron`, `at`**

**7.1 `cron`**

- Dùng để lên lịch thực hiện các tác vụ tự động tại các thời điểm định kỳ. Cho phép chạy các script, lệnh, chương trình tại các khoảng thời gian cụ thể.
- Sao lưu dữ liệu định kỳ, bảo trì hệ thống, xử lý batch (sử lý log, cập nhật hệ thống), gửi thông báo và báo cáo, tự động tạo backup, tự dộng khởi động lại dịch vụ
1. Truy cập cron
```
crontab -e
```
2. Thêm lệnh
```
phút giờ ngày_tháng tháng ngày_tuần lệnh
```

VD: chạy 1 script mỗi ngày lúc 3h sáng

```
0 3 * * * /path/to/script.sh
```
3. Lưu
4. Kiểm tra
```
crontab -l
```

**7.2 `at`
1. Cài đặt `at`
```
sudo apt update
sudo apt install at
```
2. Khởi động dịch vụ
```
sudo systemctl start atd
sudo systemctl enable atd
```
3. Lên lịch

VD:
```
echo "/path/to/script.sh" | at 4pm tomorrow
```
```
at 4pm tomorrow
/path/to/script.sh
<Ctrl+D>
```
4. Kiểm tra
```
atq
```
5. Hủy 1 tác vụ
```
atrm [job number]
```

**7.3 Ví dụ job**

**1. Thiết lập 1 job chạy vào 2 giờ sáng mỗi ngày**

```
0 2 * * * /path/tp/your/script.sh
```
tắt job

```
#0 2 * * * /path/tp/your/script.sh
```
VD: tự động sao lưu 1 thư mục quan trọng /home.user/data

tạo file .sh
```
vim /home/user/scripts/backup.sh
```
thêm lệnh sau vào file
```
#!/bin/bash
tar -czf /home/user/backups/data-$(date +\%Y\%m\%d-\%H\%M).tar.gz /home/user/data
```
cấp quyền
```
chmod +x /home/user/scripts/backup.sh
```
mở crontab
```
crontab
```
thêm dòng lệnh vào 
```
0 2 * * * /home/user/scripts/backup.sh
```
kiểm tra
```
crontab
```

**2. Thiết lập 1 job chạy vào 3 giờ, 2 ngày 1 lần**

Bước 1: Tạo Script Điều Khiển

kiểm tra ngày và thực hiện công việc nếu đã đủ hai ngày kể từ lần chạy cuối.

**Tạo script (`run_every_two_days.sh`):*

```bash
#!/bin/bash

# Đường dẫn tệp lưu ngày cuối cùng chạy
STATE_FILE="/path/to/last_run_date.txt"

# Lấy ngày hiện tại theo dạng YYYYMMDD
TODAY=$(date +%Y%m%d)

# Kiểm tra nếu tệp trạng thái tồn tại
if [ -f "$STATE_FILE" ]; then
    LAST_RUN=$(cat "$STATE_FILE")
else
    LAST_RUN=0
fi

# So sánh ngày hiện tại với ngày cuối cùng chạy
DIFF=$(( (TODAY - LAST_RUN) ))

# Nếu chênh lệch 20000, tương đương khoảng 2 ngày, chạy script
if [ "$DIFF" -ge 20000 ]; then
    echo $TODAY > "$STATE_FILE"
    /path/to/your/script.sh
fi
```

Bước 2: Cấp Quyền Thực Thi Cho Script

```bash
chmod +x /path/to/run_every_two_days.sh
```

Bước 3: Thêm Script vào Crontab

```bash
0 3 * * * /path/to/run_every_two_days.sh
```

Bước 4: Kiểm tra cài đặt Cron

```bash
crontab -l
```
