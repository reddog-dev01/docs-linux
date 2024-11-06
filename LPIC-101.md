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
 '>' chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Tạo hoặc ghi đè đích nếu là một file VD: find /user -name "*.sh" > output.txt <br>
 '>>' chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Nối thêm vào đích (cuối file) nếu là một file VD: find /user -name "*.sh" > output.txt <br>
 '<' chuyển hướng đầu vào tiêu chuẩn đến một chương trình VD: sort < /home/user/file.txt LƯU Ý: hành vi tương tự như khi sử dụng cat /home/user/file.txt | sort <br>
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

#Processing Text (Các lệnh liên quan xem tập tin văn bản)
#cat
- hiển thị nội dung của 1 tập tin
- có thể nối nội dung của nhiều tập VD: cat file1.txt file2.txt
- Tạo 1 file nhập nội dung từ bàn phím VD: cat > file.txt
- Thêm nội dung vào file có sẵn VD: cat >> file.txt sử dụng Ctrl +D để kết thúc. Các lệnh này có thể kết hợp.
- Đánh số dòng: cat -n file.txt
- Đánh số dòng trống: cat -b file.txt
#tac
- cùng chức năng như cat nhưng hiển thị từ cuối lên đầu
#sort
- sắp xếp các dòng trong file
- sắp xếp giảm: sort -r
- sắp xếp theo cột: sort -k
- sắp xếp bỏ qua chữ hoa, chữ thường: sort -f
- sắp xếp bỏ qua dòng trùng lặp: sort -u
- sắp xếp theo thứ tự số: sort -n
#split
- chia 1 file thành nhiều file lẻ
- -a [#] khi tạo các file chia, đặt tên chúng là 'x#' VD: -a 5 tạo ra file 'xaaaaa'
- -b [#][b/k/m] file mới chứa số lượng byte/kilobyte/megabyte được chỉ định
- '- [#]' files mới chứa số lượng byte hoặc dòng được chỉ định
- -l [#] files mới chứa số lượng dòng được chỉ định
#uniq
- cho phép trích xuất chỉ các dòng dữ liệu 'duy nhất' từ file
- Áp dụng sắp xếp vào file trước khi chạy lệnh này (đặc biệt là các file lớn)
- -u [filename] chỉ in ra các dòng duy nhất trong file
- -d [filename] in ra ví dụ của mỗi dòng bị lặp lại trong file
- -D [filename] in ra TẤT CẢ các trường hợp của các dòng bị lặp lại trong file
#head
- Tương tự như lệnh cat vì nó sẽ hiển thị nội dung của một file, nhưng chỉ hiển thị một số dòng nhất định từ đầu (mặc định là 10)
- -n [#] [filename] hiển thị số dòng, bắt đầu từ đầu, của tệp được chỉ định
#tail
- hiển thị một số dòng nhất định từ cuối file (mặc định 10)
- -n [#] [filename] - hiển thị số dòng, bắt đầu từ cuối, của file được chỉ định
- -f [filename] - hiển thị bất kỳ dòng mới nào được thêm vào file sau khi bạn đã chạy lệnh VD: tail -n 10 -f /var/log/syslog
#less
- Cho phép xem file nhưng hữu ích hơn cat
- space di chuyển đến màn hình tiếp theo
- q thoát
#cut
- trích xuất dữ liệu trường hoặc cột từ một vị trí cụ thể trong file được chỉ định
- -c [#][-#] [filename] sẽ chỉ hiển thị cột (hoặc phạm vi cột) từ tệp được chỉ định
- -d[delimiter] thiết lập ký tự phân cách để sử dụng khi xử lý các trường (mặc định - TAB)
- -f [field1[,field2[,field3]]] [filename] xác định số trường (được xác định bằng ký tự phân cách) để hiển thị từ file được chỉ định
#wc
- -l là đếm số dòng
- -w là đếm số từ
- -c số ký tự (byte)
- sử dụng như 1 lệnh bổ sung của lệnh khác VD cat /etc/passwd | wc -l
#grep
- Dùng để tìm kiếm chuỗi trong file, luồng, thư mục.
- -i tìm kiếm không phân biệt chữ hoa, chữ thường
- -v hiển thị các dòng không chứa từ khóa
- -n hiển thị số dòng chứa từ khóa
- -c đếm số dòng chứa từ khóa
- -w tìm kiếm chính xác từ khóa tức là chỉ khớp các dòng chứa toàn bộ chuỗi hoặc cụm từ
- -A hiển thị thêm 1 số dòng sau dòng khớp VD: grep -i -A 3 "fail" text.txt
- -B hiển thị thêm 1 số dòng trước dòng khớp
- -C hiển thị thêm 1 số dòng cả trước và sau dòng khớp
- -l Chỉ hiển thị tên file chứa từ khóa VD: grep -l "word" *.txt
- -L chỉ hiển thị tên file không chứa từ khóa
- -E sử dụng biển thức chính quy mở rộng VD: grep -E "^word|^fail" text.txt
#sed
- dùng để xử lý và thao tác văn bản. Đặc biệt là trong các tệp văn bản hoặc dòng đầu ra từ các lệnh khác. Cho phép các thao tác như tìm kiếm, thay thế, chèn, xóa dữ liệu trong văn bản.
- thay thế văn bản: sed 's/tim_kiem/thay_the/' filename
- thay thế toàn bộ xuất hiện trên mỗi dòng: sed 's/tim_kiem/thay_the/g' file.txt
- thay thế trực tiếp trong file: sed -i 's/tim_kiem/thay_the/g' file.txt
- sed '/chuoi_xoa/d' file.txt
- xóa 1 dòng cụ thể hoặc nhiều dòng sed '2,3d' file.txt
- p in ra dòng khớp với biểu thức tìm kiếm
- i\text chèn dòng text trước dòng được chỉ định
- a\text chèn dòng text sau dòng được chỉ định
#awk
- dùng phân tích văn bản, thường được sử dụng để trích xuất, định dạng và xử lý dữ liệu từ các file văn bản hoặc đầu ra của các lệnh khác.
- {print $0} in toàn bộ dòng
- {print $1, $3} in cột 1 và cột 3
- $2 == "hello" điều kiện khớp nếu cột 2 là "hello"
- -F ":" đặt dấu phân cách trường là dấu hai chấm
- BEGIN{...} thực thi lệnh trước khi đọc file
- END{...} thực thi lệnh sau khi đọc file

-----------------------------------------------------------------------------------------------------
#Editor File
#Cách sử dụng vim
#normal mode: mặc định
- h, j, k, l Di chuyển sang trái, xuống, lên, phải (tương đương với các phím mũi tên).
- w Nhảy đến đầu từ tiếp theo.
- b Nhảy đến đầu từ trước đó.
- 0 Nhảy đến đầu dòng hiện tại.
- $ Nhảy đến cuối dòng.
- yy Sao chép một dòng.
- dd Xóa một dòng.
- p Dán văn bản.

#insert mode: nhập chỉnh sửa văn bản
- Nhấn i Chèn từ vị trí con trỏ hiện tại.
- Nhấn I Chèn ở đầu dòng hiện tại.
- Nhấn a Chèn sau vị trí con trỏ hiện tại.
- Nhấn A Chèn ở cuối dòng hiện tại.
- Nhấn o Tạo dòng mới phía dưới dòng hiện tại và chuyển vào chế độ Insert.
- Nhấn O Tạo dòng mới phía trên dòng hiện tại và chuyển vào chế độ Insert.
#visual mode: cho phép bôi đen để copy, xóa, thay thế
- Nhấn v Bắt đầu chọn ký tự.
- Nhấn V Chọn toàn bộ dòng.
- Nhấn Ctrl + v Chế độ Visual Block (chọn theo khối hình chữ nhật).
#command-line mode 
- Nhấn : Mở dòng lệnh để nhập lệnh.
- Nhấn / Tìm kiếm theo từ khóa.
- Nhấn ? Tìm kiếm ngược theo từ khóa.
#replace mode
- Nhấn R trong chế độ Normal để vào chế độ Replace
#select mode
- Nhấn gh để chuyển vào chế độ Select từ chế độ Normal (có thể không được hỗ trợ trên một số bản Vim).
#Ex mode
- Nhấn Q từ chế độ Normal để vào Ex Mode.
--------------------------------------------------------------------------------------------------------

#Text-based window manager and terminal multiplexer
#byobu
![image](https://github.com/user-attachments/assets/e485451f-4503-417c-9491-931dd7fa67ed)
#cài tự dộng bật cùng terminal
byobu-enable
https://superuser.com/questions/712413/how-to-load-byobu-automatically-when-terminal-started

#Kiến thức hệ thống
#Cài đặt và quản lý gói
#Lệnh GNU và Unix
#Thiết bị, hệ thống tập tin và tiêu chuẩn hệ thống tập tin (Devices, Linux Filesystems)
