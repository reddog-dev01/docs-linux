**1. Manage processes**    

**1.1 Package**  

- Tập hợp các file được đóng gói để cài đặt 1 chương trình, thư viện, tiện ích.

**a. Các thành phần chính của 1 package:**

- File cấu hình: Các file cấu hình mặc định hoặc yêu cầu cấu hình cho ứng dụng.
- Thư viện: Các thư viện cần thiết để chương trình hoạt động.
- Dependencies: Danh sách các gói khác cần thiết để gói này hoạt động đúng cách.
- Tài liệu: Có thể bao gồm hướng dẫn sử dụng, tài liệu API, hoặc các file README.
- 
**b. Các loại Package**
  
  1. DEB
     
  - Các file có định dạng `.deb`
  - Quản lý bởi APT và dpkg.
  2. Snap
    
  - 1 loại packgae độc lập
  - Các file có dạng `.snap`
  
  3. Flatpak
  - 1 loại package độc lập được phát triển bởi cộng đồng
  - thường được phân phối qua flathub
    
  4. Các loại khác
  - PPA, Tarball, Source, AppImage, DockerImages.
- Đơn giản hóa việc cài đặt, gỡ cài đặt, tăng cường bảo mật, giảm rác hệ thống, ổn định.  

**1.2 Dependencies (phụ thuộc)**    

- là các thư viện hoặc package mà 1 phần mềm cần để hoạt động đúng. Khi tải 1 phần mềm => Package Manager sẽ tự động tải và cài đặt các depandencies cần thiết.
- Các dependencies giúp phần mềm có thể tương tác với các thư viện hệ thống, mã hóa dữ liệu, nén file, hiển thị giao diện đồ họa.
- Cách Package Manager xử lý depencies: Các Package manager sẽ tự động tải về các package phụ thuộc khi cài 1 phần mềm (package phụ thuộc có thể là thư viện, công cụ dòng lệnh,
tiện ích cần thiết mà phần mềm yêu cầu hoạt động 1 cách ổn định).

VD: Apache2 có 1 số dependencies cần thiết:  
- lipapr1: Thư viện APR giúp Apache2 thương thích trên các HĐH
- libaprutil1: Thư viện hỗ trợ bổ sung cho APR với các tiện ích quản lý cấu hình và mã hóa
- libpcre3: Thư viện xử lý biểu thức chính quy để xử lý các mô hình URL và tìm kiếm
- libssl1.1: thư viện mã hóa SSL, cần thiết nếu chạy Apache với HTTPS.
- apache2-bin: Các tệp thực thi chính của Apache2, cần thiết để khởi động và chạy dịch vụ.
- 
VD: kiểm tra dependencies: `apt show apache2`   

**1.3 Binary package (gói nhị phân)**  
-  Binary package là tập hợp các file nhị phân, thư viện, và tài nguyên khác đã được biên dịch sẵn từ source packages.Có thể được cài đặt ngay lập tức mà không cần quá trình biên dịch.
- Các định dạng Binary Package: .deb, .rpm, snap và flatpak.

VD: cài đặt chrome
```
sudo apt install nginx 
```

**1.4 Repository (kho lưu trữ phần mềm)**
- Tập hợp (kho) các packages (gồm binary packages, source packages, và các tài nguyên liên quan) được lưu trữ trên các máy chủ trực tuyến, được quản lý bởi các nhà phát triển của hệ điều hành hoặc bên thứ ba.
- Chức năng của Repository: lưu trữ packages và tài nguyên liên quan (cấu hình, tài liệu), cung cấp các phiên bản ( ổn định, thử nghiệm, mới nhất), quản lý các dependencies
- Các loại Repository: Offcial Repository (Kho chính thức), Community Repository (Kho cộng đồng), Third-Party Repository (Kho của bên thứ ba), Personal Package Archives (PPA-chỉ có trên ubuntu và bản phối Debian)
- Các thành phần của một Repository: Matadata (thông tin về các package gồm package, phiên bản, mô tả, phụ thuộc, thông tin cần thiết khác), Package files (Các tệp nhị phân (.deb, .rpm ...) của từng phần mềm,
Release files (chứa thông tin về phiên bản, phân phối, trạng thái của kho)
- Cách hoạt động của Repository: Kết nối tới Repository => Tải Matadata => Cài đặt và quản lý phụ thuộc => Lưu trữ package đã cài.
- 
**1.5 Cách kiểm tra các Repository đang dùng**
  
  ```
  ls /etc/apt/sources.list.d/
  
``

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
  sudo apt install nginx
  ```
  
**b. Cài đặt phần mềm từ tệp .deb (Debian Package)**
- Cài đặt từ tệp .deb:  
```
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

- VD: cài spotify
  
```bash
sudo snap install spotify
```

Kiểm tra danh sách cài: `snap list`

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

**f. Cài đặt phần mềm từ mã nguồn (Source Code)**

- Các bước cài đặt từ mã nguồn:
```
tar -xzf source_code.tar.gz   #Giải nén mã nguồn
cd source_code_directory      #Truy cập vào thư mục mã nguồn
./configure                   #Cấu hình trước khi biên dịch
make                          #Biên dịch mã nguồn
sudo make install             #Cài đặt phần mềm
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
- Sử dụng khi muốn cập nhật các gói và đồng ý với việc hệ thống có thể thay đổi nhiều hơn, bao gồm cả những thay đổi lớn có thể cần để chuyển lên phiên bản mới của hệ điều hành hoặc khi cần các tính năng mới được bao gồm trong các bản cập nhật.
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
-  
----------------------------------------------------------------------------------------------------------------

**3. StartUp Script**  
- Các tập lệnh tự động chạy khi hệ thống khởi động hoặc khi người dùng đăng nhập vào hệ thống. Những script này thường được sử dụng để thiết lập môi trường, khởi động các dịch vụ quan trọng, hoặc thực hiện các công việc bảo trì cần thiết mà mình muốn thực hiện tự động khi hệ thống khởi động.
   
**#Cách để chạy 1 script mỗi khi server được bật**  

**3.1 Sử dụng `rc.local` Script**  
- File /etc/rc.local là một trong những phương pháp đơn giản nhất để chạy các lệnh khi hệ thống khởi động. File này sẽ được chạy với quyền root (quyền quản trị), cho phép thực thi các lệnh yêu cầu quyền cao.
  
**#Cách thực hiện**  
1. Mở file `rc.local`
```
sudo nano /etc/rc.local
```

2. Thêm lệnh để chạy script của bạn trước dòng `exit 0`:
```
/path/to/your_script.sh
exit 0
```

3. Đảm bảo file có quyền thực thi:
```
sudo chmod +x /etc/rc.local
```

4. Khởi động lại hệ thống để kiểm tra xem script có chạy khi khởi động không.

**Ví dụ**



**3.2 Sử dụng Systemd Service**
- Systemd là hệ thống quản lý dịch vụ trên hầu hết các bản phân phối Linux hiện đại (như Ubuntu, Debian, CentOS).  
**#Cách thực hiện**
  
1. Tạo một file dịch vụ trong `/etc/systemd/system/`:
```
sudo vim /etc/systemd/system/my_startup_script.service
```

2. Thêm nội dung cấu hình cho dịch vụ:
Dán nội dung sau vào file để định nghĩa dịch vụ:  
```
[Unit]
Description=My Startup Script
After=network.target

[Service]
ExecStart=/path/to/your_script.sh
Restart=on-failure
User=root  # Hoặc thay bằng tên người dùng nếu cần chạy với quyền của người dùng khác

[Install]
WantedBy=multi-user.target
```
- ExecStart: Đường dẫn tới script.
- After=network.target: Đảm bảo dịch vụ chạy sau khi mạng đã sẵn sàng (nếu script yêu cầu mạng).
- User: Đặt quyền người dùng để chạy script. Nếu bạn muốn script chạy dưới quyền root, giữ nguyên là root.
  
3. Kích hoạt dịch vụ để nó tự động chạy khi khởi động hệ thống:
```
sudo systemctl enable my_startup_script.service
```

4. Khởi động lại máy chủ để kiểm tra nếu dịch vụ tự động chạy.

5. Kiểm tra trạng thái dịch vụ để xác nhận rằng script đã được chạy thành công:
```
sudo systemctl status my_startup_script.service
```

**Ví dụ**

Bước 1: Tạo Script

1. *Tạo một script* để kiểm tra kết nối mạng và ghi kết quả vào tệp log. Gọi script là `network-check.sh` và lưu vào thư mục `/usr/local/bin/`:

   ```bash
   sudo vim /usr/local/bin/network-check.sh
   ```

2. *Thêm mã sau vào script*:
   ```bash
   #!/bin/bash
   # Script to check network connectivity

   if ping -c 1 8.8.8.8 &> /dev/null
   then
       echo "$(date): Network is up." >> /var/log/network-status.log
   else
       echo "$(date): Network is down." >> /var/log/network-status.log
   fi
   ```

3. *Cấp quyền thực thi cho script*:
   ```bash
   sudo chmod +x /usr/local/bin/network-check.sh
   ```

Bước 2: Tạo Systemd Service File

1. *Tạo một file service mới cho systemd*. Gọi là `network-check.service` và lưu vào `/etc/systemd/system`:
   ```bash
   sudo vim /etc/systemd/system/network-check.service
   ```

2. *Thêm nội dung sau vào file service*:
   ```ini
   [Unit]
   Description=Check network connectivity and log status
   Wants=network-online.target
   After=network-online.target

   [Service]
   Type=simple
   ExecStart=/usr/local/bin/network-check.sh
   Restart=on-failure

   [Install]
   WantedBy=multi-user.target
   ```

   - `Description`: Mô tả dịch vụ.
   - `Wants` và `After`: Đảm bảo rằng dịch vụ này sẽ chạy sau khi mạng được thiết lập.
   - `Type=simple`: Chỉ ra rằng nên chờ script chạy xong.
   - `ExecStart`: Lệnh để khởi chạy script.
   - `Restart`: Cấu hình tái khởi động dịch vụ khi có lỗi xảy ra.
   - `WantedBy`: Cho biết dịch vụ này sẽ được khởi động cùng với runlevel `multi-user.target`.

Bước 3: Kích hoạt và Khởi động Dịch vụ

1. *Kích hoạt dịch vụ* để nó tự động khởi động khi hệ thống boot:
   ```bash
   sudo systemctl enable network-check.service
   ```

2. *Khởi động dịch vụ*:
   ```bash
   sudo systemctl start network-check.service
   ```

3. *Kiểm tra trạng thái của dịch vụ** để đảm bảo nó đang hoạt động:
   ```bash
   sudo systemctl status network-check.service
   ```

**Kiểm tra log**
```
sudo less /var/log/network-status.log
```

**Cách tắt**
```
sudo systemctl disable [service-name].service
sudo systemctl stop [service-name].service
sudo systemctl stop network-check.service
```

**3.3 Sử dụng `crontab` với Tùy chọn `@reboot`**

**Cách thực hiện**

1. Mở `crontab` của người dùng hiện tại:
```
crontab -e
```

2. Thêm dòng sau vào cuối file `crontab`:
```
@reboot /path/to/your_script.sh
```

3. Lưu và thoát khỏi file crontab. Từ lần khởi động tiếp theo, script sẽ được chạy tự động.

**3.4 Cách sử dụng Init.d**

Dành cho các hệ thống không sử dụng systemd, sử dụng thư mục init.d là một cách phổ biến:

Tạo script mới trong /etc/init.d/:
```
sudo nano /etc/init.d/myscript
```
Dùng mẫu script sau:
```
#!/bin/sh
# /etc/init.d/myscript

case "$1" in
  start)
    /path/to/your/script.sh
    ;;
  stop)
    # Có thể thêm mã để dừng script ở đây
    ;;
  *)
    echo "Usage: /etc/init.d/myscript {start|stop}"
    exit 1
    ;;
esac

exit 0
```
Làm cho script có quyền thực thi:
```
sudo chmod +x /etc/init.d/myscript
```
Kích hoạt script:
```
sudo update-rc.d myscript defaults
```
