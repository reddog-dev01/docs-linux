### **1. Understand File System Type** 
 
### **1.1 File System là gì**  

- Một cách thức để quản lý và tổ chức dữ liệu trên các thiết bị lưu trữ ( ổ cứng, thẻ nhớ, SSD...)
- xác định cách dữ liệu được lưu trữ, truy cập, và quản lý, đồng thời cung cấp cấu trúc logic để hệ điều hành và người dùng có thể làm việc với dữ liệu

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
- Ext4 lưu trữ dữ liệu dưới dạng các dải liên tiếp (extents)
- Delayed Allocation Thay vì phân bổ khối ngay khi nhận yêu cầu ghi, hệ thống Ext4 sẽ lưu dữ liệu tạm thời trong bộ nhớ đệm (buffer) Khi đủ dữ liệu hoặc cần ghi thực sự, Ext4 sẽ phân bổ khối trên đĩa và ghi dữ liệu xuống
- Hỗ trợ tính năng journaling(ghi lại các thay đổi trước khi áp dụng lên filesystem), giúp bảo vệ dữ liệu khỏi bị hỏng nếu hệ thống bị tắt đột ngột
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

**Inode** (viết tắt của **Index Node**) là một cấu trúc dữ liệu được sử dụng trong hệ thống tệp của Unix/Linux. Nó đóng vai trò như một "danh bạ" lưu trữ thông tin chi tiết về một tệp hoặc thư mục trong hệ thống tệp. 

 **Chức năng của inode**
**Lưu trữ thông tin tệp**: 
   Mỗi tệp hoặc thư mục trên hệ thống đều được gắn với một inode. Inode chứa các thông tin cần thiết để hệ thống quản lý tệp, bao gồm:
   - Quyền truy cập tệp (permissions).
   - Chủ sở hữu (user ID).
   - Nhóm sở hữu (group ID).
   - Kích thước tệp.
   - Loại tệp (thông thường, thư mục, liên kết, v.v.).
   - Thời gian truy cập gần nhất (last accessed).
   - Thời gian sửa đổi gần nhất (last modified).
   - Vị trí lưu trữ dữ liệu trên đĩa.

**Quản lý vị trí tệp trên đĩa**: 
   Inode không lưu tên tệp; thay vào đó, nó chứa các con trỏ trỏ tới các khối dữ liệu (data blocks) nơi nội dung thực sự của tệp được lưu trữ trên đĩa.

**Hỗ trợ hệ thống tệp hiệu quả hơn**: 
   - Mỗi hệ thống tệp có một số lượng inode cố định, được xác định khi hệ thống tệp được tạo.
   - Các inode giúp nhanh chóng tìm kiếm và quản lý dữ liệu mà không cần duyệt qua toàn bộ ổ đĩa.

---

**Thông tin KHÔNG được lưu trong inode**
Inode không lưu trữ tên tệp. Thay vào đó:
- Tên tệp được lưu trong thư mục cùng với số inode tương ứng.
- Khi truy cập tệp bằng tên, hệ thống tìm số inode liên quan trong thư mục, sau đó truy cập inode để tìm thông tin chi tiết.

---

**Ví dụ hoạt động của inode**
Khi mở một file:
1. Hệ thống tệp tra cứu tên tệp trong thư mục.
2. Lấy số inode liên kết với tên tệp.
3. Sử dụng inode để tìm các khối dữ liệu nơi nội dung tệp được lưu trữ.

---

**Ứng dụng thực tế**
- **Khắc phục lỗi đầy inode**: Dù vẫn còn dung lượng trống trên ổ đĩa, không thể tạo thêm tệp nếu số lượng inode đã hết.
- **Kiểm tra inode bằng lệnh**:
  ```bash
  ls -i          # Hiển thị số inode của các tệp/thư mục
  ```

### **3.1 Cách kiểm tra dung lượng bằng `df`**  

*1. `-h` (Human-readable): Hiển thị dung lượng ở dạng dễ đọc (KB, MB, GB).*
```
df -h
```  
*2. `-a` (All): Hiển thị tất cả các file hệ thống, bao gồm cả những file hệ thống có dung lượng bằng 0.*
```
df -a
```  
*3. `-T`: Hiển thị loại file system của mỗi phân vùng.*
```
df -T
```  
*4. `-i`: Hiển thị thông tin về các inode thay vì dung lượng bộ nhớ*
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

 **Lưu ý khi sử dụng `mkfs`**

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

### Các bước sử dụng `fdisk`

1. **Liệt kê các đĩa và phân vùng hiện có**
   - `sudo fdisk -l` để liệt kê tất cả các đĩa và phân vùng.
   - Xem cụ thể VD: `sudo fdisk -l /dev/sda`.

2. **Bắt đầu `fdisk`**
   - Truy cập `fdisk` trên một đĩa cụ thể với `sudo fdisk /dev/sda`.
   - Lệnh này mở menu `fdisk` cho đĩa cụ thể đó.

3. **Di chuyển trong menu `fdisk`**

   `m` - Hiển thị menu lệnh.
   
    `p` - Liệt kê bảng phân vùng.
   
    `n` - Tạo phân vùng mới.
   
    `d` - Xóa phân vùng.
   
    `t` - Thay đổi ID hệ thống của phân vùng.
   
        LƯU Ý: mỗi phân vùng sẽ tự động được cấp phát dưới dạng 'Linux' (loại 83) trừ khi
        thay đổi
        
        Các loại phân vùng cần biết:
      
        82 - Linux swap
      
        83 - Linux
      
        85 - Linux extended
      
        8e - Linux LVM
      
        fd - Linux RAID
   
    `w` - Ghi các thay đổi và thoát.
   
    `q`- Thoát mà không lưu các thay đổi.

5. **Tạo một phân vùng**
   - Nhấn `n` để tạo phân vùng mới.
   - Chọn tạo phân vùng chính (`p`) hoặc mở rộng (`e`). Hầu hết người dùng sẽ chọn chính.
   - Xác định số phân vùng (1-4 cho phân vùng chính).
   - Nhập số sector đầu và cuối hoặc chỉ cần nhấn Enter để chấp nhận các giá trị mặc định, sử dụng không gian khả dụng tối đa.

6. **Xóa một phân vùng**
   - Nhấn `d` để xóa một phân vùng.
   - Nhập số của phân vùng bạn muốn xóa.

7. **Thay đổi loại phân vùng**
   - Nếu cần, bạn có thể thay đổi loại phân vùng bằng cách nhấn `t`.
   - Sau đó nhập số phân vùng và mã cho loại hệ thống mong muốn (`L` liệt kê tất cả các mã).

8. **Ghi thay đổi**
   - Để lưu tất cả các thay đổi bạn đã thực hiện, nhấn `w`. Điều này sẽ ghi bảng phân vùng mới vào đĩa và thoát `fdisk`.
   - Hãy cẩn thận, vì bước này làm cho các thay đổi trở nên vĩnh viễn.

9. **Thoát không lưu**
   - Nếu bạn cần thoát mà không thực hiện thay đổi, nhấn `q`. Điều này sẽ thoát `fdisk` mà không lưu bất kỳ thay đổi nào.

### Lưu ý khi sử dụng `fdisk`
- 
- **Sao lưu dữ liệu:** Luôn sao lưu dữ liệu quan trọng trước khi sửa đổi các phân vùng đĩa vì các thay đổi có thể dẫn đến mất dữ liệu nếu không được xử lý cẩn thận.
- **Quyền quản trị:** `fdisk` yêu cầu quyền quản trị; sử dụng `sudo` để chạy nó.
- **Hệ thống tập tin:** Sau khi tạo các phân vùng, cần tạo hệ thống tập tin trên chúng (sử dụng các lệnh `mkfs` như `mkfs.ext4 /dev/sda1`) trước khi có thể sử dụng chúng.
- **Kiểm tra thay đổi:** Sau khi phân vùng, sử dụng `sudo fdisk -l` hoặc `lsblk` để kiểm tra cấu trúc phân vùng mới.

### **6.2 Phân biệt file system vs patition**

**Patition (Phân vùng)**

- **Định nghĩa:** Một partition là một phần của ổ đĩa cứng được tách ra để có thể sử dụng riêng biệt. Mỗi phân vùng có thể được định dạng với một file system riêng và hoạt động như một ổ đĩa độc lập trong hệ thống.
- **Chức năng:** Phân vùng cho phép bạn chia nhỏ ổ đĩa cứng thành nhiều khu vực riêng biệt, mỗi khu vực có thể chứa hệ điều hành, dữ liệu hoặc một loại thông tin cụ thể. Điều này hữu ích cho việc quản lý dữ liệu, cài đặt nhiều hệ điều hành trên một máy, hoặc tách dữ liệu cá nhân ra khỏi hệ thống tập tin của hệ điều hành.

**File System (Hệ thống tập tin)**

- **Định nghĩa:** file system là phương pháp tổ chức và quản lý dữ liệu trên phân vùng đĩa. Nó quy định cách dữ liệu được lưu trữ và truy cập trên phân vùng đó.
- **Chức năng:** file system kiểm soát cách dữ liệu được lưu trữ trong một phân vùng, bao gồm cách tạo, lưu trữ và xóa các tệp. Nó cũng quản lý metadata, bao gồm tên tệp, quyền truy cập, ngày tạo, và kích thước tệp.

**Mối quan hệ giữa File System và Partition**
- Một partition cần có một file system để dữ liệu bên trong nó có thể được sử dụng và quản lý một cách hiệu quả. Ví dụ, khi định dạng một patition mới trên ổ cứng, bạn có thể chọn định dạng FAT32, EXT4, v.v.

- **Lưu ý:** Một patition không có file system được gọi là patition "raw" hoặc "chưa định dạng" và không thể được sử dụng để lưu trữ dữ liệu cho đến khi một file system được thiết lập.

### 6. Understanding RAID, ‘mdadm' command**

**6.1 Khái niệm và cấu trúc RAID**

RAID là một công nghệ lưu trữ được sử dụng để kết hợp nhiều ổ đĩa vật lý thành 1 đơn vị duy nhất với mục đích cải thiện hiệu suất, độ tin cậy.

**Cấu trúc**

1. Ổ đĩa vật lý (physical disks): Các ổ cứng, SSD được sử dụng trong mảng RAID (min 2)
2. Bộ điều khiển RAID (RAID Controller): 1 phần cứng hoặc phần mềm điều khiển cách thức dữ liệu được ghi và đọc từ các ổ đĩa (1 card phần cứng riêng hoặc được tích hợp vào bo mạch chủ, hoặc 1 phần mềm được tích hợp vào HĐH)
3. Mảng đĩa (Array): 1 nhóm các ổ đĩa được tổ chức và quản lý bởi RAID
4. Phương thức lưu trữ:
- Striping (Phân chia dải): Tách luồng dữ liệu thành các khối có kích thước nhất định (được gọi là kích thước khối) sau đó viết từng khối này qua từng RAID. Cách lưu trữ dữ liệu này ảnh hưởng đến hiệu suất.
- Mirroring (mirroring): Là một kỹ thuật lưu trữ trong đó các bản sao dữ liệu giống hệt nhau được lưu trữ trên các thành viên RAID cùng một lúc. Loại vị trí dữ liệu này ảnh hưởng đến khả năng chịu lỗi cũng như hiệu suất.
- Parity là một kỹ thuật lưu trữ được sử dụng các phương pháp phân loại và tổng kiểm tra. Trong kỹ thuật chẵn lẻ, một hàm chẵn lẻ nhất định được tính cho các khối dữ liệu. Nếu một ổ đĩa bị lỗi, khối bị thiếu được tính toán lại từ tổng kiểm tra, cung cấp khả năng chịu lỗi RAID.

**6.2 Nguyên lý hoạt động**

Các phương thức lưu trữ dữ liệu chính trong mảng là:

**Striping (Phân chia dải):** Tách luồng dữ liệu thành các khối có kích thước nhất định (được gọi là kích thước khối) sau đó viết từng khối này qua từng RAID. Cách lưu trữ dữ liệu này ảnh hưởng đến hiệu suất.

**Mirroring (mirroring):** Là một kỹ thuật lưu trữ trong đó các bản sao dữ liệu giống hệt nhau được lưu trữ trên các thành viên RAID cùng một lúc. Loại vị trí dữ liệu này ảnh hưởng đến khả năng chịu lỗi cũng như hiệu suất.

**Parity** là một kỹ thuật lưu trữ được sử dụng các phương pháp phân loại và tổng kiểm tra. Trong kỹ thuật chẵn lẻ, một hàm chẵn lẻ nhất định được tính cho các khối dữ liệu. Nếu một ổ đĩa bị lỗi, khối bị thiếu được tính toán lại từ tổng kiểm tra, cung cấp khả năng chịu lỗi RAID.

**a. RAID 0**

RAID 0 – dựa trên kỹ thuật striping. Mức RAID này không cung cấp khả năng chịu lỗi nhưng tăng hiệu năng hệ thống (tốc độ đọc và ghi cao). RAID 0 cần ít nhất 2 ổ đĩa (có thể sử dụng 1 ổ đĩa). Tổng quát ta có n đĩa (n>=2) và các đĩa là cùng loại. Dữ liệu sẽ được chia ra thành nhiều phần bằng nhau.

![image](https://github.com/user-attachments/assets/ed328f6f-0747-4c1b-b967-bb63e8b95377)

**Ưu điểm:** Tăng tốc độ đọc/ghi ổ đĩa, mỗi đĩa chỉ cần đọc/ghi 1/n lượng dữ liệu yêu cầu.

**Nhược điểm:** Tính an toàn thấp vì nếu một đĩa hư thì dữ liệu trên tất cả các đĩa còn lại sẽ không còn sử dụng được.

**Sử dụng lý tưởng:** RAID 0 lý tưởng cho việc lưu trữ dữ liệu không quan trọng cần được đọc / ghi ở tốc độ cao. Chẳng hạn như trên chỉnh sửa hình ảnh hoặc video.


**b. RAID 1**

RAID 1 – sử dụng kỹ thuật mirroring, tăng tốc độ đọc trong một số trường hợp. Và cung cấp khả năng chịu lỗi khi mất không quá một đĩa thành viên. Đây là RAID cơ bản nhất có khả năng đảm bảo an toàn dữ liệu. Cũng giống như RAID 0, thì RAID 1 cũng yêu cầu 2 ổ đĩa cứng để làm việc. Dữ liệu sẽ được ghi vào 2 ổ đĩa giống nhau (Mirroring) và nếu một ổ đĩa gặp trục trặc thì ổ đĩa còn lại vẫn làm việc và hoạt động bình thường.

![image](https://github.com/user-attachments/assets/63b23243-ca65-4b4a-b95c-bc3fa98095a1)

**Ưu điểm:** RAID 1 cung cấp tốc độ đọc tuyệt vời và tốc độ ghi có thể so sánh với tốc độ của một ổ đĩa duy nhất. Trong trường hợp một ổ đĩa bị lỗi, dữ liệu không cần phải được xây dựng lại. Chỉ cần sao chép chúng vào ổ đĩa drive thay thế.

**Nhược điểm:** Dung lượng lưu trữ hiệu quả chỉ bằng một nửa tổng dung lượng drive. Vì tất cả dữ liệu đều được ghi hai lần. Các giải pháp phần mềm RAID 1 không phải lúc nào cũng cho phép hoán đổi nhanh ở drive bị lỗi. Điều đó có nghĩa là drive bị lỗi chỉ có thể được thay thế sau khi tắt nguồn máy tính mà nó được gắn vào. Đối với các server được sử dụng đồng thời bởi nhiều người, điều này có thể không được chấp nhận. Các hệ thống như vậy thường sử dụng bộ điều khiển phần cứng hỗ trợ hoán đổi nhanh.

**Sử dụng lý tưởng:** RAID-1 lý tưởng cho nhiệm vụ lưu trữ quan trọng, chẳng hạn như cho các hệ thống kế toán. Nó cũng thích hợp cho các server nhỏ, trong đó chỉ có hai drive dữ liệu sẽ được sử dụng.

**c. RAID 5**

RAID 5 – sử dụng cả kỹ thuật phân stripe và parity. Cung cấp cải thiện tốc độ đọc như trong RAID 0 xấp xỉ, tồn tại khi mất một đĩa thành viên RAID. Có cơ chế khôi phục dũ liệu, các parity dùng để khổi phục dữ liệu được phân bổ đều trên tất cả các ổ cứng. RAID 5 yêu cầu tối thiểu 3 ổ cứng.

![image](https://github.com/user-attachments/assets/619f929f-3320-4ae6-8bba-2c435d15b246)

Ví dụ dữ liệu A được phân tách thành 3 phần A1, A2, A3, khi đó dữ liệu được chia thành 3 phần chứa trên các ổ đĩa cứng 0, 1, 2 (giống như RAID 0). Phần ổ đĩa cứng thứ 3 chứa Parity (Ap) của A1, A2, A3 để khôi phục dữ liệu có thể sẽ mất ở ổ đĩa cứng 0, 1, 2.

Dữ liệu B được chia thành B1 B2 B3 và Parity của nó là Bp, theo thứ tự B1 B2 B3 được lưu trữ tại ổ 0 1 3, và Bp được lưu trữ tại ổ 2. Các Parity được lưu trữ tuần tự trên các ổ đĩa cứng. RAID 5 cho phép tối đa có 1 ổ cứng bị chết tại một thời điểm, nếu có nhiều hơn 1 ổ cứng bị chết tại một thời điểm thì toàn bộ dữ liệu coi như mất hết. RAID 5 cũng yêu cầu các ổ cứng tham gia RAID phải có dung lượng bằng nhau.

Dung lượng cuối cùng RAID 5 được tính: (Dung lượng 1 ổ cứng) x [(Số lượng ổ cứng tham gia) – 1].

**Ưu điểm:** Các giao dịch dữ liệu đọc rất nhanh trong khi các giao dịch dữ liệu ghi có phần chậm hơn (do parity phải được tính toán). Nếu một drive bị lỗi, bạn vẫn có quyền truy cập vào tất cả dữ liệu. Ngay cả khi drive bị lỗi đang được thay thế và bộ điều khiển lưu trữ rebuild dữ liệu trên ổ đĩa mới.

**Nhược điểm:** Lỗi drive có ảnh hưởng đến thông lượng, mặc dù điều này vẫn có thể chấp nhận được. Đây là công nghệ phức tạp. Nếu một trong các đĩa trong mảng sử dụng đĩa 4TB bị lỗi và cần thay thế, việc khôi phục dữ liệu có thể mất một ngày hoặc lâu hơn. Việc này tùy thuộc vào load trên array và tốc độ của bộ điều khiển. Nếu một đĩa khác bị hỏng trong thời gian đó, dữ liệu sẽ bị mất vĩnh viễn.

**Sử dụng lý tưởng:** RAID 5 là một hệ thống toàn diện tốt, kết hợp khả năng lưu trữ hiệu quả với khả năng bảo mật tuyệt vời và hiệu suất tốt. Nó lý tưởng cho các server file và ứng dụng có số lượng ổ đĩa dữ liệu hạn chế.
