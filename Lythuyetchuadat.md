**1.Using Streams**  
  
**1.1 Standard Input (stdin)**
- Sử dụng bởi các chương trình hoặc lệnh để nhập dữ liệu đầu vào từ người dùng hoặc từ nguồn khác (tệp).
- Mặc đinh dữ liệu nhập qua stdin đến từ bàn phím.  
*Nhập từ bàn phím:* Nếu 1 chương trình đọc từ stdin và không có dữ liệu nào được chuyển hướng, nó sẽ đợi người dùng nhập dữ liệu từ bàn phím.
*Chuyển hướng stdin từ 1 tệp:* Đọc dữ liệu từ 1 tệp thay vì bàn phím
  VD:
  ```
  cat < file.txt
  ```
*Sử dụng pipe để truyền stdin:* chuyển stdout của 1 lệnh làm đầu vào stdin của cho lệnh khác.

**1.2 Standard Output (stdout)**
- Hiển thị kết quả hoặc dữ liệu đầu ra của chương trình. Mặc định stdout sẽ hiển thị trên màn hình terminal, nhưng có thể chuyển hướng đầu ra này sang 1 tệp hoặc 1 lệnh khác.

**1.3 Standard Error**
- Sử dụng để hiển thị các thông báo lỗi của chương trình hoặc lệnh. Mặc định sẽ hiển thị ra terminal, nhưng cũng có thể chuyển hướng stderr độc lập với stdout để xử lý lỗi riêng biệt mà không ảnh hưởng đến dữ liệu hoặc kết quả. Tức là stderr 1 file riêng, stdout 1 file riêng.  
  
**2. Pipe, Redirection**  
**2.1 Pipe `(|)`**  
- chuyển stdout của 1 lệnh thành stdin của lệnh khác. Giúp xử lý dữ liệu 1 cách liên tục không cần lưu vào file trung gian.
  
**2.2 Redirection**  
**a. `>`**  
- Ghi đầu ra của 1 lệnh vào file
- Tạo mới file nếu chưa tồn tại
- Ghi đè nội dung file nếu đã tồn tại  
**b. `>>`**  
- Ghi nội dung vào cuối file (không mất nội dung cũ)
- Tạo mới file nếu chưa tồn tại  
**c. `<`**  
- Đưa nội dung của 1 tệp và stdin cho 1 lệnh
- Thay thế việc nhập dữ liệu thủ công từ bàn phím  
VD:
```
cat < text.txt
```
  
**3. Tác dụng less**
- Hiển thị nội dung tệp từng phần.
- Cuộn hoặc tìm kiếm trong nội dung tệp.
- Tiết kiệm tài nguyên vì không tải toàn bộ tệp vào bộ nhớ.
- Hỗ trợ đọc dữ liệu từ tệp, lệnh, hoặc stdin.
  
**4. Byobu**
- Tách phiên làm việc để chạy ngầm: `Ctrl A` rồi `D` hoặc dùng F6
- Kiểm tra danh sách phiên làm việc:
```
byobu list-sessions
```
- Kết nối lại
```
byobu attach-session -t <session_name or ID>
```
**5. Top**  
**5.1 Thời gian hiện tại**: Được lấy từ system oclock tính theo system timezone được cấu hình trên server.  
**5.2 Uptime**  
- Khoảng thời gian mà server đã hoạt động liên tục kể từ lần khởi động gần nhất => reboot uptime sẽ về 0
- Đo lường độ ổn định của hệ thống và cho biết thời gian máy đã chạy mà không gặp sự cố hoặc cần phải khởi động lại.  
**5.3 Loadavg**
- Mỗi tiến trình đang chạy hoặc chờ đợi cpu xử lý sẽ add giá trị 1 vào load.
- Loadavg thể hiện tải trung bình của hệ thống qua mỗi đoạn thời gian: cho thấy trung bình có bao nhiều process mà server phải thực hiện.
- Loadavg cho ta thấy được trung bình khối lượng công việc hệ thống phải xử lý trong mỗi khoảng thời gian: 1 phút, 5 phút và 15 phút.  
**5.4 %Cpu(s)**  
**a. `us` (User Space)**  
Thời gian CPU dành cho các tiến trình người dùng, như ứng dụng, phần mềm đang chạy.  
Giá trị cao ở đây cho thấy CPU đang được sử dụng bởi các ứng dụng hoặc dịch vụ.  
**b. `sy` (System)**  
- Thời gian CPU dành cho các tiến trình hệ thống, hoạt động trong không gian kernel.
- Giá trị cao ở đây có thể chỉ ra rằng hệ thống đang xử lý nhiều tác vụ hệ thống, chẳng hạn như quản lý tài nguyên hoặc điều khiển thiết bị phần cứng.  
**c. `wa` (I/O Wait)**  
- Thời gian CPU chờ hoàn thành các tác vụ I/O, chẳng hạn như đọc hoặc ghi dữ liệu vào đĩa.
- Giá trị cao ở đây thường báo hiệu vấn đề về hiệu suất I/O (thiết bị ngoại vi, lưu trữ dữ liệu)  
**d. `hi` (Hardware Interrupts)**  
- Thời gian CPU dành để xử lý các ngắt phần cứng (ví dụ: xử lý tín hiệu từ card mạng, ổ đĩa, v.v.).  
**e. `si` (Software Interrupts)**  
- Thời gian CPU dành để xử lý các ngắt phần mềm, chẳng hạn như các dịch vụ hệ thống hoặc thông điệp giữa các tiến trình.  
**f. `st` (Steal Time)**  
- Chỉ xuất hiện khi chạy trong môi trường ảo hóa.
- Đây là thời gian CPU bị hypervisor sử dụng để chạy các tác vụ khác ngoài hệ điều hành hiện tại.
- Giá trị cao ở đây có thể chỉ ra rằng tài nguyên CPU bị hạn chế trong môi trường ảo hóa.  
**5.5 Mem**  
- *total:* bộ nhớ vật lý được cài đặt trên hệ thống.
- *used:* RAM được sử dụng bởi các tiến trình và ứng dụng.
- *free:* Bộ nhớ thực sự nhàn rỗi, không bị tiến trình hoặc hệ thống chiếm dụng.
- *buff/cache:* Buffer: Bộ nhớ tạm trước khi dữ liệu được ghi vào đĩa.  S
                Cache: Lưu trữ dữ liệu đã đọc từ đĩa để tăng tốc độ truy xuất.    
**5.6 Swap**
- Một không gian trên ổ đĩa (hoặc thiết bị lưu trữ) được hệ điều hành sử dụng như bộ nhớ RAM bổ sung khi hệ thống hết RAM vật lý. Swap cho phép hệ thống tiếp tục hoạt động ngay cả khi RAM đã đầy, tuy nhiên nó chậm hơn rất nhiều so với RAM.  
*Cách hoạt động:*
- Khi hệ thống không còn đủ RAM để lưu trữ tiến trình và dữ liệu, nó bắt đầu sử dụng Swap.
- Các trang bộ nhớ ít được sử dụng sẽ được chuyển từ RAM sang Swap để giải phóng RAM cho các tiến trình quan trọng.  
**5.7 PID**  
- Được cấp bởi kernel. PID được lấy từ một danh sách các số PID chưa được sử dụng. Khi cấp sẽ cấp từ giá trị nhỏ nhất.  

**6. Kill**  
**6.1 kill**  
- Mặc định, lệnh kill gửi tín hiệu SIGTERM (15) đến một tiến trình.
- Tiến trình có thể xử lý tín hiệu này trước khi thoát:  
    Giải phóng tài nguyên.  
    Lưu trạng thái.  
    Thực hiện các thao tác dọn dẹp.  
- Tiến trình sẽ tự quyết định cách xử lý tín hiệu này.
- Nếu tiến trình không phản hồi hoặc không lập trình để xử lý tín hiệu, nó sẽ không dừng.  

**6.2 kill -9**  
- Lệnh kill -9 gửi tín hiệu SIGKILL (9) đến tiến trình.
- Tín hiệu SIGKILL là tín hiệu không thể bị chặn, bắt, hoặc bỏ qua.
- Kernel sẽ ngay lập tức dừng tiến trình, bất kể trạng thái của nó.
- Kernel sẽ dừng tiến trình ngay lập tức.
- Tiến trình không thể từ chối hoặc xử lý tín hiệu này.

**7. Các thành phần của 1 server vật lý**

**7.1 CPU**

CPU (Central Processing Unit - bộ xử lý trung tâm) gồm:
- Đơn vị điều khiển: quản lý và điều khiển luồng dữ liệu giữ các thành phần của máy tính, giải mã và thực thi các lệnh.
- Đơn vị tính toán và logic: thực hiện các phép toán số học, xử lý các phép logic
- Thanh ghi: bộ nhớ nhỏ, tốc độ cao trong CPU, lưu trữ tạm thời dữ liệu và lệnh trong khi xử lý.

**Chức năng CPU:**

- xử lý dữ liệu
- giải mã và thực thi lệnh
- điều phối hoạt động của hệ thống
- đa nhiệm
- quản lý bộ nhớ: sử dụng các thanh ghi (registers) và cache để lưu trữ tạm thời dữ liệu trong quá trình xử lý. Nó cũng phối hợp với RAM để lấy và trả dữ liệu nhanh chóng, đảm bảo hiệu suất hoạt động tối ưu

**Đơn vị đo:**

*a. Tốc độ xung nhịp* 

Đơn vị: Hertz (Hz)

Thường được đo bằng:

MHz (Megahertz): 1 triệu chu kỳ/giây.

GHz (Gigahertz): 1 tỷ chu kỳ/giây.

Ý nghĩa: Thể hiện số chu kỳ xử lý mà CPU có thể thực hiện trong mỗi giây.

Ví dụ: CPU có xung nhịp 3.5 GHz có thể thực hiện 3.5 tỷ chu kỳ mỗi giây.

*b. Số lõi (Cores) và Số luồng (Threads)*

Số lõi: Số đơn vị xử lý độc lập trong CPU.

Số luồng: Các luồng xử lý ảo được hỗ trợ nhờ công nghệ siêu phân luồng (Hyper-Threading hoặc SMT).

Ý nghĩa:

CPU nhiều lõi và luồng có thể xử lý đồng thời nhiều tác vụ hơn, đặc biệt trong các ứng dụng đa luồng như dựng phim, xử lý video, hoặc chơi game hiện đại.

**7.2 RAM**

- Bộ nhớ tạm thời trong máy tính, lưu trữ dữ liệu và các lệnh đang được CPU xử lý, giúp tăng tốc độ truy xuất

**Chức năng**

- Lưu trữ dữ liệu tạm thời
- Hỗ trợ đa nhiệm
- Tăng tốc độ xử lý: giúp CPU không phải truy cập dữ liệu từ ổ cứng
- Dung lượng RAM: Gigabytes (GB) hoặc Terabytes (TB), RAM dung lượng lớn cho phép chạy nhiều chương trình nặng hoặc xử lý dữ liệu lớn hơn.
- Tốc độ RAM: Đơn vị: MHz hoặc MT/s (Megatransfers per second), Tốc độ càng cao, dữ liệu được truyền tải giữa RAM và CPU càng nhanh.

**7.3 DISK**

thiết bị dùng để lưu trữ dữ liệu trong máy tính. Nó giữ toàn bộ hệ điều hành, phần mềm, tệp tin và dữ liệu cá nhân, hoạt động ngay cả khi máy tính tắt.

**Chức năng**
- Lưu trữ dữ liệu lâu dài
- Cung cấp dữ liệu cho hệ thống
- Quản lý không gian lưu trữ
- Dung lượng lưu trữ (Capacity): Gigabytes (GB), Terabytes (TB)
- Tốc độ đọc/ghi (Read/Write Speed): MB/s (Megabytes per second), GB/s (Gigabytes per second).
