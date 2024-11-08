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

#Cách xem lịch sử của các lệnh đã gõ, đã thực hiện (history hoặc cat ~/.bash_history)

- Tìm kiếm lệnh cụ thể trong lịch sử: history | grep <từ khóa> <br>
  VD: history | grep ls
- Xem số lượng nhất định: history 10
- Thực thi lệnh gần nhất bắt đầu bằng 1 từ khóa: !<từ khóa> VD: !sudo
- để chạy 1 lệnh bất kì sử dụng: !<số> VD: !234
- chuỗi: !<chuỗi> VD: !ls
- lệnh cuối cùng: !!
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
- cung cấp đầu vào cho các thiết bị đầu cuối, ứng dụng, tiện ích. Thường kết nối với bàn phím.
- luồng đầu vào mà chương trình có thể đọc dữ liệu từ đó.
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
#Pipes (đường ống)
- | đường ống để gửi đầu ra đến lệnh mà không cần phải ghi vào 1 file trung gian khác VD: cat /var/log/messages | more <br>
#Redirection (chuyển hướng)  
- Quá trình lấy 1 luồng và gửi nó đến nơi khác (không phải mặc định) <br>
 '>' chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Tạo hoặc ghi đè đích nếu là một file VD: find /user -name "*.sh" > output.txt <br>
 '>>' chuyển hướng đầu ra tiêu chuẩn đến một file hoặc thiết bị. Nối thêm vào đích (cuối file) nếu là một file VD: find /user -name "*.sh" > output.txt <br>
 '<' chuyển hướng đầu vào tiêu chuẩn đến một chương trình VD: sort < /home/user/file.txt LƯU Ý: hành vi tương tự như khi sử dụng cat /home/user/file.txt | sort <br>  
2>: Chuyển hướng lỗi đến một file.  
 VD: command 2> error.log  
2>&1: Chuyển hướng stderr đến cùng một nơi như stdout.  
 VD: command > output.log 2>&1  
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
- Đánh số dòng có nội dung: cat -b file.txt  
#tac  
- cùng chức năng như cat nhưng hiển thị từ cuối lên đầu  
#sort  
- sắp xếp các dòng trong file
- sắp xếp giảm: sort -r
- sắp xếp theo cột: sort -k[#]
- sắp xếp bỏ qua chữ hoa, chữ thường: sort -f
- sắp xếp bỏ qua dòng trùng lặp: sort -u
- sắp xếp theo thứ tự số: sort -n
- chỉ định kí tự phân tách: sort -t VD: sort -t ',' -k 1 file.csv
#nl
- nl -ba đánh số dòng kể cả dòng trống
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
- -N: Hiển thị số dòng bên cạnh nội dung. VD: less -N filename.txt
- -S: Cắt các dòng dài thay vì xuống dòng, giúp bạn dễ dàng xem mà không bị phân tâm bởi việc xuống dòng. VD: less -S filename.txt
- -F: Tự động thoát nếu file đủ nhỏ để hiển thị trên một trang. VD: less -F filename.txt
- -X: Không xóa màn hình khi thoát, giữ lại nội dung trên màn hình. VD: less -X filename.txt
- SPACE: Di chuyển xuống một trang.
- b: Di chuyển lên một trang.
- ↑ hoặc ↓: Di chuyển lên hoặc xuống một dòng.
- g: Đi đến đầu file.
- G: Đi đến cuối file.
- nhấn g để quay lại đầu trang rồi <N>: Đi đến dòng số N (thay thế N bằng số dòng thực tế). VD g 300 enter
- /: Tìm kiếm xuống. Nhập từ khóa và nhấn Enter để tìm.
- ?: Tìm kiếm ngược. Nhập từ khóa và nhấn Enter.
- n: Chuyển đến kết quả tìm kiếm tiếp theo.
- N: Chuyển đến kết quả tìm kiếm trước đó.
- q: Thoát khỏi less. 
#cut  
- trích xuất dữ liệu trường hoặc cột từ một vị trí cụ thể trong file được chỉ định
- -c [#][-#] [filename] sẽ chỉ hiển thị cột (hoặc phạm vi cột) từ tệp được chỉ định VD: cut -c 1-3 text.txt là cắt 3 kí tự đầu của mỗi dòng
- -d[delimiter] thiết lập ký tự phân cách để sử dụng khi xử lý các trường (mặc định - TAB) VD: cut -d ':' -f 1 /etc/passwd GT: Lệnh này sử dụng dấu : làm dấu phân cách và chọn cột đầu tiên từ file /etc/passwd.
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
- ^: bắt đầu dòng VD: grep "^Helo" text.txt
- $: kết thúc dòng VD: grep "helo$" text.txt
- .: đại diện cho bất kì kí tự nào VD: grep "h...l" text.txt
- "*": số lượng kí tự trước '*' xuất hiện (có thể 0 hoặc nhiều kí tự) VD: grep "hel*o" text.txt (kết quả là heo, helo, hello)
- 
#sed  
- dùng để xử lý và thao tác văn bản. Đặc biệt là trong các tệp văn bản hoặc dòng đầu ra từ các lệnh khác. Cho phép các thao tác như tìm kiếm, thay thế, chèn, xóa dữ liệu trong văn bản.
- thay thế văn bản: sed 's/tim_kiem/thay_the/' filename
- thay thế toàn bộ xuất hiện trên mỗi dòng xuất hiện trên màn hình (không thay thế vào file): sed 's/tim_kiem/thay_the/g' file.txt
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
- h: Di chuyển sang trái một ký tự.
- j: Di chuyển xuống một dòng.
- k: Di chuyển lên một dòng.
- l: Di chuyển sang phải một ký tự.
- gg: Đi đến đầu file.
- G: Đi đến cuối file.
- 0: Đi đến đầu dòng.
- $: Đi đến cuối dòng..  
- Xóa một ký tự: Trong Normal Mode, nhấn x.
- Xóa một dòng: Trong Normal Mode, gõ dd.
- Sao chép một dòng: Trong Normal Mode, gõ yy.
- Dán: Trong Normal Mode, gõ p.
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
#tìm kiếm và thay thế
- :%s/old_word/new_word/g
#copy dòng bất kì
- 3yy hoặc 5yy số dòng + yy
#paste số lần tùy ý
- :let i=0 | while i < 1000 | put | let i=i+1 | endwhile
- :normal! 1000p
#den dòng bất bì
- :x (thay bằng số)
--------------------------------------------------------------------------------------------------------

#Text-based window manager and terminal multiplexer  
#byobu  
![image](https://github.com/user-attachments/assets/e485451f-4503-417c-9491-931dd7fa67ed)  
#cài tự dộng bật cùng terminal  
- byobu-enable
- https://superuser.com/questions/712413/how-to-load-byobu-automatically-when-terminal-started  
#lý do dùng byobu  
- quản lý nhiều phiên làm việc trên cùng 1 terminal
- duy trì phiên làm việc ngay cả khi bị mất kết nối SSH
- cung cấp thông tin hệ thống theo thời gian thực

-----------------------------------------------------------------------------------------------------------
#Quản lý tiến trình (Processes)  
#Command 'ps', 'top', 'htop'  
#top  
- time: thời gian thực.
- uptime: Hiển thị thời gian hệ thống đã chạy kể từ khi khởi động.
- users: Số lượng người dùng đang đăng nhập vào hệ thống.
- load average: Hiển thị mức tải của hệ thống trong thời gian khác nhau thường là 1, 5 và 15 phút gần nhất. Do số lượng tiến trình đang chờ CPU (gồm cả các tiến trình chờ truy cập vào tài nguyên I/O như ổ đĩa hoặc mạng). Tính theo số lõi CPU. VD: 4 lõi CPU => <4.0 là nhàn rỗi, không phải xử lý nhiều. =4.0 là mức tải tối ưu. Mỗi lõi có thể xử lý 1.0 đơn vị tải. >4.0 là quá tải, nhiều tiến trình chờ xử lý.  
- Tasks: Tổng số tiến trình đang chạy, bao gồm các tiến trình đang hoạt động (running), tạm dừng (sleeping), bị dừng (stopped), và bị zombie (zombie).  
  total: tổng số tiến trình hiện tại của hệ thống  
  running: tiến trình đang hoạt động và sử dụng CPU (số lượng tiến trình chạy cùng lúc thường bị giới hạn bởi số lượng lõi CPU)  
  sleeping: các tiến trình đang "ngủ" hoặc "chờ". không hoạt động trực tiếp trên CPU, chờ 1 đkiện nào đó để đánh thức. Hiện diện trong bộ nhớ  
  stopped: số lượng tiến trình đã dừng  
  zombie: tiến trình đã kết thúc nhưng chưa được dọn dẹp (không tiêu tốn tài nguyên CPU nhưng vẫn chiếm dụng 1 ID tiến trình PID)  
- %Cpu(s): Hiển thị phần trăm CPU đang được sử dụng bởi các thành phần sau:  
    us: Phần trăm CPU dành cho các tiến trình người dùng (user).  
    sy: Phần trăm CPU dành cho các tiến trình hệ thống (system).  
    ni: Phần trăm CPU dành cho các tiến trình ưu tiên (nice). Tức là các tiến trình mà người dùng đã thay đổi mức độ ưu tiên.  
    id: Phần trăm CPU nhàn rỗi (idle).  
    wa: Phần trăm CPU đang chờ hoạt động I/O (iowait).  
    hi: Phần trăm CPU dành cho xử lý các ngắt từ phần cứng (hardware interrupts).  
    si: Phần trăm CPU dành cho xử lý các ngắt từ phần mềm (software interrupts).    
    st: Phần trăm CPU bị đánh cắp bởi máy ảo (chỉ xuất hiện trong hệ thống ảo hóa). Thời lượng CPU bị chiếm bởi máy ảo khác và không có sẵn trong HĐH này.  
- Mem: Hiển thị thông tin về bộ nhớ RAM, bao gồm tổng dung lượng (total), dung lượng đang sử dụng (used), dung lượng trống (free), và dung lượng đang được cache (buff/cache).  
- Swap: Hiển thị thông tin về bộ nhớ swap với các cột tương tự như bộ nhớ RAM.  
- Chi tiết của từng tiến trình:
  PID: ID của tiến trình (Process ID).  
  USER: Tên người dùng sở hữu tiến trình.  
  PR: Độ ưu tiên của tiến trình (Priority). Số nhỏ hơn có độ ưu tiên cao hơn.  
  NI: Giá trị "nice" của tiến trình (mức độ ưu tiên thấp hơn).  
  VIRT: Dung lượng bộ nhớ ảo mà tiến trình sử dụng.  
  RES: Dung lượng bộ nhớ thực (RAM) mà tiến trình sử dụng.  
  SHR: Dung lượng bộ nhớ được chia sẻ với các tiến trình khác.  
  S: Trạng thái của tiến trình (R=running, S=sleeping, T=stopped, Z=zombie, D=Uninterruptible Sleep(Ngủ không thể gián đoạn lquan đến I/O), I(idle - nhàn rỗi)).  
  %CPU: Phần trăm CPU mà tiến trình đang sử dụng. VD: 6 lõi có thể lên 600%  
  %MEM: Phần trăm RAM mà tiến trình đang sử dụng.  
  TIME+: Thời gian CPU đã dành cho tiến trình (bao gồm giây và phần giây).  
  COMMAND: Tên lệnh hoặc chương trình chạy tiến trình.

  ![image](https://github.com/user-attachments/assets/83f3f496-220b-4e73-854b-1a3a80ce7799)
  - -d <tgian làm mới> VD: top -d 1
  - -u <username> hiển thị tiến trình của user
  - -p <pid> hiển thị thông tin của PID cụ thể VD: top -p 123 -p 345

#ps
- Liệt kê trạng thái tiến trình của từng tiến trình đang chạy trên hệ thống

![image](https://github.com/user-attachments/assets/53ee6fe3-b50c-4063-93b4-e5a8150d0ba1)
- -a hiển thị tất cả các quá trình đang chạy trên hệ thống, cho bất kỳ người dùng nào 
- -u hiển thị thông tin người dùng cho các tiến trình được hiển thị  
- -x hiển thị quá trình không có tty (terminal) kết nối  
- LƯU Ý: các tùy chọn này thường được sử dụng cùng nhau và có thể được sử dụng có hoặc không có ký tự - ở trước
#htop
- Danh sách tiến trình: 
  PID: ID của tiến trình.  
  USER: Người dùng sở hữu tiến trình.  
  PRI: Độ ưu tiên của tiến trình.  
  NI: Giá trị "nice" của tiến trình, liên quan đến độ ưu tiên.  
  VIRT: Bộ nhớ ảo tiến trình đang sử dụng.  
  RES: Bộ nhớ thực (RAM) mà tiến trình đang sử dụng.  
  SHR: Bộ nhớ được chia sẻ với các tiến trình khác.  
  S: Trạng thái của tiến trình (R=running, S=sleeping, T=stopped, Z=zombie).  
  CPU%: Phần trăm CPU tiến trình đang sử dụng.  
  MEM%: Phần trăm RAM tiến trình đang sử dụng.  
  TIME+: Thời gian CPU đã dành cho tiến trình.  
  COMMAND: Lệnh hoặc tên của tiến trình.
- Phím tắt:
![image](https://github.com/user-attachments/assets/fc97ead6-34fb-426c-a517-3142691eb4c2)
- Các tùy chọn tương tự top
#mức độ thân thiện
ps<top<htop  
![image](https://github.com/user-attachments/assets/3ba82938-aa08-4538-9647-223701adfaa3)  
  CPU Usage: Hiển thị mức sử dụng CPU dưới dạng phần trăm cho mỗi lõi (core) của CPU, thường được hiển thị với các màu sắc khác nhau:  
  Xanh lá: Tải hệ thống của các tiến trình người dùng không ưu tiên.  
  Xanh dương: Tải hệ thống của các tiến trình nhân hệ điều hành (kernel).  
  Vàng/Đỏ: Tải của các tiến trình ưu tiên thời gian thực (real-time) hoặc tải nặng hơn.  
  Xám: CPU nhàn rỗi (không sử dụng).  
  ![image](https://github.com/user-attachments/assets/5ea82988-ab8e-4227-a733-cdbb25fa20d2)  
Tasks: tổng số tác vụ (tiến trình) hiện đang tồn tại trên hệ thống  
thr: Tổng số luồng (threads) của tất cả các tiến trình. Mỗi tiến trình có thể bao gồm một hoặc nhiều luồng.  
kthr: Số luồng nhân hệ điều hành (kernel threads). Các luồng do kernel quản lý và hoạt động trong không gian nhân hệ điều hành, thường phục vụ cho các tác vụ hệ thống.  
running: Tiến trình đang thực sự chạy (sử dụng CPU) tại thời điểm đó.  
------------------------------------------------------------------------------------------------------------------

#Killing Processes
#signals
- những gì được gửi đến tiến trình và tiến trình sau đó phản ứng tương ứng  
  SIGHUP tín hiệu(signal) 1 tắt và khởi động lại tiến trình (hang up)    
  SIGINT tín hiệu 2 gián đoạn một tiến trình (CTL-C)   
  SIGKILL tín hiệu 9 kill tiến trình (không thể bị bỏ qua hoặc bắt được)    
  SIGTERM tín hiệu 15 kết thúc tiến trình (tiến trình có thể bỏ qua hoặc bắt được tín hiệu)    
  SIGSTOP tín hiệu 19 dừng tiến trình (không thể bị bỏ qua hoặc bắt được)    
  SIGTSTP tín hiệu 20 dừng terminal (CTL-Z)   
#kill
- kill <PID>  
  -1 (-HUP) tham chiếu đặc biệt để yêu cầu tiến trình khởi động lại
  -9 (-KILL) kill/stop/end/dump ngay lập tức (thường dùng để kill ngay cả một tiến trình zombie hoặc đang treo)  
#killall kill tất cả các phiên bản của tiến trình được đặt tên
#pkill kill các tiến trình dựa trên tên, ID, người dùng, phiên hoặc thiết bị đầu cuối (tty)
- LƯU Ý: nếu có nhiều tiêu chí được sử dụng, TẤT CẢ các tùy chọn phải khớp để áp dụng cho một tiến trình  
        -signal (hoặc --signal) [#] gửi số tín hiệu đến tiến trình khớp  
        -t [terminal] khớp với thiết bị đầu cuối/tty được chỉ định  
        -U (hoặc --uid) [user] khớp với ID người dùng    
--------------------------------------------------------------------------------------------------------------
