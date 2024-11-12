### **1. Understand File System Type** 
 
### **1.1 File System là gì**  

- Một cách thức để quản lý và tổ chức dữ liệu trên các thiết bị lưu trữ ( ổ cứng, thẻ nhớ, SSD...)
-  
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

### **1.2 Các loại File System**
  
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

**d. Btrfs (B-tree file system)**
- Hệ thống tệp hiện đại với nhiều tính năng mạnh mẽ như snapshotting (giúp quay lại trạng thái hệ thống trước đó), compression (tiết kiệm không gian đĩa), RAID (quản lý nhiều ổ đĩa trong file system).
- Sử dụng trong các máy chủ hoặc hệ thống cần khả năng phục hồi cao.
- 16EB

**e. XFS**
- Chủ yếu sử dụng trong các hệ thống lưu trữ có dung lượng lớn.
- Hiệu suất cao, hỗ trợ journaling.
- Tối ưu hóa cho lưu trữ lớn, đặc biệt là dữ liệu song song.
- Khả năng mở rộng tốt phù hợp cho các hệ thống có phân vùng rất lớn (500TB).
- Hệ thống lưu trữ lớn, cơ sở dữ liệu.

### **2. Check file system `fsck`**  

### **2.1 Cách sử dụng `fsck`**  

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

### **3. Monitoring Disk: `df`, `du`**  

### **3.1 Cách kiểm tra dung lượng bằng `df`**  

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
  
### **3.2 Cách kiểm tra dung lượng bằng `du`**  

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
### **3.3 Sự khác nhau giữa `du` và `df`**

| **Thuộc tính**          | **`du`**                                            | **`df`**                                      |
|-------------------------|-----------------------------------------------------|-----------------------------------------------|
| **Mục đích**            | Kiểm tra dung lượng file/thư mục đang chiếm               | Kiểm tra dung lượng phân vùng (gồm đã sử dụng và còn trống)                 |
| **Cách tính toán**      | Tính dung lượng thực tế của các file/thư mục, bao gồm cả các file đã bị xóa nhưng vẫn đang mở bởi một tiến trình                  | Lấy thông tin từ hệ thống file phân vùng      |
| **Kết quả hiển thị**    | Dung lượng thực tế của thư mục/file đang chiếm                 | Tổng dung lượng, đã dùng và còn trống         |
| **Tình huống sử dụng**  | Khi muốn biết thư mục nào đang chiếm nhiều dung lượng | Khi muốn biết tình trạng dung lượng của phân vùng |

### **4. Creating Filesystems: `mkfs`**

Lệnh này giúp định dạng một phân vùng hoặc thiết bị lưu trữ để chuẩn bị nó sẵn sàng cho việc lưu trữ dữ liệu bằng một loại hệ thống file cụ thể, chẳng hạn như `ext4`, `xfs`, `ntfs`, hoặc `vfat`.

```bash
mkfs -t <loại_hệ_thống_file> <thiết_bị>
```

Trong đó:
- **`-t <loại_hệ_thống_file>`**: Chỉ định loại hệ thống file muốn tạo (ví dụ: `ext4`, `xfs`, `vfat`, v.v.).
- **`<thiết_bị>`**: Là phân vùng hoặc thiết bị đích muốn tạo hệ thống file trên đó (ví dụ: `/dev/sda1`).

**VD: Tạo hệ thống file ext4 trên phân vùng `/dev/sda1`:**

   ```bash
   mkfs -t ext4 /dev/sda1
   ```
hoặc
```
mkfs.ext4 /dev/sda1
```

### Lưu ý khi sử dụng `mkfs`

- **Xóa dữ liệu**: Lệnh `mkfs` sẽ xóa tất cả dữ liệu hiện có trên phân vùng hoặc thiết bị, vì nó sẽ tạo lại hệ thống file từ đầu.
- **Quyền quản trị**: cần quyền `root` hoặc `sudo` để sử dụng `mkfs` vì lệnh này can thiệp trực tiếp vào thiết bị lưu trữ.
- **Kiểm tra đúng phân vùng**: Đảm bảo bạn chọn đúng phân vùng hoặc thiết bị để tránh mất dữ liệu do tạo nhầm hệ thống file trên phân vùng chứa dữ liệu quan trọng.

### **4. Mounting and Unmounting Filesystems**

**Mount:** 

- Sử dụng để kết nối file system của một thiết bị lưu trữ (ổ cứng, USB, thiết bị mạng) và cây thư mục của HĐH. Cho phép người dùng truy cập vào dữ liệu trên thiết bị đó như 1 phần của hệ thống tập tin chính.
- Dùng để sao lưu, khôi phụ dữ liệu, mở rộng không gian lưu trữ.

```bash
sudo mount [options] <device> <directory>
```
- `<device>`: là tập tin thiết bị của thiết bị lưu trữ (ví dụ, `/dev/sda1`).
- `<directory>`: là thư mục nơi thiết bị sẽ được gắn kết, thường được gọi là điểm gắn kết (ví dụ, `/mnt` hoặc `/media`).

**Ví dụ:**

1. *Gắn kết ổ USB:*
   ```bash
   sudo mount /dev/sdb1 /mnt/usb
   ```
   Lệnh này gắn kết phân vùng `/dev/sdb1` vào điểm gắn kết `/mnt/usb`.

2. *Gắn kết với loại hệ thống tập tin cụ thể:*
   Nếu bạn biết loại hệ thống tập tin (ví dụ, ntfs, ext4), bạn có thể chỉ định nó với tùy chọn `-t`.
   ```bash
   sudo mount -t ext4 /dev/sda1 /mnt/data
   ```

3. *Gắn kết chỉ đọc:*
   Để gắn kết hệ thống tập tin ở chế độ chỉ đọc, sử dụng tùy chọn `-o`.
   ```bash
   sudo mount -o ro /dev/sdb1 /mnt/usb
   ```
   
**Unmount:**

 - Sử dụng để ngắn kết nối file system đã được mount. Mọi dữ liệu đang được truy cập hoàn tất và thiết bị sẽ không bị ảnh hưởng.
 - Ngăn ngừa mất mát hoặc hư hại dữ liệu khi gỡ bỏ thiết bị lưu trữ, đảm bảo mọi thao tác đọc ghi hoàn tất trc khi thiết bị tách khỏi hệ thống.
Để sử dụng hiệu quả các lệnh `mount` và `umount` trong Linux, rất quan trọng là bạn phải hiểu cú pháp và các tùy chọn cơ bản của chúng. Dưới đây là hướng dẫn chi tiết cách sử dụng hai lệnh này.

```bash
sudo umount <directory or device>
```

**Ví dụ:**

1. *Ngắt kết nối bằng điểm gắn kết:*
   ```bash
   sudo umount /mnt/usb
   ```
   Lệnh này ngắt kết nối hệ thống tập tin từ `/mnt/usb`.

2. *Ngắt kết nối bằng thiết bị:*
   ```bash
   sudo umount /dev/sdb1
   ```
   Tương tự, lệnh này ngắt kết nối thiết bị `/dev/sdb1` ở bất cứ đâu nó đang được gắn.
   
### **5. Disks Partioning**

Disk partitioning là quá trình chia ổ đĩa cứng vật lý thành các phần riêng biệt, mỗi phần được gọi là một phân vùng (partition). Mỗi phân vùng hoạt động như một ổ đĩa độc lập, cho phép cài đặt nhiều hệ điều hành hoặc tổ chức dữ liệu một cách linh hoạt hơn. Các loại phân vùng phổ biến gồm:

- **Primary Partition**: Có thể chứa hệ điều hành.
- **Extended Partition**: Chứa các phân vùng logic và mở rộng không gian khi thiếu chỗ.
- **Logical Partition**: Dùng để lưu trữ dữ liệu trong phân vùng mở rộng. 

Mục đích của việc phân vùng ổ đĩa (disk partitioning) là:

1. **Cài đặt nhiều hệ điều hành**: Mỗi phân vùng có thể chứa một hệ điều hành riêng, cho phép chuyển đổi giữa các hệ điều hành mà không ảnh hưởng lẫn nhau.
   
2. **Quản lý dữ liệu tốt hơn**: Phân chia dữ liệu như hệ thống, ứng dụng và file cá nhân giúp bảo vệ dữ liệu và quản lý dễ dàng hơn.

3. **Tăng hiệu quả khôi phục**: Khi gặp sự cố, bạn có thể cài đặt lại hệ điều hành mà không mất dữ liệu cá nhân trên các phân vùng khác.
  
4. **Tăng hiệu suất**: Tổ chức các loại dữ liệu trên từng phân vùng riêng giúp hệ thống truy xuất nhanh hơn.

### **6. `fdiks` và sự khác nhau giữa file system vs partition**

### **6.1 `fdisk`**

`fdisk` là công cụ phân vùng đĩa mạnh mẽ được sử dụng trong các hệ thống dựa trên Linux để quản lý các phân vùng ổ cứng. Nó rất hữu ích cho việc tạo, sửa đổi, và xóa bảng phân vùng, cũng như thiết lập các phân vùng để cài đặt Linux hoặc quản lý cấu hình khởi động kép. Dưới đây là cách sử dụng `fdisk` để quản lý các phân vùng đĩa:

### Các bước sử dụng `fdisk`

1. **Liệt kê các đĩa và phân vùng hiện có**
   - Mở terminal.
   - Chạy `sudo fdisk -l` để liệt kê tất cả các đĩa và phân vùng trên hệ thống của bạn, giúp xác định đĩa bạn muốn làm việc.

2. **Bắt đầu `fdisk`**
   - Truy cập `fdisk` trên một đĩa cụ thể với `sudo fdisk /dev/sda`, thay thế `/dev/sda` bằng định danh đĩa của bạn.
   - Lệnh này mở menu `fdisk` cho đĩa cụ thể đó.

3. **Di chuyển trong menu `fdisk`**
   - Trong `fdisk`, bạn có thể nhập `m` để xem tất cả các lệnh có sẵn.
   - Các lệnh trong `fdisk` bao gồm tạo phân vùng mới (`n`), xóa phân vùng (`d`), và ghi thay đổi vào đĩa (`w`).

4. **Tạo một phân vùng**
   - Nhấn `n` để tạo phân vùng mới.
   - Chọn tạo phân vùng chính (`p`) hoặc mở rộng (`e`). Hầu hết người dùng sẽ chọn chính.
   - Xác định số phân vùng (1-4 cho phân vùng chính).
   - Nhập số sector đầu và cuối hoặc chỉ cần nhấn Enter để chấp nhận các giá trị mặc định, sử dụng không gian khả dụng tối đa.

5. **Xóa một phân vùng**
   - Nhấn `d` để xóa một phân vùng.
   - Nhập số của phân vùng bạn muốn xóa.

6. **Thay đổi loại phân vùng**
   - Nếu cần, bạn có thể thay đổi loại phân vùng bằng cách nhấn `t`.
   - Sau đó nhập số phân vùng và mã cho loại hệ thống mong muốn (`L` liệt kê tất cả các mã).

7. **Ghi thay đổi**
   - Để lưu tất cả các thay đổi bạn đã thực hiện, nhấn `w`. Điều này sẽ ghi bảng phân vùng mới vào đĩa và thoát `fdisk`.
   - Hãy cẩn thận, vì bước này làm cho các thay đổi trở nên vĩnh viễn.

8. **Thoát không lưu**
   - Nếu bạn cần thoát mà không thực hiện thay đổi, nhấn `q`. Điều này sẽ thoát `fdisk` mà không lưu bất kỳ thay đổi nào.

### Lưu ý khi sử dụng `fdisk`

- **Sao lưu dữ liệu:** Luôn sao lưu dữ liệu quan trọng trước khi sửa đổi các phân vùng đĩa vì các thay đổi có thể dẫn đến mất dữ liệu nếu không được xử lý cẩn thận.
- **Quyền quản trị:** `fdisk` yêu cầu quyền quản trị; sử dụng `sudo` để chạy nó.
- **Hệ thống tập tin:** Sau khi tạo các phân vùng, bạn cần tạo hệ thống tập tin trên chúng (sử dụng các lệnh `mkfs` như `mkfs.ext4 /dev/sda1`) trước khi bạn có thể sử dụng chúng.
- **Kiểm tra thay đổi:** Sau khi phân vùng, sử dụng `sudo fdisk -l` hoặc `lsblk` để kiểm tra cấu trúc

phân vùng mới của bạn.
