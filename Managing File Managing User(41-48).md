### **1.Understanding Filesystem Hierarchy Standard**

**1.1 Cấu trúc file thư mục**
Trong hệ điều hành Linux, cấu trúc hệ thống tập tin được tổ chức theo tiêu chuẩn Filesystem Hierarchy Standard (FHS), mỗi thư mục trong hệ thống có mục đích sử dụng và nội dung rõ ràng. Dưới đây là chi tiết về mục đích và nội dung của các thư mục chính trong cấu trúc file system của Linux:

**1.2 Mục đích**
 1. `/` (Root)
- **Mục đích**: Là thư mục gốc của toàn bộ hệ thống tập tin.
- **Chứa**: Thư mục này chứa tất cả các thư mục và tập tin khác trong hệ thống, bao gồm cả thư mục của hệ điều hành và dữ liệu người dùng.

 2. `/bin` (User Binaries)
- **Mục đích**: Chứa các chương trình thiết yếu cho người dùng.
- **Chứa**: Lệnh cơ bản như `ls`, `cp`, `mv`, `cat`, `echo`.

 3. `/sbin` (System Binaries)
- **Mục đích**: Chứa các chương trình thiết yếu cho quản trị hệ thống.
- **Chứa**: Lệnh như `init`, `ip`, `reboot`.

 4. `/etc` (Configuration Files)
- **Mục đích**: Chứa các tập tin cấu hình toàn cục của hệ thống.
- **Chứa**: Tập tin cấu hình như `passwd`, `group`, `hostname`, cũng như các tập tin cấu hình cho các dịch vụ khác nhau như `httpd`, `sshd`.

 5. `/dev` (Device Files)
- **Mục đích**: Chứa các tập tin thiết bị.
- **Chứa**: Tập tin đặc biệt biểu diễn các thiết bị hệ thống như ổ đĩa cứng (`sda`), các thiết bị ký tự (`tty`), các thiết bị âm thanh (`snd`).

 6. `/proc` (Process Information)
- **Mục đích**: Chứa thông tin về hệ thống và các tiến trình đang chạy.
- **Chứa**: Thư mục ảo, không thực sự lưu trữ dữ liệu trên đĩa. Nó chứa thông tin động về hệ thống như thông tin bộ nhớ, thông tin CPU, thông tin các tiến trình đang chạy.

 7. `/var` (Variable Files)
- **Mục đích**: Chứa các tập tin thường xuyên thay đổi.
- **Chứa**: Log hệ thống (`/var/log`), gói và cơ sở dữ liệu các dịch vụ (`/var/lib`), tập tin tạm thời (`/var/tmp`).

 8. `/tmp` (Temporary Files)
- **Mục đích**: Lưu trữ tập tin tạm thời do hệ thống và người dùng tạo ra.
- **Chứa**: Tập tin tạm thời, thường được xóa khi hệ thống khởi động lại.

 9. `/usr` (User Programs)
- **Mục đích**: Chứa ứng dụng và tập tin có thể chia sẻ được.
- **Chứa**: Thư viện (`/usr/lib`), tập tin thực thi của người dùng (`/usr/bin`), tài liệu (`/usr/share/doc`), mã nguồn (`/usr/src`).

 10. `/home` (Home Directories)
- **Mục đích**: Chứa thư mục cá nhân của từng người dùng.
- **Chứa**: Dữ liệu cá nhân, cài đặt cấu hình riêng của từng người dùng.

 11. `/boot` (Boot Loader Files)
- **Mục đích**: Chứa các tập tin cần thiết cho quá trình khởi động hệ thống.
- **Chứa**: Kernel Linux, initrd, GRUB.

 12. `/lib` (System Libraries)
- **Mục đích**: Chứa thư viện cần thiết cho các tập tin thực thi trong `/bin` và `/sbin`.
- **Chứa**: Thư viện hệ thống cần thiết cho các chương trình để chạy.

 13. `/opt` (Optional add-on Applications)
- **Mục đích**: Chứa các ứng dụng thêm vào.
- **Chứa**: Phần mềm và ứng dụng của bên thứ ba.

 14. `/mnt` và `/media` (Mount Directories)
- **Mục đích**: Điểm gắn kết cho các ổ đĩa và thiết bị lưu trữ tạm thời.
- **Chứa**: `/mnt` cho gắn kết tạm thời, `/media` cho gắn kết thiết bị như USB, CD-ROM.

### **2. Managing Files and Link: `ls`, `cp`, `mv`, `rm`, `touch`, `ln`**

**2.1 `ls`**

1. **`-a`**: Hiển thị tất cả các file, bao gồm cả các file ẩn (các file bắt đầu bằng dấu `.`).
   ```bash
   ls -a
   ```

2. **`-l`**: Hiển thị chi tiết theo dạng danh sách, bao gồm thông tin về quyền truy cập, số lượng liên kết, chủ sở hữu, nhóm, kích thước, và thời gian chỉnh sửa cuối.
   ```bash
   ls -l
   ```

3. **`-h`**: Hiển thị kích thước file theo dạng dễ đọc (KB, MB, GB), thường sử dụng cùng với `-l`.
   ```bash
   ls -lh
   ```

4. **`-R`**: Liệt kê tất cả các file trong thư mục hiện tại và các thư mục con (đệ quy).
   ```bash
   ls -R
   ```

5. **`-d`**: Chỉ hiển thị thư mục, không liệt kê nội dung bên trong.
   ```bash
   ls -d */
   ```

6. **`-t`**: Sắp xếp file theo thời gian chỉnh sửa cuối, từ mới nhất đến cũ nhất.
   ```bash
   ls -lt
   ```

7. **`-r`**: Sắp xếp theo thứ tự ngược lại, ví dụ: từ Z đến A hoặc từ mới nhất đến cũ nhất khi kết hợp với `-t`.
   ```bash
   ls -lr
   ```

8. **`-S`**: Sắp xếp file theo kích thước, từ lớn nhất đến nhỏ nhất.
   ```bash
   ls -lS
   ```

9. **`--color`**: Hiển thị màu sắc để phân biệt loại file và thư mục.
   ```bash
   ls --color=auto
   ```

10. **`-i`**: Hiển thị số inode của mỗi file.
    ```bash
    ls -i
    ```

11. **`-1`**: Hiển thị mỗi file trên một dòng.
    ```bash
    ls -1
    ```

12. **`-X`**: Sắp xếp theo phần mở rộng của file.
    ```bash
    ls -lX
    ```

13. **`-F`**: Thêm ký tự xác định loại file, ví dụ: `/` cho thư mục, `*` cho file thực thi.
    ```bash
    ls -F
    ```    

**2.2 `cp`**

1. **`-r`**: Sao chép thư mục đệ quy (recursively), bao gồm cả các thư mục con. Bắt buộc dùng khi sao chép thư mục.
   ```bash
   cp -r source_directory destination_directory
   ```

2. **`-i`**: Chế độ tương tác (interactive), yêu cầu xác nhận nếu file đích đã tồn tại.
   ```bash
   cp -i source_file destination_file
   ```

3. **`-f`**: Ghi đè file đích mà không cần yêu cầu xác nhận (force).
   ```bash
   cp -f source_file destination_file
   ```

4. **`-u`**: Chỉ sao chép nếu file nguồn mới hơn file đích hoặc nếu file đích chưa tồn tại (update).
   ```bash
   cp -u source_file destination_file
   ```

5. **`-v`**: Hiển thị chi tiết quá trình sao chép (verbose).
   ```bash
   cp -v source_file destination_file
   ```

6. **`-p`**: Bảo toàn các thuộc tính của file, như quyền truy cập, thời gian chỉnh sửa, và chủ sở hữu (preserve attributes).
   ```bash
   cp -p source_file destination_file
   ```

7. **`-a`**: Chế độ lưu trữ (archive), sao chép tất cả các thuộc tính và thư mục con. Tương đương với `-dR --preserve=all`.
   ```bash
   cp -a source_directory destination_directory
   ```

8. **`-l`**: Tạo liên kết cứng (hard link) thay vì sao chép nội dung.
   ```bash
   cp -l source_file destination_file
   ```

9. **`-s`**: Tạo liên kết mềm (symbolic link) thay vì sao chép nội dung.
   ```bash
   cp -s source_file destination_file
   ```

10. **`--backup`**: Tạo bản sao lưu file đích nếu file đã tồn tại. Sử dụng cùng với `-b` để tạo bản sao lưu tự động.
    ```bash
    cp --backup source_file destination_file
    ```

11. **`--parents`**: Giữ lại cấu trúc thư mục của file nguồn khi sao chép vào thư mục đích.
    ```bash
    cp --parents source_directory/file destination_directory
    ```

12. **`--remove-destination`**: Xóa file đích trước khi sao chép (hữu ích khi file đích có quyền chỉ đọc).
    ```bash
    cp --remove-destination source_file destination_file
    ```

13. **`--sparse=WHEN`**: Kiểm soát cách sao chép file thưa (sparse file) để tiết kiệm dung lượng. `WHEN` có thể là `auto`, `always`, hoặc `never`.
    ```bash
    cp --sparse=always source_file destination_file
    ```

14. **`-n`**: Không sao chép nếu file đích đã tồn tại (no-clobber).
    ```bash
    cp -n source_file destination_file
    ```

**2.3 `mv`**

1. `-i`: Hỏi trước khi ghi đè file đích
2. `-f`: Ghi đè file đích mà không cần hỏi
3. `-v`: Hiển thị thông tin chi tiết về file được di chuyển
4. `-u`: CHỉ di chuyển khi file nguồn mới hơn hoặc file đích không tồn tại

**2.4 `rm`**

1. `-f`: xóa các file mà không cần xác nhận
2. `-i`: Hỏi xác nhận trước khi xóa
3. `-r`: Xóa thư mục và toàn bộ nội dung bên trong (gồm cả file con và thư mục con)
4. `-v`: Hiện chi tiết quá trình xóa

**2.5 `touch`**
- Tạo 1 file nếu chưa tồn tại hoặc cập nhật ngày/giờ cho file nếu nó đã tồn tại

1. `-a` Chỉ thay đổi thời gian truy cập của file `touch -a file_name`
2. `-m` Chỉ thay đổi thời gian sửa đổi của file `touch -m file_name`
3. `-c` Không tạo file mới nếu file không tồn tại. Chỉ đổi thời gian nếu file đã tồn tại `touch -c file_name`
4. `-d` Sử dụng chuỗi thời gian cụ thể áp dụng cho file. VD: `touch -d "DATE_STRING" file_name #YYYY-MM-DD HH:MM:SS or DD/MM/YYYY HH:MM:SS`
5. `-r` Sao chép thời gian truy cập, sửa đổi từ file chiếu sang file đích mà không thay đổi nội dung. `touch -r reference_file target_file`
6. `-t` Cho phép chỉnh sửa thời gian truy cập và thời gian sửa đổi. `touch -t YYYYMMDDhhmm.ss file_name`

**2.6 `ln`**
- Sử dụng để tạo các liên kết cứng (hard link) và liên kết mềm (soft link or symbolic link)
```
ln [OPTION] TARGET [LINK_NAME]
```
Lệnh `ln` trong Linux được sử dụng để tạo liên kết (link) giữa các tệp hoặc thư mục. Mục địch liên kết để tiết kiệm dung lượng, tạo đường dẫn ngắn gọn, chia sẻ và quản lý phân quyền.

Có hai loại liên kết chính:

1. **Liên kết cứng (Hard Link)**: Đây là một liên kết trực tiếp đến nội dung của tệp gốc. Cả tệp gốc và liên kết cứng đều trỏ đến cùng một dữ liệu trong ổ đĩa, vì vậy nếu bạn xóa một trong hai, dữ liệu vẫn còn (cho đến khi tất cả các liên kết bị xóa).

   ```bash
   ln source_file link_name
   ```

2. **Liên kết mềm (Soft Link hoặc Symbolic Link)**: Đây là một liên kết gián tiếp, chỉ trỏ đến vị trí của tệp gốc. Nếu tệp gốc bị xóa, liên kết mềm sẽ không hoạt động (dẫn đến lỗi "file not found").

   ```bash
   ln -s source_file link_name
   ```

 Ví dụ:

- Tạo một liên kết cứng cho `file.txt`:
  ```bash
  ln file.txt file_hardlink.txt
  ```

- Tạo một liên kết mềm cho `file.txt`:
  ```bash
  ln -s file.txt file_softlink.txt
  ```

**Các tùy chọn phổ biến**:

- `-f`: Ghi đè liên kết nếu nó đã tồn tại.
- `-i`: Hỏi xác nhận trước khi ghi đè.
- `-v`: Hiển thị thông tin chi tiết về quá trình tạo liên kết.
- `-b` và `-S` (Tạo bản sao lưu liên kết nếu tồn tại - backup và suffix):

Khi dùng -b, ln sẽ tạo bản sao lưu liên kết đích nếu liên kết đó đã tồn tại. Kết hợp với -S để thêm hậu tố cho bản sao lưu.
```
ln -sb -S .backup source_file link_name
```
Ví dụ:
```
ln -sb -S .old /path/to/original /path/to/existing_link
```

### **2. Managing File Ownership: `chown`, `chgrp`**

**2.1 `chown`**
Lệnh `chown` trong Linux được sử dụng để thay đổi chủ sở hữu và/hoặc nhóm của một hoặc nhiều file hoặc thư mục. Dưới đây là hướng dẫn chi tiết về cách sử dụng lệnh `chown`, bao gồm cú pháp cơ bản và một số ví dụ.

### Cú pháp Cơ Bản
```bash
chown [options] [user][:group] file...
```

Trong đó:
- **user**: Tên người dùng mới mà bạn muốn gán làm chủ sở hữu cho file.
- **group**: Tên nhóm mới mà bạn muốn gán cho file. Việc chỉ định nhóm là tùy chọn và nếu bạn muốn chỉ định nhóm mà không thay đổi chủ sở hữu, bạn có thể bỏ qua phần user.
- **file**: Đường dẫn đến file hoặc thư mục mà bạn muốn thay đổi. Bạn có thể liệt kê nhiều file hoặc thư mục cách nhau bằng khoảng trắng.

### Các Tùy Chọn Phổ Biến
- `-c`, `--changes`: Hiển thị thông tin về các thay đổi đã được thực hiện.
- `-v`, `--verbose`: Hiển thị thông tin chi tiết về quá trình thực hiện lệnh.
- `-f`, `--silent`, `--quiet`: Không hiển thị các thông báo lỗi.
- `-R`, `--recursive`: Áp dụng lệnh cho tất cả file và thư mục con một cách đệ quy.

### Ví dụ

1. **Thay Đổi Chủ Sở Hữu của File**
   ```bash
   sudo chown newuser filename.txt
   ```
   Lệnh này sẽ thay đổi chủ sở hữu của `filename.txt` thành `newuser`.

2. **Thay Đổi Chủ Sở Hữu và Nhóm**
   ```bash
   sudo chown newuser:newgroup filename.txt
   ```
   Lệnh này sẽ thay đổi chủ sở hữu của `filename.txt` thành `newuser` và nhóm thành `newgroup`.

3. **Thay Đổi Chủ Sở Hữu của Thư Mục và Nội Dung Bên Trong**
   ```bash
   sudo chown -R newuser:newgroup /path/to/directory
   ```
   Lệnh này sẽ thay đổi chủ sở hữu và nhóm của thư mục `/path/to/directory` và tất cả nội dung bên trong một cách đệ quy.

4. **Chỉ Thay Đổi Nhóm**
   ```bash
   sudo chown :newgroup filename.txt
   ```
   Lệnh này sẽ thay đổi nhóm của `filename.txt` thành `newgroup` mà không thay đổi chủ sở hữu hiện tại.

5. **Sử Dụng Verbose để Kiểm Tra Thay Đổi**
   ```bash
   sudo chown -v newuser:newgroup filename.txt
   ```
   Lệnh này sẽ thay đổi chủ sở hữu và nhóm của `filename.txt` và hiển thị thông tin chi tiết về thay đổi.

### Lưu Ý
- Bạn cần quyền quản trị để thay đổi chủ sở hữu của file hoặc thư mục. Vì vậy, lệnh `chown` thường được sử dụng với `sudo` để tăng quyền truy cập.
- Hãy cẩn thận khi sử dụng tùy chọn `-R` vì nó có thể gây ra thay đổi sở hữu trên một lượng lớn file và thư mục, có thể ảnh hưởng đến hệ thống của bạn.

**2.2 chgrp**

Lệnh `chgrp` trong Linux dùng để thay đổi nhóm của một hoặc nhiều file hoặc thư mục. Đây là công cụ giúp bạn quản lý nhóm sở hữu các file, cho phép bạn thiết lập nhóm quản lý nội dung cụ thể trong hệ thống tệp của bạn.

### Cú pháp Cơ Bản của chgrp

```bash
chgrp [OPTIONS] GROUP FILE...
```

Trong đó:
- **GROUP**: Tên của nhóm mà bạn muốn gán cho file.
- **FILE...**: Một hoặc nhiều file mà bạn muốn thay đổi nhóm. Bạn có thể liệt kê nhiều file cách nhau bởi khoảng trống.

### Các Tùy Chọn Phổ Biến
- `-c`, `--changes`: Chỉ hiển thị thông báo khi thực hiện thay đổi.
- `-f`, `--silent`, `--quiet`: Không hiển thị lỗi cho các file không thể thay đổi.
- `-v`, `--verbose`: Hiển thị thông báo chi tiết cho mỗi file xử lý.
- `-R`, `--recursive`: Áp dụng thay đổi cho tất cả các file và thư mục con một cách đệ quy.

### Ví dụ Sử Dụng chgrp

1. **Thay Đổi Nhóm của Một File**
   ```bash
   chgrp groupname filename.txt
   ```
   Thay đổi nhóm của file `filename.txt` thành `groupname`.

2. **Thay Đổi Nhóm Của Nhiều File**
   ```bash
   chgrp groupname file1.txt file2.txt file3.txt
   ```
   Thay đổi nhóm của nhiều file cùng một lúc.

3. **Thay Đổi Nhóm Của Thư Mục và Nội Dung Bên Trong**
   ```bash
   chgrp -R groupname /path/to/directory
   ```
   Thay đổi nhóm của thư mục `/path/to/directory` và tất cả các file và thư mục con bên trong nó một cách đệ quy.

4. **Sử Dụng Verbose để Kiểm Tra Thay Đổi**
   ```bash
   chgrp -v groupname filename.txt
   ```
   Hiển thị thông tin chi tiết khi thay đổi nhóm của `filename.txt`.

### Lưu Ý Khi Sử Dụng chgrp
- Bạn cần có quyền hạn đối với file để thay đổi nhóm của nó, hoặc bạn phải là người dùng root hoặc có quyền sudo.
- Sử dụng tùy chọn `-R` cẩn thận, nhất là khi áp dụng trên các thư mục lớn hoặc thư mục gốc, vì điều này có thể ảnh hưởng đến hoạt động của hệ thống.
- Nếu không chắc chắn về quyền của mình, bạn có thể dùng lệnh `ls -l` để kiểm tra nhóm hiện tại của các file trước khi sử dụng `chgrp`.

Sử dụng `chgrp` cùng với các công cụ như `chmod` và `chown` giúp bạn kiểm soát hiệu quả quyền truy cập và quản lý các file và thư mục trong hệ thống Linux của mình.
