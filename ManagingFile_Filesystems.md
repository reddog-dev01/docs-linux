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
*a. Kiểm tra cơ bản*
```
sudo fsck /dev/...
```
*b. Kiểm tra mà không sửa lỗi*  
```
sudo fsck -n /dev/...
```
