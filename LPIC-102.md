**1. Manage processes**    

**1.1 Package**  
- Tập hợp các tệp cần thiết để cài đặt và chạy 1 ứng dụng. Bao gồm tệp thực thi, thư viện, cấu hình, tài liệu.
- Các loại package chính: DEB, RPM, Tarball (TAR, TAR.GZ, TAR.BZ2)
- Đơn giản hóa việc cài đặt, gỡ cài đặt, tăng cường bảo mật, giảm rác hệ thống, ổn định.  

**1.2 Dependencies (phụ thuộc)**    
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

**1.3 Binary package (gói nhị phân)**  
- 1 loại package chứa các tệp đã được biên dịch sẵn (nghĩa là mã nguồn của phần mềm đã được chuyển thành tệp nhị phân mà HĐH có thể chạy trực tiếp)
- Gồm các tệp thực thi, thư viện, các tệp cấu hình cần thiết cho phần mềm hoạt động.
- Đặc điểm: Không cần biên dịch lại, phân phối dễ dàng, phụ thuộc vào kiến trúc hệ thống.
- Các định dạng Binary Package: .deb, .rpm, snap và flatpak.  
VD: cài đặt chrome
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
sudo apt install -f   # Cài đặt các dependencies còn thiếu nếu có  
```
**1.4 Repository (kho lưu trữ phần mềm)**
- Tập hợp các package phần mềm được lưu trữ trên các máy chủ trực tuyến, được quản lý bởi các nhà phát triển của hệ điều hành hoặc bên thứ ba.
- Nguồn chính để tải về và cài đặt các phần mềm, cập nhật, vá.
- Các loại Repository: Offcial Repository (Kho chính thức), Community Repository (Kho cộng đồng), Third-Party Repository (Kho của bên thứ ba), Personal Package Archives (PPA-chỉ có trên ubuntu và bản phối Debian)
- Các thành phần của một Repository: Matadata (thông tin về các package gồm package, phiên bản, mô tả, phụ thuộc, thông tin cần thiết khác), Package files (Các tệp nhị phân (.deb, .rpm ...) của từng phần mềm,
Release files (chứa thông tin về phiên bản, phân phối, trạng thái của kho)
- Cách hoạt động của Repository: Kết nối tới Repository => Tải Matadata => Cài đặt và quản lý phụ thuộc => Lưu trữ package đã cài.
**1.5 Cách kiểm tra các Repository đang dùng**  
**a. Ubuntu/Debian**  
- Liệt kê các repo hiện có: apt policy
**b. CentOS/Fedora**
- yum repolist
**c. DNF**
- dnf repolist
**1.6 Các cách cài phần mềm**
**a. Sử dụng APT (Advanced Package Tool)**
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
**b. Cài đặt phần mềm từ tệp .deb (Debian Package)**
- Cài đặt từ tệp .deb:  
```
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
**c. Cài đặt phần mềm với Snap**
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
**d. Cài đặt phần mềm với Flatpak**
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
**e. Cài đặt phần mềm**
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
**f. Cài đặt phần mềm từ mã nguồn (Source Code)**
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
**2. Cách dùng các trình quản lý package**  
**2.1 dpkg**  
**a. Cài đặt Package từ File .deb**  
```
sudo dpkg -i package_name.deb
```
VD: cài chrome
```
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

- Nếu trong quá trình cài đặt có lỗi phụ thuộc, có thể sử dụng lệnh apt để tự động cài đặt các phụ thuộc còn thiếu:
```
sudo apt install -f
```
**b. Gỡ cài đặt Package**  
```
sudo dpkg -r package_name
```
VD:  
```
sudo dpkg -r google-chrome-stable
```
**c. Gỡ cài đặt Oackage và xóa cấu hình (Purge)**  
```
sudo dpkg --purge package_name
```
VD: Gỡ hoàn toàn chrome
```
sudo dpkg --purge google-chrome-stable
```
**c. Liệt kê các package đã cài đặt**  
```
dpkg -l
```
- Tìm kiếm cụ thể
```
dpkg -l | grep package_name
```
**d. Kiểm tra trạng thái của một package**  
```
dpkg -s pack_name
```
VD:  
```
dpkg -s curl
```
**e. Hiển thị danh sách các file của 1 package đã cài đặt**  
```
dpkg -L package_name
```
VD: 
```
dpkg -L curl
```
**f. Tìm kiếm package đang sở hữu một file cụ thể**  
```
dpkg -S /path/to/file
```
VD:  
```
dpkg -S /usr/bin/curl
```
**g. Trích xuất File từ package .deb mà không cài đặt**
```
dpkg-deb -x package_name.deb /path/to/extract
```
VD: Trích xuất Google Chrome vào thư mục /tmp/chrome
```
dpkg-deb -x google-chrome-stable_current_amd64.deb /tmp/chrome
```
**h. Kiểm tra nội dung của Package .deb**
```
dpkg-deb -c package_name.deb
```
**k. Cấu hình lại tất cả package chưa cấu hình hoàn chỉnh**
```
sudo dpkg --configure -a
```
**2.2 apt-get**
**a. Cập nhật danh sách package ```apt-get update```**
- Tải về danh sách các package và phiên bản mới nhất từ các repository đã cấu hình trong hệ thống. Chạy lệnh này trước khi cài đặt hoặc cập nhật package để đảm bảo bạn có danh sách mới nhất
```
sudo apt-get update
```
**b. Nâng cấp các package ```apt-get upgrade```**
-  Nâng cấp tất cả các package đã cài đặt trên hệ thống lên phiên bản mới nhất, giữ nguyên các package hiện tại mà không cài thêm package mới
```
sudo apt-get upgrade
```
**c. Nâng cấp hệ thống toàn diện**
- Nâng cấp tất cả các package và sẽ cài đặt hoặc xóa các package cần thiết để hoàn tất việc nâng cấp hệ thống một cách toàn diện.
```
sudo apt-get dist-upgrade
```
**d. Cài đặt 1 package mới**
- tải về và cài đặt một package mới cùng với tất cả các phụ thuộc cần thiết từ repository.
```
sudo apt-get install package_name
```
VD: Cài đặt nginx
```
sudo apt-get install nginx
```
**e. Gỡ cài đặt package**
```
sudo apt-get remove package_name
```
VD: gỡ cài đặt nginx
```
sudo apt-get remove nginx
```
**f. Gỡ cài đặt hoàn toàn package (purge)**
- gỡ cài đặt package và đồng thời xóa luôn các tệp cấu hình liên quan
```
sudo apt-get purge package_name
```
VD: Gỡ hoàn toàn nginx
```
sudo apt-get purge nginx
```
**g. Tự động xóa các package không cần thiết**
- Gỡ bỏ các package không còn được sử dụng bởi bất kỳ package nào khác
```
sudo apt-get autoremove
```
**h. Tìm kiếm package**
```
apt-cache search package_name
``` 
VD: Tìm kiếm các package liên quan đến nginx
```
apt-cache search nginx
```
**i. Dọn dẹp Cache của package**
- Xóa các tệp `.deb` đã tải xuống trong thư mục `/var/cache/apt/archives`, giúp giải phóng không gian đĩa.
```
sudo apt-get clean
```
**j. Xóa Cache của Package Đã Cài Đặt**
```
sudo apt-get autoclean
```
**2.3 apt update và apt upgrade**
**a. apt update**
- có nhiệm vụ cập nhật danh sách các package và phiên bản mới nhất từ các kho lưu trữ (repository). Nó không cài đặt hay nâng cấp bất kỳ package nào, mà chỉ tải về thông tin mới nhất về các package để hệ thống biết đâu là phiên bản mới nhất có thể cài đặt.  
**#Khi nào cần dùng**
- Trước khi cài đặt bất kỳ package nào: Để đảm bảo rằng đang cài đặt phiên bản mới nhất của package, giúp tránh các sự cố hoặc xung đột do cài đặt các package lỗi thời.
- Trước khi chạy `apt upgrade` hoặc `apt full-upgrade`: Cập nhật danh sách package trước khi nâng cấp đảm bảo bạn đang cài đặt các phiên bản mới nhất.
- Sau khi thêm mới hoặc thay đổi repository: chạy apt update sẽ làm mới danh sách package, bao gồm các package từ repository mới.
- Định kỳ để cập nhật danh sách package:  để đảm bảo rằng hệ thống luôn có danh sách package mới nhất, đặc biệt là các bản vá bảo mật.
**b. apt upgrate**
- Dùng để nâng cấp tất cả các package đã cài đặt trên hệ thống lên phiên bản mới nhất có sẵn trong danh sách package hiện tại. Khi bạn chạy apt upgrade, nó sẽ cài đặt phiên bản mới cho tất cả các package đã cài đặt nhưng không cài đặt các **package phụ thuộc mới** hoặc **xóa các package hiện có**.  
**#Khi nào cần dùng**
- Sau khi chạy `apt update`: `apt upgrade` sẽ kiểm tra và nâng cấp các package lên phiên bản mới nhất, giúp hệ thống luôn cập nhật và bảo mật hơn.
- Khi muốn cập nhật các bản vá bảo mật và sửa lỗi: Nhiều bản cập nhật bao gồm các bản vá bảo mật và sửa lỗi cho các package đã cài đặt. Việc nâng cấp các package giúp bảo vệ hệ thống khỏi các lỗ hổng bảo mật.
- Định kỳ để đảm bảo hệ thống luôn cập nhật: Chạy `apt upgrade` một cách thường xuyên (hàng tuần hoặc hàng tháng) giúp hệ thống cập nhật và bảo mật hơn, giảm thiểu các rủi ro tiềm ẩn.
----------------------------------------------------------------------------------------------------------------
**3. StartUp Script**
