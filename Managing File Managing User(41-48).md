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

1. **`-a`**: Hiển thị tất cả các tệp, bao gồm cả các tệp ẩn (các tệp bắt đầu bằng dấu `.`).
   ```bash
   ls -a
   ```

2. **`-l`**: Hiển thị chi tiết theo dạng danh sách, bao gồm thông tin về quyền truy cập, số lượng liên kết, chủ sở hữu, nhóm, kích thước, và thời gian chỉnh sửa cuối.
   ```bash
   ls -l
   ```

3. **`-h`**: Hiển thị kích thước tệp theo dạng dễ đọc (KB, MB, GB), thường sử dụng cùng với `-l`.
   ```bash
   ls -lh
   ```

4. **`-R`**: Liệt kê tất cả các tệp trong thư mục hiện tại và các thư mục con (đệ quy).
   ```bash
   ls -R
   ```

5. **`-d`**: Chỉ hiển thị thư mục, không liệt kê nội dung bên trong.
   ```bash
   ls -d */
   ```

6. **`-t`**: Sắp xếp tệp theo thời gian chỉnh sửa cuối, từ mới nhất đến cũ nhất.
   ```bash
   ls -lt
   ```

7. **`-r`**: Sắp xếp theo thứ tự ngược lại, ví dụ: từ Z đến A hoặc từ mới nhất đến cũ nhất khi kết hợp với `-t`.
   ```bash
   ls -lr
   ```

8. **`-S`**: Sắp xếp tệp theo kích thước, từ lớn nhất đến nhỏ nhất.
   ```bash
   ls -lS
   ```

9. **`--color`**: Hiển thị màu sắc để phân biệt loại tệp và thư mục.
   ```bash
   ls --color=auto
   ```

10. **`-i`**: Hiển thị số inode của mỗi tệp.
    ```bash
    ls -i
    ```

11. **`-1`**: Hiển thị mỗi tệp trên một dòng.
    ```bash
    ls -1
    ```

12. **`-X`**: Sắp xếp theo phần mở rộng của tệp.
    ```bash
    ls -lX
    ```

13. **`-F`**: Thêm ký tự xác định loại tệp, ví dụ: `/` cho thư mục, `*` cho tệp thực thi.
    ```bash
    ls -F
    ```    

**2.2 cp**

1. **`-r`**: Sao chép thư mục đệ quy (recursively), bao gồm cả các thư mục con. Bắt buộc dùng khi sao chép thư mục.
   ```bash
   cp -r source_directory destination_directory
   ```

2. **`-i`**: Chế độ tương tác (interactive), yêu cầu xác nhận nếu tệp đích đã tồn tại.
   ```bash
   cp -i source_file destination_file
   ```

3. **`-f`**: Ghi đè tệp đích mà không cần yêu cầu xác nhận (force).
   ```bash
   cp -f source_file destination_file
   ```

4. **`-u`**: Chỉ sao chép nếu tệp nguồn mới hơn tệp đích hoặc nếu tệp đích chưa tồn tại (update).
   ```bash
   cp -u source_file destination_file
   ```

5. **`-v`**: Hiển thị chi tiết quá trình sao chép (verbose).
   ```bash
   cp -v source_file destination_file
   ```

6. **`-p`**: Bảo toàn các thuộc tính của tệp, như quyền truy cập, thời gian chỉnh sửa, và chủ sở hữu (preserve attributes).
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

10. **`--backup`**: Tạo bản sao lưu tệp đích nếu tệp đã tồn tại. Sử dụng cùng với `-b` để tạo bản sao lưu tự động.
    ```bash
    cp --backup source_file destination_file
    ```

11. **`--parents`**: Giữ lại cấu trúc thư mục của tệp nguồn khi sao chép vào thư mục đích.
    ```bash
    cp --parents source_directory/file destination_directory
    ```

12. **`--remove-destination`**: Xóa tệp đích trước khi sao chép (hữu ích khi tệp đích có quyền chỉ đọc).
    ```bash
    cp --remove-destination source_file destination_file
    ```

13. **`--sparse=WHEN`**: Kiểm soát cách sao chép tệp thưa (sparse file) để tiết kiệm dung lượng. `WHEN` có thể là `auto`, `always`, hoặc `never`.
    ```bash
    cp --sparse=always source_file destination_file
    ```

14. **`-n`**: Không sao chép nếu tệp đích đã tồn tại (no-clobber).
    ```bash
    cp -n source_file destination_file
    ```

