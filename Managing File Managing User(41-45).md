### **1.Understanding Filesystem Hierarchy Standard**

**1.1 Cấu trúc file thư mục**
Trong hệ điều hành Linux, cấu trúc hệ thống file được tổ chức theo tiêu chuẩn Filesystem Hierarchy Standard (FHS), mỗi thư mục trong hệ thống có mục đích sử dụng và nội dung rõ ràng. Dưới đây là chi tiết về mục đích và nội dung của các thư mục chính trong cấu trúc file system của Linux:

**1.2 Mục đích**
 1. `/` (Root)
- **Mục đích**: Là thư mục gốc của toàn bộ file system.
- **Chứa**: Thư mục này chứa tất cả các thư mục và file khác trong server, bao gồm cả thư mục của hệ điều hành và dữ liệu người dùng.

 2. `/bin` (User Binaries)
- **Mục đích**: Chứa các chương trình thiết yếu cho người dùng.
- **Chứa**: Lệnh cơ bản như `ls`, `cp`, `mv`, `cat`, `echo`.

 3. `/sbin` (System Binaries)
- **Mục đích**: Chứa các chương trình thiết yếu cho quản trị hệ thống.
- **Chứa**: Lệnh như `init`, `ip`, `reboot`.

 4. `/etc` (Configuration Files)  
- **Mục đích**: Chứa các file cấu hình của hệ thống.
- **Chứa**: file cấu hình như `passwd`, `group`, `hostname`, cũng như các file cấu hình cho các dịch vụ khác nhau như `httpd`, `sshd`.

 5. `/dev` (Device Files)
- **Mục đích**: Chứa các file thiết bị.
- **Chứa**: file đặc biệt biểu diễn các thiết bị hệ thống như ổ đĩa cứng (`sda`), các thiết bị ký tự (`tty`), các thiết bị âm thanh (`snd`).

 6. `/proc` (Process Information)
- **Mục đích**: Chứa thông tin về hệ thống và các tiến trình đang chạy.
- **Chứa**: Thư mục ảo, không thực sự lưu trữ dữ liệu trên đĩa. Nó chứa thông tin động về hệ thống như thông tin bộ nhớ, thông tin CPU, thông tin các tiến trình đang chạy.

 7. `/var` (Variable Files)
- **Mục đích**: Chứa các file thường xuyên thay đổi.
- **Chứa**: Log hệ thống (`/var/log`), gói và cơ sở dữ liệu các dịch vụ (`/var/lib`), file tạm thời (`/var/tmp`).

 8. `/tmp` (Temporary Files)
- **Mục đích**: Lưu trữ file tạm thời do hệ thống và người dùng tạo ra.
- **Chứa**: file tạm thời, thường được xóa khi hệ thống khởi động lại.

 9. `/usr` (User Programs)
- **Mục đích**: Chứa ứng dụng và file có thể chia sẻ được.
- **Chứa**: Thư viện (`/usr/lib`), file thực thi của người dùng (`/usr/bin`), tài liệu (`/usr/share/doc`), mã nguồn (`/usr/src`).

 10. `/home` (Home Directories)
- **Mục đích**: Chứa thư mục cá nhân của từng người dùng.
- **Chứa**: Dữ liệu cá nhân, cài đặt cấu hình riêng của từng người dùng.

 11. `/boot` (Boot Loader Files)
- **Mục đích**: Chứa các file cần thiết cho quá trình khởi động hệ thống. Cần thiết trong quá trình khởi động vì thiếu kernel, initramfs và các file cấu hình bootloader. Nhưng trong 1 số cài đặt hệ thống có thể tích hợp vào `/` thay vì phân vùng riêng.
- **Chứa**: Kernel Linux, initramfs/initrd, GRUB.

 12. `/lib` (System Libraries)
- **Mục đích**: Chứa thư viện cần thiết cho các file thực thi trong `/bin` và `/sbin`.
- **Chứa**: Thư viện hệ thống cần thiết cho các chương trình để chạy.

 13. `/opt` (Optional add-on Applications)
- **Mục đích**: Chứa các ứng dụng thêm vào.
- **Chứa**: Phần mềm và ứng dụng của bên thứ ba.

 14. `/mnt` và `/media` (Mount Directories)
- **Mục đích**: Điểm gắn kết cho các ổ đĩa và thiết bị lưu trữ tạm thời.
- **Chứa**: `/mnt` cho gắn kết tạm thời, `/media` cho gắn kết thiết bị như USB, CD-ROM.

15. `/srv`
- Chứa dữ liệu và tài nguyên được cung cấp bởi các dịch vụ (web, FTP, NFS, v.v.).

16. `/run`
- sử dụng để lưu trữ dữ liệu runtime của hệ thống hoặc các ứng dụng đang chạy
- chứa các tệp mà hệ thống hoặc các ứng dụng cần truy cập trong suốt thời gian chạy

17. `/lib64`
- chứa các thư viện được biên dịch dành riêng cho các ứng dụng 64-bit.

18. `sys`
- Cung cấp thông tin về phần cứng: cho phép người dùng và các chương trình truy cập thông tin chi tiết về thiết bị phần cứng như CPU, bộ nhớ, thiết bị lưu trữ, card mạng, v.v.

19. ` lost+found`
- được tạo tự động trên mỗi phân vùng sử dụng ext. được sử dụng để lưu trữ các file hoặc khối dữ liệu bị "mất" hoặc bị lỗi trong hệ thống tệp, thường xảy ra sau các sự cố như mất điện, hỏng ổ đĩa, hoặc tắt máy đột ngột.


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


9. **`-i`**: Hiển thị số inode của mỗi file.
    ```bash
    ls -i
    ```

10. **`-1`**: Hiển thị mỗi file trên một dòng.
    ```bash
    ls -1
    ```

11. **`-X`**: Sắp xếp theo phần mở rộng của file.
    ```bash
    ls -lX
    ```

12. **`-F`**: Thêm ký tự xác định loại file, ví dụ: `/` cho thư mục, `*` cho file thực thi.
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
**Xoá liên kết**: `unlink`

### **2. Managing File Ownership: `chown`, `chgrp`**

**2.1 `chown`**

Lệnh `chown` trong Linux được sử dụng để thay đổi chủ sở hữu và/hoặc nhóm của một hoặc nhiều file hoặc thư mục.

Cú pháp Cơ Bản
```
chown [options] [user][:group] file...
```

Trong đó:
- **user**: Tên người dùng mới muốn gán làm chủ sở hữu cho file.
- **group**: Tên nhóm mới muốn gán cho file.
- **file**: Đường dẫn đến file hoặc thư mục muốn thay đổi, có thể liệt kê nhiều file hoặc thư mục cách nhau bằng khoảng trắng.

**Các Tùy Chọn Phổ Biến**

- `-c`, `--changes`: Hiển thị thông tin về các thay đổi đã được thực hiện.
- `-v`, `--verbose`: Hiển thị thông tin chi tiết về quá trình thực hiện lệnh.
- `-f`, `--silent`, `--quiet`: Không hiển thị các thông báo lỗi.
- `-R`, `--recursive`: Áp dụng lệnh cho tất cả file và thư mục con một cách đệ quy.

**Ví dụ**

1. **Thay Đổi Chủ Sở Hữu của File**
   ```bash
   sudo chown newuser filename.txt
   ```

2. **Thay Đổi Chủ Sở Hữu và Nhóm**
   ```bash
   sudo chown newuser:newgroup filename.txt
   ```

3. **Thay Đổi Chủ Sở Hữu của Thư Mục và Những gì Bên Trong**

   Không chỉ thay đổi thư mục mà thay đổi cả file và thư mục con

   ```bash
   sudo chown -R newuser:newgroup /path/to/directory
   ```

5. **Chỉ Thay Đổi Nhóm**
   ```bash
   sudo chown :newgroup filename.txt
   ```
   Lệnh này sẽ thay đổi nhóm của `filename.txt` thành `newgroup` mà không thay đổi chủ sở hữu hiện tại.

6. **Sử Dụng Verbose để Kiểm Tra Thay Đổi**
   ```bash
   sudo chown -v newuser:newgroup filename.txt
   ```
   Lệnh này sẽ thay đổi chủ sở hữu và nhóm của `filename.txt` và hiển thị thông tin chi tiết về thay đổi.

**2.2 chgrp**

Lệnh `chgrp` trong Linux dùng để thay đổi nhóm của một hoặc nhiều file hoặc thư mục.

 Cú pháp Cơ Bản của chgrp

```bash
chgrp [OPTIONS] GROUP FILE...
```

Trong đó:
- **GROUP**: Tên của nhóm muốn gán cho file.
- **FILE...**: Một hoặc nhiều file muốn thay đổi nhóm, có thể liệt kê nhiều file cách nhau bởi khoảng trống.

**Các Tùy Chọn Phổ Biến**
- `-c`, `--changes`: Chỉ hiển thị thông báo khi thực hiện thay đổi.
- `-f`, `--silent`, `--quiet`: Không hiển thị lỗi cho các file không thể thay đổi.
- `-v`, `--verbose`: Hiển thị thông báo chi tiết cho mỗi file xử lý.
- `-R`, `--recursive`: Áp dụng thay đổi cho tất cả các file và thư mục con một cách đệ quy.

**Ví dụ Sử Dụng chgrp**

1. **Thay Đổi Nhóm của Một File**
   ```bash
   chgrp groupname filename.txt
   ```

2. **Thay Đổi Nhóm Của Nhiều File**
   ```bash
   chgrp groupname file1.txt file2.txt file3.txt
   ```

3. **Thay Đổi Nhóm Của Thư Mục và Những Gì Bên Trong**
   ```bash
   chgrp -R groupname /path/to/directory
   ```
   Thay đổi nhóm của thư mục `/path/to/directory` và tất cả các file và thư mục con bên trong nó một cách đệ quy.

4. **Sử Dụng Verbose để Kiểm Tra Thay Đổi**
   ```bash
   chgrp -v groupname filename.txt
   ```
   
### **3. Controlling Access to Files: Understanding Permissions, `chmod`**

Cú pháp Cơ Bản của chmod

```bash
chmod [options] mode file...
```

Trong đó:
- **options**: Các tùy chọn thêm để điều chỉnh cách thức thực thi lệnh.
- **mode**: Cách thức thay đổi quyền truy cập, được chỉ định bằng số hoặc bằng chữ.
- **file**: Đường dẫn đến file hoặc thư mục mà thay đổi.

**Quyền truy cập:**
- **r (read)**: Quyền đọc file.
- **w (write)**: Quyền ghi hoặc sửa file.
- **x (execute)**: Quyền thực thi file.

Quyền này có thể được áp dụng cho ba nhóm:
- **u (user)**: Chủ sở hữu file.
- **g (group)**: Nhóm của file.
- **o (others)**: Người dùng khác.

**Quyền sử dụng Số:**
Bạn có thể sử dụng các số từ 0 đến 7 để thiết lập quyền truy cập.
- **4** đại diện cho `r`
- **2** đại diện cho `w`
- **1** đại diện cho `x`
- Các số được cộng lại để kết hợp quyền, ví dụ, `6` (4+2) đại diện cho đọc và viết (rw-).

**Ví dụ:**
1. **Cho phép chủ sở hữu đọc và ghi file, nhóm đọc file, và người khác không có quyền gì:**
   ```bash
   chmod 640 filename
   ```

2. **Cho phép mọi người đọc, viết, và thực thi một file:**
   ```bash
   chmod 777 filename
   ```

3. **Sử dụng Ký tự để Thay Đổi Quyền:**
   - Thêm quyền thực thi cho chủ sở hữu:
     ```bash
     chmod u+x filename
     ```
   - Xóa quyền ghi cho nhóm:
     ```bash
     chmod g-w filename
     ```
   - Đặt quyền đọc và ghi cho người dùng và nhóm, không cho người khác:
     ```bash
     chmod ug+rw,o-rwx filename
     ```

**Tùy chọn Phổ Biến:**
- **`-R`**: Áp dụng thay đổi một cách đệ quy cho tất cả file và thư mục con.
- **`-v`**: Hiển thị mô tả chi tiết về những thay đổi đối với các file.
- **`-c`**: Tương tự như `-v` nhưng chỉ báo cáo khi thực sự có thay đổi quyền.

### **4. Tools for Locating Files: `find`, `locate`, `whereis`, `which`**

**4.1 `find`**

Lệnh `find` trong Linux là một công cụ mạnh mẽ để tìm kiếm các file và thư mục dựa trên các tiêu chí nhất định như tên file, loại file, ngày sửa đổi, kích thước, và nhiều tiêu chí khác.

Cú pháp Cơ Bản của `find`
```bash
find [where to start searching from] [options] [what to find] [action]
```

**Ví Dụ Cơ Bản**
1. *Tìm Tất Cả Các File Trong Thư Mục Hiện Tại và Các Thư Mục Con:*
   ```bash
   find .
   ```
   Dấu chấm (`.`) nghĩa là bắt đầu tìm kiếm từ thư mục hiện tại.

2. *Tìm Tất Cả Các File Với Tên Cụ Thể:*
   ```bash
   find /path/to/directory -name "filename.txt"
   ```
   Thay thế `/path/to/directory` với đường dẫn thực tế và `"filename.txt"` với tên file cần tìm.

3. *Tìm và Xóa Các File Với Tên Nhất Định:*
   ```bash
   find /path/to/directory -type f -name "*.tmp" -delete
   ```
   Lệnh này tìm tất cả các file có phần mở rộng `.tmp` và xóa chúng.

**Các Option và Argument Phổ Biến**
- **`-name 'pattern'`**: Tìm file theo mẫu, sử dụng các ký tự đại diện như `*`.
- **`-iname 'pattern'`**: Giống như `-name` nhưng không phân biệt chữ hoa chữ thường.
- **`-type [f/d/l]`**: Chỉ định loại file để tìm. `f` cho file, `d` cho thư mục, `l` cho liên kết tượng trưng.
- **`-size [+-]size`**: Tìm file theo kích thước. Ví dụ, `-size +2M` tìm các file lớn hơn 2 megabytes.
- **`-mtime -n`**: Tìm các file đã được sửa đổi trong `n` ngày trước.
- **`-user 'username'`**: Tìm tất cả các file thuộc về người dùng `username`.
- **`-exec cmd {} \;`**: Thực hiện lệnh `cmd` 1 lần cho mỗi file tìm thấy. `{}` là nơi tên file được chèn vào.
- **`-exec cmd {} +`**: Thực hiện lệnh `cmd` trên 1 lần trên tất cả các file tìm thấy. `{}` là nơi tên file được chèn vào.

**Ví Dụ Nâng Cao**

1. *Tìm File Được Sửa Đổi Trong 7 Ngày Qua và Sắp Xếp Chúng:*
   ```bash
   find /path/to/directory -mtime -7 -exec ls -lt {} +
   ```
   Lệnh này tìm các file đã sửa trong 7 ngày qua và sắp xếp chúng theo thời gian sửa đổi.

2. *Tìm Thư Mục Trống và Xóa Chúng:*
   ```bash
   find /path/to/directory -type d -empty -delete
   ```
   Lệnh này tìm các thư mục rỗng và xóa chúng.

**Lưu Ý Khi Sử Dụng `find`**
- Hãy cẩn thận khi sử dụng lệnh `-delete` vì nó xóa file mà không hỏi lại.
- Luôn kiểm tra lệnh `find` của bạn với `-print` hoặc `-ls` trước khi chạy các hành động có thể không thể hoàn tác như `-delete`.

**4.2 `locate`**

Lệnh `locate` trong Linux là một công cụ tìm kiếm cực kỳ nhanh, được sử dụng để tìm vị trí của các file trong cơ sở dữ liệu file hệ thống. Cơ sở dữ liệu này được cập nhật thường xuyên bởi dịch vụ `updatedb`. So với `find`, `locate` có thể trả về kết quả tìm kiếm nhanh hơn rất nhiều vì nó không quét qua hệ thống file mà chỉ tìm kiếm trong cơ sở dữ liệu đã được lập chỉ mục.

Cách Sử Dụng Cơ Bản

```bash
locate [options] pattern
```

```bash
locate filename.txt
```

**Các Tùy Chọn Phổ Biến**

- **`-i`**: Không phân biệt chữ hoa chữ thường trong khi tìm kiếm.
  ```bash
  locate -i Filename.txt
  ```
  Tìm kiếm không phân biệt chữ hoa chữ thường, sẽ trả về kết quả cho `filename.txt`, `Filename.txt`, `FILENAME.TXT`, v.v.

- **`--regex`**: Cho phép mẫu là một biểu thức chính quy.
  ```bash
  locate --regex 'filename[0-9].txt'
  ```
  Tìm kiếm các file có tên phù hợp với biểu thức chính quy, chẳng hạn như `filename1.txt`, `filename2.txt`, v.v.

- **`-n, --limit`**: Giới hạn số lượng kết quả trả về.
  ```bash
  locate -n 10 filename.txt
  ```
  Giới hạn chỉ trả về 10 kết quả đầu tiên.

- **`-b, --basename`**: Chỉ tìm kiếm với phần tên cơ bản của file (không bao gồm đường dẫn).
  ```bash
  locate -b '\filename.txt'
  ```
  Chỉ trả về các file mà tên đúng là `filename.txt`, không bao gồm các file có đường dẫn như `/path/to/filename.txt`.

**Cập Nhật Cơ Sở Dữ liệu**

- Cơ sở dữ liệu của `locate` cần được cập nhật thường xuyên để phản ánh các thay đổi trong hệ thống file. Điều này thường được thực hiện tự động thông qua dịch vụ `updatedb` hoặc có thể được thực hiện thủ công bằng lệnh:
  ```bash
  sudo updatedb
  ```
  Lệnh này cần quyền quản trị để chạy và sẽ cập nhật cơ sở dữ liệu, đảm bảo rằng các kết quả từ `locate` là cập nhật.

**Lưu Ý**

- `locate` có thể không trả về các file mới được tạo nếu `updatedb` chưa chạy sau khi file đó được tạo.
- Dù nhanh, nhưng `locate` có thể trả về các kết quả đã không còn tồn tại trên hệ thống nếu file đã được xóa mà `updatedb` chưa cập nhật.
- Vì lý do bảo mật, một số hệ thống có thể hạn chế quyền truy cập vào cơ sở dữ liệu `locate` để chỉ root mới có thể xem được tất cả các kết quả.


**4.3 `whereis`**

Lệnh `whereis` trong Linux được sử dụng để tìm vị trí của file thực thi, mã nguồn, và trang man của các chương trình.

Cú pháp Cơ Bản của `whereis`

```bash
whereis [options] program_name
```

**Tùy Chọn Phổ Biến**

- **`-b`**: Chỉ tìm các file thực thi.
- **`-m`**: Chỉ tìm các file trang man.
- **`-s`**: Chỉ tìm các file mã nguồn.
- **`-u`**: Tìm các file không rõ mục đích. Điều này sẽ loại bỏ các file thực thi, trang man, và mã nguồn, giúp bạn tìm các file không rõ mục đích.

Ví dụ Sử Dụng `whereis`

1. *Tìm Đường Dẫn Của Lệnh `ls`*
   ```bash
   whereis ls
   ```
   Lệnh này sẽ trả về đường dẫn của file thực thi `ls`, cũng như đường dẫn của trang man và mã nguồn nếu có.

2. *Tìm Đường Dẫn Của File Thực Thi `grep`*
   ```bash
   whereis -b grep
   ```
   Lệnh này chỉ trả về đường dẫn của file thực thi `grep`, loại trừ trang man và mã nguồn.

3. *Tìm Trang Man Của `chmod`*
   ```bash
   whereis -m chmod
   ```
   Lệnh này chỉ trả về đường dẫn của trang man cho `chmod`.

4. *Tìm Mã Nguồn Của `gcc`*
   ```bash
   whereis -s gcc
   ```
   Lệnh này chỉ trả về đường dẫn của mã nguồn `gcc`.

**Lưu Ý Khi Sử Dụng `whereis`**

- `whereis` sử dụng một cơ sở dữ liệu đã được lập chỉ mục trước để tìm nhanh các file. Do đó, nó có thể không luôn cập nhật với những thay đổi mới nhất trong hệ thống file.
- `whereis` thường chỉ tìm các file liên quan đến chương trình, không phải các file dữ liệu hoặc các loại file khác.

**4.4 `which`**

Lệnh `which` trong Linux được sử dụng để xác định đường dẫn của các lệnh thực thi mà shell có thể gọi, tìm kiếm trong các thư mục được liệt kê trong biến môi trường `PATH` và trả về đường dẫn đầu tiên tìm thấy. 

Cú pháp Cơ Bản của `which`

```bash
which [options] command_name
```

**Tùy Chọn Phổ Biến**

- **`-a`**: Liệt kê tất cả các vị trí chứa lệnh được chỉ định trong `PATH`, không chỉ đường dẫn đầu tiên tìm thấy.
- **`--skip-dot`**: Bỏ qua các thư mục có dấu chấm (.) trước trong `PATH` khi tìm kiếm.
- **`--skip-alias`**: Bỏ qua các bí danh được định nghĩa trong shell.

Ví dụ Sử Dụng `which`

1. *Xác Định Đường Dẫn của Lệnh `ls`*
   ```bash
   which ls
   ```
   Lệnh này sẽ trả về đường dẫn của lệnh `ls` mà shell sử dụng, chẳng hạn `/bin/ls`.

2. *Tìm Tất Cả Các Đường Dẫn Của Lệnh `python`*
   ```bash
   which -a python
   ```
   Lệnh này liệt kê tất cả các đường dẫn mà `python` có thể được gọi trong biến môi trường `PATH`.

3. *Kiểm Tra Lệnh `gcc` và Bỏ Qua Các Bí Danh*
   ```bash
   which --skip-alias gcc
   ```
   Lệnh này sẽ tìm kiếm và trả về đường dẫn thực thi của `gcc`, bỏ qua các bí danh có thể đã được định nghĩa trong shell.

**Lưu Ý Khi Sử Dụng `which`**

- `which` chỉ tìm kiếm trong các thư mục được liệt kê trong biến `PATH`. Nếu một lệnh nằm ngoài các thư mục này, `which` sẽ không tìm thấy nó.
- `which` chỉ có thể tìm các lệnh thực thi, không tìm được các script hoặc các file thực thi không nằm trong `PATH`.


