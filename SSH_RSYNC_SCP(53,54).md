### **1. SSH**

- SSH (Secure Shell) là một giao thức mạng an toàn cho việc điều khiển và quản lý các máy tính từ xa qua mạng. Nó được sử dụng chủ yếu trong các hệ thống máy chủ Linux/Unix và cung cấp một kênh bảo mật, giúp người dùng có thể truyền tải dữ liệu, chạy các lệnh, và quản lý hệ thống từ xa mà không cần phải ở trực tiếp tại máy chủ. SSH thay thế các giao thức không an toàn hơn như Telnet và rlogin, cung cấp các phương thức mã hóa mạnh mẽ để bảo vệ thông tin trao đổi giữa các hệ thống.

#### **1.1 Các thành phần cơ bản và đặc điểm nổi bật**

Các thành phần cơ bản của SSH (Secure Shell) bao gồm các yếu tố chính sau:

##### 1. **Máy khách (SSH Client)**
   - Máy khách SSH là phần mềm hoặc công cụ cho phép người dùng kết nối với một máy chủ SSH từ xa. Máy khách này sẽ thực hiện các kết nối an toàn đến máy chủ SSH và cung cấp các tính năng như mã hóa, xác thực, và truyền tải dữ liệu.
   - Ví dụ về các công cụ máy khách SSH bao gồm:
     - **OpenSSH client**: Một công cụ dòng lệnh phổ biến trên hệ điều hành Unix/Linux.
     - **PuTTY**: Một công cụ phổ biến trên Windows để kết nối SSH.
     - **Mosh**: Một công cụ thay thế SSH cho môi trường không ổn định.
   
##### 2. **Máy chủ (SSH Server)**
   - Máy chủ SSH là một phần mềm chạy trên một máy tính từ xa, cho phép các máy khách SSH kết nối và giao tiếp với nó. Máy chủ này sẽ xử lý tất cả các yêu cầu kết nối từ các máy khách và quản lý xác thực, bảo mật, cũng như các quyền truy cập của người dùng.
   - Ví dụ về các phần mềm máy chủ SSH phổ biến là **OpenSSH Server** và **Dropbear**.

##### 3. **Cơ chế xác thực (Authentication Mechanism)**
   - SSH cung cấp hai phương thức chính để xác thực người dùng khi kết nối:
     - **Xác thực bằng mật khẩu**: Người dùng nhập tên đăng nhập và mật khẩu để xác thực. Mặc dù dễ sử dụng, phương thức này không được coi là an toàn nếu mật khẩu yếu hoặc bị tấn công.
     - **Xác thực bằng khóa công khai (Public Key Authentication)**: Phương thức an toàn hơn, nơi người dùng tạo một cặp khóa công khai và khóa riêng. Khóa công khai được lưu trên máy chủ SSH, và khóa riêng được lưu trên máy khách. Khi kết nối, máy chủ sử dụng khóa công khai để xác thực khóa riêng của máy khách, thay vì yêu cầu mật khẩu.

##### 4. **Mã hóa (Encryption)**
   - SSH sử dụng mã hóa mạnh mẽ để bảo vệ dữ liệu trong quá trình truyền tải giữa máy khách và máy chủ. Các thuật toán mã hóa như AES (Advanced Encryption Standard), 3DES (Triple DES), và ChaCha20 được sử dụng để mã hóa dữ liệu.
   - Mã hóa trong SSH có hai loại:
     - **Mã hóa đối xứng (Symmetric encryption)**: Cả máy khách và máy chủ sử dụng cùng một khóa để mã hóa và giải mã dữ liệu.
     - **Mã hóa không đối xứng (Asymmetric encryption)**: Sử dụng cặp khóa công khai và khóa riêng. Đây là phương thức được dùng trong xác thực khóa công khai.

##### 5. **Xác thực máy chủ (Server Authentication)**
   - Khi một máy khách kết nối tới máy chủ lần đầu tiên, máy khách sẽ kiểm tra khóa công khai của máy chủ để xác thực máy chủ đó. Nếu khóa của máy chủ không thay đổi, máy khách sẽ kết nối mà không cần yêu cầu xác nhận. Nếu khóa thay đổi (có thể là dấu hiệu của một cuộc tấn công Man-in-the-Middle), máy khách sẽ thông báo và không kết nối.
   - Điều này giúp bảo vệ người dùng khỏi các cuộc tấn công giả mạo máy chủ.

##### 6. **Tính toàn vẹn của dữ liệu (Data Integrity)**
   - SSH sử dụng các hàm băm như SHA (Secure Hash Algorithm) để đảm bảo rằng dữ liệu không bị thay đổi trong quá trình truyền tải. Các thuật toán này tạo ra một giá trị băm duy nhất cho dữ liệu, giúp phát hiện sự thay đổi hoặc giả mạo trong quá trình truyền.

##### 7. **Chuyển tiếp cổng (Port Forwarding)**
   - SSH cung cấp tính năng chuyển tiếp cổng, cho phép bạn truyền tải dữ liệu giữa các cổng máy tính cục bộ và máy tính từ xa qua kênh bảo mật. Điều này giúp bạn có thể truy cập các dịch vụ nội bộ mà không cần mở các cổng trực tiếp trên tường lửa.
   - Có ba loại chuyển tiếp cổng trong SSH:
     - **Local port forwarding**: Chuyển tiếp cổng từ máy tính cục bộ tới máy chủ từ xa.
     - **Remote port forwarding**: Chuyển tiếp cổng từ máy chủ từ xa tới máy tính cục bộ.
     - **Dynamic port forwarding**: Sử dụng SSH như một proxy để kết nối tới các dịch vụ mạng khác.

##### 8. **Chạy lệnh từ xa (Remote Command Execution)**
   - SSH cho phép người dùng chạy các lệnh từ xa trên máy chủ mà không cần đăng nhập vào hệ thống. Điều này rất hữu ích cho các quản trị viên hệ thống, giúp họ thực hiện các tác vụ tự động hoặc điều khiển máy chủ từ xa mà không cần có giao diện đồ họa.

##### 9. **Sao chép và truyền tải tệp (SCP và SFTP)**
   - **SCP (Secure Copy Protocol)**: Là một giao thức cho phép sao chép tệp an toàn giữa máy tính cục bộ và máy tính từ xa qua kết nối SSH.
   - **SFTP (SSH File Transfer Protocol)**: Là một giao thức an toàn để truyền tệp, tương tự như FTP nhưng sử dụng SSH để mã hóa và bảo mật các dữ liệu truyền tải.

##### 10. **Chuyển tiếp X (X11 Forwarding)**
   - SSH hỗ trợ chuyển tiếp giao diện đồ họa, cho phép bạn chạy các ứng dụng đồ họa từ một máy chủ từ xa và hiển thị chúng trên máy tính của bạn. Điều này rất hữu ích khi bạn cần truy cập và sử dụng ứng dụng GUI trên một máy chủ Linux từ xa thông qua kết nối SSH.
