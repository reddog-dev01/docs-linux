#Manage processes  

#Package  
- Tập hợp các tệp cần thiết để cài đặt và chạy 1 ứng dụng. Bao gồm tệp thực thi, thư viện, cấu hình, tài liệu.
- Các loại package chính: DEB, RPM, Tarball (TAR, TAR.GZ, TAR.BZ2)
- Đơn giản hóa việc cài đặt, gỡ cài đặt, tăng cường bảo mật, giảm rác hệ thống, ổn định.  

#Dependencies (phụ thuộc)  
- là các thư viện hoặc package mà 1 phần mềm cần để hoạt đông đúng. Khi tải 1 phần mềm => Package Manager sẽ tự động tải và cài đặt các depandencies cần thiết.
- Các dependencies giúp phần mềm có thể tương tác với các thư viện hệ thống, mã hóa dữ liệu, nén file, hiển thị giao diện đồ họa.
- Cách Package Manager xử lý depencies: Các Package manager sẽ tự động tải về các package phụ thuộc khi cài 1 phần mềm (package phụ thuộc có thể là thư viện, công cụ dòng lệnh,
tiện tích cần thiết mà phần mềm yêu cầu hoạt động 1 cách ổn định).  
VD: Apache2 có 1 số dependencies cần thiết:  
- lipapr1: Thư viện APR giúp Apache2 thương thích trên các HĐH
- libaprutil1: Thư viện hỗ trợ bổ sung cho APR với các tiện ích quản lý cấu hình và mã hóa
- libpcre3: Thư viện xử lý biểu thức chính quy để xử lý các mô hình URL và tìm kiếm
- libssl1.1: thư viện mã hóa SSL, cần thiết nếu chạy Apache với HTTPS.
- apache2-bin: Các tệp thực thi chính của Apache2, cần thiết để khởi động và chạy dịch vụ.  
VD: kiểm tra dependencies: apt-cache depends apache2    

#Binary package (gói nhị phân)  
- 1 loại package chứa các tệp đã được biên dịch sẵn (nghĩa là mã nguồn của phần mềm đã được chuyển thành tệp nhị phân mà HĐH có thể chạy trực tiếp)
- Gồm các tệp thực thi, thư viện, các tệp cấu hình cần thiết cho phần mềm hoạt động.
- Đặc điểm: Không cần biên dịch lại, phân phối dễ dàng, phụ thuộc vào kiến trúc hệ thống.
- Các định dạng Binary Package: .deb, .rpm, snap và flatpak.  
VD: cài đặt chrome  
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt install -f   # Cài đặt các dependencies còn thiếu nếu có  

#Repository (kho lưu trữ phần mềm)
- Tập hợp các package phần mềm được lưu trữ trên các máy chủ trực tuyến, được quản lý bởi các nhà phát triển của hệ điều hành hoặc bên thứ ba.
- Nguồn chính để tải về và cài đặt các phần mềm, cập nhật, vá.
- Các loại Repository: Offcial Repository (Kho chính thức), Community Repository (Kho cộng đồng), Third-Party Repository (Kho của bên thứ ba), Personal Package Archives (PPA-chỉ có trên ubuntu và bản phối Debian)
- Các thành phần của một Repository: Matadata (thông tin về các package gồm package, phiên bản, mô tả, phụ thuộc, thông tin cần thiết khác), Package files (Các tệp nhị phân (.deb, .rpm ...) của từng phần mềm,
Release files (chứa thông tin về phiên bản, phân phối, trạng thái của kho)
- Cách hoạt động của Repository: Kết nối tới Repository => Tải Matadata => Cài đặt và quản lý phụ thuộc => Lưu trữ package đã cài.
#Cách kiểm tra các Repository đang dùng  
#Ubuntu/Debian  
- Liệt kê các repo hiện có: apt policy
#CentOS/Fedora
- yum repolist
#DNF
- dnf repolist
#Các cách cài phần mềm
#Sử dụng APT (Advanced Package Tool)
- Cài đặt phần mềm:  
```bash
  sudo apt update
  sudo apt install package_name

