### **Lab 2**

1. Sử dụng fdisk để chia thành 3 patition
```
sudo fdisk /dev/sdb
```
- Trong menu tìm kiếm ấn `n`
- Pattion type: `p` phân vùng chính, phân vùng độc lập, sử dụng bảng phân vùng MBR => tạo tối đa 4. `e` phân vùng mở rộng chỉ có thể tạo 1/1ổ đĩa, không chứa trực tiếp dữ liệu mà chứa các phân vùng logic, phân vùng logic hoạt động như phân vùng chính trong phân vùng mở rộng.
- Partitin number: số phân vùng (tối đa 4)
- First sector: mặc định 2048
- 
2. Định dạng patition
  ```
  sudo mkfs.ext4 /dev/sdb1
  #Tải công cụ quản lý xfs nếu chưa có
  sudo apt update
  sudo apt install xfsprogs
  sudo mkfs.xfs /dev/sdb2
  sudo mkfs.ext3 /dev/sdb3
  ```
  
3. Mount
 ```
sudo mkdir /mnt/data1 /mnt/data2 /mnt/data3
sudo mount /dev/sdb1 /mnt/data1 #2,3 tương tự
```

4. Reboot tự mount lại

*a. Cấu trúc /etc/fstab*

![image](https://github.com/user-attachments/assets/7eb85f8d-ad1e-4102-a934-f6a42bf776c8)
- file system: đường dẫn /dev/sda1, UUID=xxx-xxx-xxx, LABEL(LABEL=root_disk)
- mount point: điểm trong file system sẽ được gắn `/`, `/home`...
- type: loại file system trên patition (ext4, xfs...)
- options: `defaults` mặc định, `ro` chỉ đọc, `rw` đọc viết, `noexec` không cho phép thực thi các file
- dump: `0` không sao lưu, `1` sao lưu
- pass: `0` file system không được kiểm tra bởi `fsck`, `1` phân vùng gốc `/` được kiểm tra đầu tiên, `2` không phải phân vùng gốc được kiểm tra sau phân vùng gốc.

```
sudo vim /etc/fstab #phải cấp quyền để sửa file
```
thêm vào fstab và lưu lại
![image](https://github.com/user-attachments/assets/92f593c2-2ae3-4fde-a5d0-b88c8157b74a)
