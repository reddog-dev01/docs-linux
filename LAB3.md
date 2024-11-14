![image](https://github.com/user-attachments/assets/61fd2249-8787-4b8f-9368-a2e3f47e9752)

### **Các bước thực hiện lab**

**1. Tạo máy ảo ubuntu server**
![image](https://github.com/user-attachments/assets/0077df1b-912a-456a-ba55-b2ba48e2baaf)

**2. Tạo 2 disk cấu hình raid1**

![image](https://github.com/user-attachments/assets/837ecf00-6544-4340-8945-f3b0dbc6bdad)

Tạo các patition từ free space
![image](https://github.com/user-attachments/assets/22a6473f-81a7-43ee-b3bc-26835e5dc861)

tại đây chọn `unformatted` vì khi cấu hình RAID sẽ định dạng lại toàn bộ mảng (/dev/md0).
- Tương tự chia mỗi disk thành 3 patition với dung lượng là 1GB, 4GB, và còn lại
![image](https://github.com/user-attachments/assets/644c1796-e14b-4f65-a142-9d0dd93deeb4)
- Tại phần này chọn các patition chia làm md0, md1, md2.
- Sau khi tạo thì mới format định dạng ổ là ext3 hoặc 4 hoặc ... và chọn phần 1GB mount `/boot`. 4G mount mount `SWAP`. phần còn lại mount `/`

**Lý do làm như vậy**: 

chia làm 3 phân vùng làm việc `/` phân vùng chính chứa HĐH và các file cần thiết để chạy server (cấu hình với dung lượng lớn nhất), 

`/boot` chứa các file khởi động của HĐH (kernel, initial ramdisk) để đơn giản hóa quá trình khởi động, đảm bảo sự an toàn khi có sự cố, 

`swap` sử dụng như 1 phần mở rộng của RAM.
**3. Tạo 2 disk cấu hình RAID0**

