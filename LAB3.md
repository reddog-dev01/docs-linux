![image](https://github.com/user-attachments/assets/61fd2249-8787-4b8f-9368-a2e3f47e9752)

### **Các bước thực hiện lab**

**1. Tạo máy ảo ubuntu server**
![image](https://github.com/user-attachments/assets/6a18f2c3-aac7-4d6c-9a04-3f81c7264399)


**2. Tạo 2 disk cấu hình raid1**

![image](https://github.com/user-attachments/assets/837ecf00-6544-4340-8945-f3b0dbc6bdad)

Tạo các patition từ free space

![image](https://github.com/user-attachments/assets/22a6473f-81a7-43ee-b3bc-26835e5dc861)

tại đây chọn `unformatted` vì khi cấu hình RAID sẽ định dạng lại toàn bộ mảng (/dev/md0).
- Tương tự chia mỗi disk thành 3 patition với dung lượng là 1GB, 4GB, và còn lại
- 
![image](https://github.com/user-attachments/assets/644c1796-e14b-4f65-a142-9d0dd93deeb4)

- Tại phần này chọn các patition chia làm md0, md1, md2.

![image](https://github.com/user-attachments/assets/65417d75-81aa-40bc-bdc9-5e5182bb290b)

- Sau khi tạo thì mới format định dạng ổ là ext3 hoặc 4 hoặc ... và chọn phần 1GB mount `/boot`. 4G mount mount `SWAP`. phần còn lại mount `/`

![image](https://github.com/user-attachments/assets/1574a92a-e48e-41ad-8c79-111c6bf40320)

**Lý do làm như vậy**: 

chia làm 3 phân vùng làm việc `/` phân vùng chính chứa HĐH và các file cần thiết để chạy server (cấu hình với dung lượng lớn nhất), 

`/boot` chứa các file khởi động của HĐH (kernel, initial ramdisk) để đơn giản hóa quá trình khởi động, đảm bảo sự an toàn khi có sự cố, 

`swap` sử dụng như 1 phần mở rộng của RAM.
![image](https://github.com/user-attachments/assets/defe7eb5-64e9-46bf-af84-076641507dd3)

### **Lưu ý**:

**3. Tạo 2 disk cấu hình RAID0**

1. Cài mdadm nếu chưa có

Bước 1: Cài Đặt `mdadm`

```bash
sudo apt update
sudo apt install mdadm
```

Bước 2: Kiểm Tra Ổ Đĩa

```bash
sudo fdisk -l /dev/sdc /dev/sdd
```

Bước 3: Tạo Mảng RAID 0

```bash
sudo mdadm --create --verbose /dev/md3 --level=0 --raid-devices=2 /dev/sdc /dev/sdd
```

Trong đó:
- `--create /dev/md3`: Tạo mảng RAID mới và gán nó tới thiết bị ảo `/dev/md0`.
- `--verbose`: Hiển thị chi tiết quá trình thực hiện.
- `--level=0`: Thiết lập RAID level 0.
- `--raid-devices=2`: Số lượng ổ đĩa tham gia vào mảng RAID.
- `/dev/sdc /dev/sdd`: Đường dẫn đến các ổ đĩa được sử dụng.

Bước 4: Tạo File System

```bash
sudo mkfs.ext4 /dev/md0
```

### Bước 5: Gắn Kết Mảng RAID

```bash
sudo mkdir -p /mnt/raid0
sudo mount /dev/md3 /mnt/raid0
```

Bước 6: Cập Nhật `mdadm.conf`

```bash
sudo mdadm --detail --scan | sudo tee -a /etc/mdadm/mdadm.conf
```

### Bước 7: Cập Nhật `fstab`

Để tự động gắn kết mảng RAID khi khởi động, thêm dòng sau vào `/etc/fstab`:

```
sudo vim /etc/fstab
```
![image](https://github.com/user-attachments/assets/56550320-3c84-49e6-8666-1c5656983b7d)


### Bước 8: Kiểm Tra Mảng RAID

Sau cùng, kiểm tra trạng thái của mảng RAID:

```bash
cat /proc/mdstat
sudo mdadm --detail /dev/md0
```

**4. Tạo 2 disk cấu hình RAID1**

**Làm tương tự như RAID0**

**5. Đánh giá tốc độ**

**RAID0**

Bước 1: Cài đặt Sysbench

```bash
sudo apt update
sudo apt install sysbench
```

Bước 2: Chuẩn bị File cho Kiểm Tra

Đi vào thư mục `/mnt/raid0`, nơi mảng RAID 0 được gắn kết, và tạo các file kiểm tra. Lệnh này sẽ tạo ra một lượng file tạm thời để kiểm tra:

```bash
cd /mnt/raid0
sudo sysbench fileio --file-total-size=10G prepare
```

Trong đó, `--file-total-size=10G` là tổng kích thước file sẽ được tạo.

Bước 3: Thực Hiện Bài Kiểm Tra I/O

đọc ghi ngẫu nhiên
```bash
sudo sysbench fileio --file-total-size=10G --file-test-mode=rndrw --time=60 --max-requests=0 run
```

Tùy chọn:
- `--file-test-mode=rndrw` cho biết kiểm tra sẽ bao gồm đọc và ghi ngẫu nhiên.
- `--time=300` chỉ định thời gian kiểm tra là 300 giây.
- `--max-requests=0` cho phép kiểm tra chạy cho đến khi hết thời gian đã thiết lập mà không giới hạn số yêu cầu.
- `--file-num=16` chỉ định số lượng file sẽ được sử dụng cho bài kiểm tra.
- `--file-extra-flags=direct` sử dụng I/O trực tiếp để bỏ qua bộ nhớ đệm của hệ thống tập tin.
- `--threads=4` chỉ định số luồng sử dụng để thực hiện bài kiểm tra.

Bước 4: Dọn Dẹp Sau Kiểm Tra

Sau khi bài kiểm tra hoàn tất, bạn cần dọn dẹp các file tạm thời để không chiếm dụng không gian đĩa không cần thiết:

```bash
sysbench fileio --file-total-size=5G cleanup
```

** ĐỐI VỚI RAID1 VÀ DISK LÀM TƯƠNG TỰ**

**KẾT QUẢ**

raid0

![image](https://github.com/user-attachments/assets/d6115588-43de-43b5-9237-ce571e3f4303)

raid1

![image](https://github.com/user-attachments/assets/1295eb03-be10-4503-91e1-1f5d3960150f)

disk

![image](https://github.com/user-attachments/assets/58972d6d-eb9c-4088-86ea-81ee5bba959d)

