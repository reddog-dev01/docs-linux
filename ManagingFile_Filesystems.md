**1. Understand File System Type**  
**1.1 File System là gì**  
- Một cách thức để quản lý và tổ chức dữ liệu trên các thiết bị lưu trữ ( ổ cứng, thẻ nhớ, SSD...)  
**Các thành phần cơ bản của 1 file system**
  1. Tệp(file)
  2. Thư mục (directory) lưu trữ các tệp và các thư mục con.
  3. Bảng phân vùng (partition table): Phân vùng ổ đĩa là ncasc đơn vị logic mà hệ thống tệp sử dụng để lưu trữ dữ liệu. Mỗi phân vùng có thể chứa 1 tệp hệ thống riêng biệt.
  4. Chỉ mục và inode: Là các cấu trúc dữ liệu mà hệ thống tệp sử dụng để lưu trữ thông tin về tệp như tên tệp, quyền truy cập, vị trí của tệp trên ổ đĩa, thời gian tạo, sửa, truy cập cuối.  
**Chức năng**
- Lưu trữ dữ liệu: Quản lý cách tệp được lưu trữ trên các thiết bị lưu trữ
- Tổ chức dữ liệu: Cung cấp các phương thức tổ chức dữ liệu (thư mục, tệp)
- Quản lý quyền truy cập: Quyền truy cập tệp được kiểm soát bởi hệ thống tệp, cho phép or từ chối quyền đọc, ghi, sửa của người dùng.
- Quản lý không gian lưu trữ: Hệ thống tệp phân bổ và giải phóng không gian trên ổ đĩa khi tệp được tạo hoặc xóa.  
**1.2 Các loại File System**  
**a. Ext4**
- Hệ thống tệp mặc định trong hầu hết các bản phối linux. Hiệu suất tốt, khả năng mở rộng cao
- Hỗ trợ tính năng journaling, giúp bảo vệ dữ liệu khỏi bị hỏng nếu hệ thống bị tắt đột ngột
- Thường sử dụng cho các phân vùng gốc `/` và các phân vùng dữ liệu trên các hệ thống Linux.
- 16TB, sử dụng trong máy tính cá nhân, máy chủ và các hệ thống lưu trữ thông thường.  
**b. Ext3**
- Tiền thân của Ext4 hỗ trợ tính năng journaling nhưng không có khả năng cải tiến hiệu suất và mở rộng.
- Kích thước tối đa 2TB
- Sử dụng: máy chủ cũ hoặc thiết bị lưu trữ không yêu cầu hiệu suất cao.
**c. Ext2**
- Đời thứ 2 của Extended, không có tính năng journaling.
- Thích thước tối đa 2GB (trên kernel cũ 2.x, 3.x), 4TB (trên kernel mới)
- Sử dụng phổ biến: thẻ nhớ, USB, phân vùng không yêu cầu journaling
**d. Btrfs (B-tree file system)
- Hệ thống tệp hiện đại với nhiều tính năng mạnh mẽ như snapshotting (giúp quay lại trạng thái hệ thống trước đó), compression (tiết kiệm không gian đĩa), RAID (quản lý nhiều ổ đĩa trong file system).
- Sử dụng trong các máy chủ hoặc hệ thống cần khả năng phục hồi cao.
- 16EB
**d. XFS**
- Chủ yếu sử dụng trong các hệ thống lưu trữ có dung lượng lớn.
- Hiệu suất cao, hỗ trợ journaling.
- Tối ưu hóa cho lưu trữ lớn, đặc biệt là dữ liệu song song.
- Khả năng mở rộng tốt phù hợp cho các hệ thống có phân vùng rất lớn (500TB).
- Hệ thống lưu trữ lớn, cơ sở dữ liệu.

**2. Check file system `fsck`**  
**2.1 Cách sử dụng `fsck`**  
*1. Kiểm tra cơ bản*
```
sudo fsck /dev/...
```
*2. `-y`: Tự động trả lời "yes" cho tất cả các yêu cầu sửa lỗi.*  
```
sudo fsck -y /dev/sdXN
```  
*3. `-n`: Chỉ kiểm tra mà không sửa lỗi. fsck sẽ trả lời "no" cho tất cả yêu cầu sửa lỗi.*  
```
sudo fsck -n /dev/sdXN
```  
*4. `-f`: Buộc kiểm tra ngay cả khi hệ thống tập tin đã được đánh dấu là sạch (không có lỗi).*  
```
sudo fsck -f /dev/sdXN
```  
*5. `-c`: Kiểm tra các khối hỏng (bad blocks) trên ổ đĩa.*  
```  
sudo fsck -c /dev/sdXN
```  
*6. `-C`: Hiển thị tiến trình kiểm tra dưới dạng thanh tiến độ.*  
```
sudo fsck -C /dev/sdXN
```  
*7. `-t`: Chỉ định loại hệ thống tập tin để kiểm tra (như ext4, xfs...).*
```
sudo fsck -t ext4 /dev/sdXN
```  
*8. `-A`: Kiểm tra tất cả các hệ thống tập tin được liệt kê trong /etc/fstab. Điều này hữu ích khi bạn muốn kiểm tra toàn bộ các phân vùng.*
```
sudo fsck -A
```  
*9. `-M`: Bỏ qua các phân vùng đã gắn kết (được mount).*
```
sudo fsck -AM
```  
*10. `-V`: Hiển thị thông tin chi tiết khi kiểm tra.*
```
sudo fsck -V /dev/sdXN
```

**3. Monitoring Disk: `df`, `du`**  
**3.1 Cách kiểm tra dung lượng bằng `df`**  
*1. `-h` (Human-readable): Hiển thị dung lượng ở dạng dễ đọc (KB, MB, GB).*
```
df -h
```  
*2. `-a` (All): Hiển thị tất cả các file hệ thống, bao gồm cả những file hệ thống có dung lượng bằng 0.*
```
df -a
```  
*3. `-T`: Hiển thị loại hệ thống tập tin của mỗi phân vùng.*
```
df -T
```  
*4. `-i`: Hiển thị thông tin về các inode thay vì dung lượng bộ nhớ. Inode là các chỉ mục quản lý thông tin file trên hệ thống.*
```
df -i
```  
*5. `-l` (Local): Chỉ hiển thị các file hệ thống cục bộ, bỏ qua các hệ thống được gắn kết từ xa.*
```
df -l
```  
*6. `--total`: Tính tổng dung lượng cho tất cả các file hệ thống.*
```
df -h --total
```  
*7. `-x` (Exclude): Loại trừ một hoặc nhiều loại hệ thống file nhất định khỏi kết quả.*
```  
df -x tmpfs
```  
*8. `--output`: Chỉ hiển thị các cột cụ thể, cho phép tùy chỉnh các thông tin hiển thị như source, size, used, avail, pcent, target.*
```
df --output=source,size,used,avail,pcent
```  
*9. `-P` (POSIX): Hiển thị kết quả ở định dạng tương thích với POSIX, đảm bảo các giá trị nằm trong một dòng duy nhất.*
```
df -P
```  
  
**3.2 Cách kiểm tra dung lượng bằng `du`**  

1. **`-h`** (Human-readable): Hiển thị dung lượng ở dạng dễ đọc (KB, MB, GB).
   ```bash
   du -h
   ```

2. **`-s`** (Summarize): Chỉ hiển thị tổng dung lượng của thư mục hoặc file được chỉ định, thay vì liệt kê từng file và thư mục con.
   ```bash
   du -sh /path/to/directory
   ```

3. **`-a`** (All): Hiển thị dung lượng của tất cả các file và thư mục con trong thư mục chỉ định.
   ```bash
   du -a /path/to/directory
   ```

4. **`-c`** (Total): Hiển thị tổng dung lượng sau khi liệt kê chi tiết từng file và thư mục.
   ```bash
   du -c /path/to/directory
   ```

5. **`-d`** (Depth): Giới hạn độ sâu thư mục để kiểm tra. Ví dụ, `-d 1` sẽ chỉ kiểm tra các thư mục con cấp 1 trong thư mục chỉ định.
   ```bash
   du -h -d 1 /path/to/directory
   ```

6. **`-x`**: Chỉ kiểm tra các file và thư mục trên cùng một file hệ thống (phân vùng), bỏ qua các file và thư mục được gắn kết từ hệ thống khác.
   ```bash
   du -x /path/to/directory
   ```

7. **`--max-depth`**: Tương tự như `-d`, chỉ định độ sâu tối đa của thư mục để kiểm tra.
   ```bash
   du -h --max-depth=2 /path/to/directory
   ```

8. **`--exclude`**: Loại trừ các file hoặc thư mục có tên phù hợp với mẫu đã chỉ định khỏi kết quả.
   ```bash
   du -h --exclude="*.log" /path/to/directory
   ```

9. **`-t`** (Threshold): Chỉ hiển thị các file và thư mục có dung lượng lớn hơn hoặc bằng kích thước xác định (theo KB, MB, hoặc GB).
   ```bash
   du -h -t 100M /path/to/directory
   ```

10. **`--time`**: Hiển thị thời gian sửa đổi cuối cùng của các file và thư mục (nếu được hỗ trợ).
    ```bash
    du -h --time /path/to/directory
    ```

### Ví dụ kết hợp các tùy chọn
1. Hiển thị tổng dung lượng các thư mục cấp 1 dưới dạng dễ đọc:
   ```bash
   du -h -d 1 /path/to/directory
   ```

2. Liệt kê tất cả các file và thư mục con với tổng dung lượng cuối cùng:
   ```
   du -ahc /path/to/directory
   ```
