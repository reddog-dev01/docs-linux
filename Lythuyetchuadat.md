**1.Using Streams**  
  
**1.1 Standard Input (stdin)**
- Sử dụng bởi các chương trình hoặc lệnh để nhập dữ liệu đầu vào từ người dùng hoặc từ nguồn khác (tệp).
- Mặc đinh dữ liệu nhập qua stdin đến từ bàn phím.  
**Nhập từ bàn phím:** Nếu 1 chương trình đọc từ stdin và không có dữ liệu nào được chuyển hướng, nó sẽ đợi người dùng nhập dữ liệu từ bàn phím.
**Chuyển hướng stdin từ 1 tệp:** Đọc dữ liệu từ 1 tệp thay vì bàn phím
  VD:
  ```
  cat < file.txt
  ```
**Sử dụng pipe để truyền stdin:** chuyển stdout của 1 lệnh làm đầu vào stdin của cho lệnh khác.

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
