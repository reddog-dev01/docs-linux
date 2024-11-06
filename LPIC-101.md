#Cách thay đổi thư mục làm việc (cd)  

- Có thể sử dụng đường dẫn tuyệt đối, đường dẫn tương đối hoặc giá trị trong biến làm phần của đường dẫn.
- VD: cd /home/user/Documents (đường dẫn tuyệt đối là bắt đầu từ thư mục gốc) hoặc cd Documents (đường dẫn tương đối là bắt đầu từ thư mục hiện tại)
- Trở về thư mục gốc (home directory): cd ~ hoặc cd
- Quay về thư mục trước đó vừa ở: cd -
- Di chuyển đến thư mục cha: cd .. hoặc 2 cấp: cd ../..
- Di chuyển đến thư mục root(/): cd /
  
  ~ đại diện thư mục gốc của người dùng hiện tại <br>
  . đại diện đại diện cho thư mục hiện tại  
  .. đại diện cho thư mục cha của thư mục hiện tại
  
- LƯU Ý: để đến thư mục gốc của mình dùng cd~ nhưng đến như mục gốc người khác dùng cd~user

--------------------------------------------------------------------------------------

#Cách xem thư mục đang làm việc (pwd)

-------------------------------------------------------------------------------------------

#Cách xem lịch sử của các lệnh đã gõ, đã thực hiện (history hoặc cat ~./bash_history)

- Tìm kiếm lệnh cụ thể trong lịch sử: history | grep <từ khóa> <br>
  VD: history | grep ls
- Xem số lượng nhất định: history 10
- Thực thi lệnh gần nhất bắt đầu bằng 1 từ khóa: !<từ khóa> VD: !sudo
- Ctrl + R tìm kiếm lệnh gần nhất với từ khóa nhập sử dụng mũi tên lên xuống để chuyển đổi qua lại <br>
  VD: Ctrl + R nhập 'sudo' hệ thống chạy lệnh gần nhất có chưa 'sudo'. Có thể sử dụng mũi tên sang phải để chỉnh sửa lệnh đó.
- Ctrl + G để thoát chế độ tìm kiếm "reverse-i-search" (Ctrl + R)
- Ctrl + U xóa từ đầu dòng đến con trỏ
- Ctrl + K xóa từ con trỏ đến cuối dòng <br>
LƯU Ý: xóa toàn bộ lịch sử: history -c hoặc rm ~/.bash_history <br>
       xóa 1 dòng cụ thể history -d 25
-----------------------------------------------------------------------------------------

#Các phím tắt trong terminal

- Ctrl + S tạm dừng đầu ra terminal
- Ctrl + Q tiếp tục đầu ra terminal
- còn nữa

----------------------------------------------------------------------------------------------------

#Getting help
#Cách sử dụng lệnh man (manual)
- Sử dụng để hiển thị tài liệu hướng dẫn chi tiết lệnh, file cầu hình, chương trình khác.
- Cú pháp: man [ten_lenh] VD: man cat 
- Xem 1 phần cụ thể: man [so_phan] [ten_phan] VD: man 5 passwd
- Tìm kiếm 1 từ khóa trong các trang man: man -k [tu_khoa] hoặc apropos [tu_khoa]
- Hiển thị đường dẫn đầy đủ của trang man: man -w [ten_len] VD: man -w cat

--------------------------------------------------------------------------------------------------

#Using streams, Redirection, Pipes
#Cách sử dụng luồng, ống, chuyển hướng
#Streams
#Standard input (luồng đầu vào tiêu chuẩn)
- cung cấp đầu vào cho các thiết bị đầu cuối, ứng dụng, tiện ích.
- Kí hiệu: "stdin" thường đại diện bởi số 0
- /dev/stdin
- chỉ số file 0. file /proc/self/fd/0
#Standard output (luồng đầu ra tiêu chuẩn)
-  cung cấp đầu ra cho các thiết bị đầu cuối, ứng dụng, tiện ích.
-  /dev/stdout
-  chỉ số file 1. file /proc/self/fd/1
#Standard error (luồng lỗi tiêu chuẩn)
- Thông báo lỗi đến các thiết bị đầu cuối, ứng dụng, tiện ích  coi như tập coi của tập ra.
- /dev/stderr
- chỉ số file 2. file /proc/self/fd/2
#Redirection (chuyển hướng)
- Quá trình lấy 1 luồng và gửi nó đến nơi khác (không phải mặc định) <br>
| đường ống để gửi đầu ra đến lệnh khác VD: cat /var/log/messages | more <br>
> chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Tạo hoặc ghi đè đích nếu là một file VD: find /user -name "*.sh" > output.txt <br>
>> chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Nối thêm vào đích (cuối file) nếu là một file VD: find /user -name "*.sh" > output.txt <br>
< chuyển hướng đầu vào tiêu chuẩn đến một chương trình VD: sort < /home/user/file.txt LƯU Ý: hành vi tương tự như khi sử dụng cat /home/user/file.txt | sort <br>
#Redirecting standard error (chuyển hướng luồng lỗi)
- stderr thường được chuyển đến log hoặc /dev/null
- Cho phép xóa lỗi từ đầu ra tiêu chuẩn bình thường VD: find / -iname "*.sh" 2> /dev/null hiển thị mà không thông báo lỗi liên quan quyền hạn.
#Kết hợp chuyển hướng
- VD: find / -iname "*.sh" 2> /dev/null > output.txt => dữ liệu đưa vào file txt thay vì in ra màn hình
- VD: sort < listfile | nl
#tee
- Nhận luồng đầu vào tiêu chuẩn và gửi một luồng đầu ra (giống nhau) đến một file được chỉ định
- sử dụng khi muốn thu thập đầu ra của một ứng dụng nhưng cũng cần nhìn thấy kết quả trên màn hình
- VD: find / -name "*.sh" | tee name.txt
#xargs
- nhận 1 luồng đầu vào (kqua của lệnh khác thường là find) sau đó đẩy vào 1 file khác theo yêu cầu.
- VD: find / -name "*.sh" | xargs ls -al > myresults.txt

--------------------------------------------------------------------------------------------------------------------------------


#Kiến thức hệ thống
#Cài đặt và quản lý gói
#Lệnh GNU và Unix
#Thiết bị, hệ thống tập tin và tiêu chuẩn hệ thống tập tin (Devices, Linux Filesystems)
