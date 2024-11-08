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
```
- Gỡ cài đặt phần mềm:
  ``` bash
  sudo apt remove package_name      #gỡ bỏ phần mềm
  sudo apt auto remove              #xóa các package không cần thiết
  ```
  VD:
  ```bash
  sudo apt update
  sudo apt install vlc
  ```
#Cài đặt phần mềm từ tệp .deb (Debian Package)
- Cài đặt từ tệp .deb:
```bash
Copy code
sudo dpkg -i package_name.deb
sudo apt install -f  # Sửa lỗi và cài đặt các dependencies còn thiếu (nếu có)
```
VD: cài chrome
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt install -f
```
#Cài đặt phần mềm với Snap
- Cài snap:
```bash
sudo apt update
sudo apt install snapd
```
- Cài phần mềm:
```bash
sudo snap install package_name
```
- VD: cài tele
```bash
sudo snap install telegram
```
#Cài đặt phần mềm với Flatpak
- Cài đặt Flatpak
```bash
sudo apt install flatpak
```
- Thêm Flathub Repo (Kho ứng dụng flatpak chính)
```bash
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo
```
- Cài đặt phần mềm:
```bash
flatpak install flathub package_name
```
VD:
```bash
flatpak install flathub org.gimp.GIMP
```
#Cài đặt phần mềm
- Thêm PPA
```bash
sudo add-apt-repository ppa:user/ppa-name
sudo apt update
```
- Cài đặt phần mềm:
```bash
sudo apt install package_name
```
- VD: cài driver NVIDIA
```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
sudo apt update
sudo apt install nvidia-driver-460
```
#Cài đặt phần mềm từ mã nguồn (Source Code)
- Các bước cài đặt từ mã nguồn:
```
tar -xzf source_code.tar.gz   # Giải nén mã nguồn
cd source_code_directory      # Truy cập vào thư mục mã nguồn
./configure                   # Cấu hình trước khi biên dịch
make                          # Biên dịch mã nguồn
sudo make install             # Cài đặt phần mềm
```
- VD: cài mã nguồn từ htop
```
wget https://hisham.hm/htop/releases/2.2.0/htop-2.2.0.tar.gz
tar -xzf htop-2.2.0.tar.gz
cd htop-2.2.0
./configure
make
sudo make install
```
---------------------------------------------------------------------------------------------------
#Cách dùng các trình quản lý package
#dpkg
