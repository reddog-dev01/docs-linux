#Khái niệm Linux và các Distro Linux

#Khái niệm

Linux coi tất cả các thiết bị phần cứng là dưới dạng như là 1 file. VD các thiết bị ổ cứng, USB, card mạng... đại diện bởi 1 file trong file systems (ext2, ext3, ext4, xfs, btrfs, f2fs, ntfs).
- ext2, ext3 cũ ít gặp
- ext4 hay gặp tại vì ổn định, hiệu suất phù hợp Ubuntu, Debian, Fedora.
- xfs hiệu xuất cao hỗ trợ tính năng snapshot qua hệ thống LVM. Sử dụng trong các hệ thống máy chủ cần quản lý tệp lớn và hiệu suất ghi cao. VD máy chủ CSDL, truyền thông, dữ liệu lớn.
- Btrfs (B-tree File System) cho phép tạo snapshot nhanh, có RAID tích hợp, tự động kiểm tra dữ liệu, cơ chế nén dư liệu, Clone and copy-on-write. Cũng như xfs nhưng ngon hơn là có RAID, đang trong quá trình phát triển.
- F2FS phù hợp để tích hợp các thiết bị lưu trữ flash như SSD và các thiết bị di động.
- NTFS phát triển bởi Microsoft dùng cho windows dùng tương tự ext4, xfs.

#Distro Linux

Distro (distribution) các bản phân phối hệ điêu hành Linux
- Ubuntu: người dùng cá nhân và doanh nghiệp, cloud do cộng đồng hỗ trợ lớn, có nhiều tài liệu hướng dẫn.
- Debian: cá nhân và doanh nghiệp cần một hệ thống ổn định do ít cập nhật nền tảng cho nhiều bản ubuntu.
- Fedora: Cho ai muốn trải nghiệm công nghệ mới, được Red Hat hỗ trợ.
- CentOS / AlmaLinux / Rocky Linux: hệ thống máy chủ và doanh nghiệp do ổn định và bảo mật cao.
- Arch Linux: Cho ai muốn tự cấu hình hệ thống.
- Linux Mint: Người dùng mới làm quen với Linux.
- Kali Linux: bảo mật, chuyên gia an ninh mạng, hắc cơ.
- Red Hat Enterprise Linux (RHEL): Doanh nghiệp và tổ chức lớn cần một hệ thống hỗ trợ chuyên nghiệp.
