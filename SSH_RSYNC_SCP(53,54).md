### **1. SSH**

**SSH là gì**
- SSH (Secure Shell) là một giao thức mạng cho phép truy cập vào máy chủ từ xa thông qua mạng internet không bảo mật. 

**SSH dùng để làm gì**
- Truy cập từ xa, quản lý hệ thống, truyền tải dữ liệu.


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

#### **1.2 Quy trình hoạt động SSH**

Quy trình hoạt động của SSH (Secure Shell) có thể được mô tả qua các bước sau đây, từ khi kết nối bắt đầu cho đến khi người dùng có thể thực hiện các lệnh từ xa trên máy chủ.

##### 1. **Kết nối và Thiết lập**
   - **Máy khách SSH (Client)** gửi một yêu cầu kết nối tới **Máy chủ SSH (Server)**. Khi kết nối được thiết lập, máy chủ sẽ bắt đầu quá trình xác thực và bảo mật.

##### 2. **Xác thực Máy chủ (Server Authentication)**
   - Máy khách kiểm tra khóa công khai của máy chủ để đảm bảo rằng nó đang kết nối với đúng máy chủ (tránh các cuộc tấn công Man-in-the-Middle).
   - Nếu đây là lần đầu tiên máy khách kết nối, máy khách sẽ hỏi người dùng có muốn tiếp tục kết nối hay không (vì máy khách chưa có bản sao của khóa máy chủ).
   - Sau khi xác thực, máy khách sẽ lưu khóa công khai của máy chủ vào một tệp (thường là `known_hosts` trên máy khách) để sử dụng trong các lần kết nối tiếp theo.

##### 3. **Đàm phán Thuật toán Mã hóa**
   - Máy khách và máy chủ đàm phán để chọn các thuật toán mã hóa mà họ sẽ sử dụng trong suốt phiên làm việc. Các thuật toán này có thể bao gồm:
     - **Mã hóa dữ liệu (Encryption)**: Đảm bảo tính bảo mật của dữ liệu.
     - **Hàm băm (Hashing)**: Đảm bảo tính toàn vẹn của dữ liệu.
     - **Xác thực (Authentication)**: Đảm bảo rằng hai bên là những người hợp lệ.

##### 4. **Xác thực Người Dùng (User Authentication)**
   - Máy chủ yêu cầu xác thực người dùng để đảm bảo rằng người dùng có quyền truy cập.
   - Có hai phương thức xác thực chính:
     - **Xác thực bằng mật khẩu (Password Authentication)**: Máy khách gửi mật khẩu của người dùng đến máy chủ để xác thực.
     - **Xác thực bằng khóa công khai (Public Key Authentication)**: Máy khách gửi khóa công khai của mình đến máy chủ, và máy chủ sử dụng khóa công khai để xác thực khóa riêng của máy khách (cặp khóa đã được tạo trước).

   - **Quá trình xác thực bằng khóa công khai**:
     - Máy khách tạo cặp khóa công khai và khóa riêng (private key). Khóa công khai được lưu trữ trên máy chủ.
     - Khi kết nối, máy khách sẽ tạo ra một thông điệp ký bằng khóa riêng của mình và gửi nó đến máy chủ.
     - Máy chủ sử dụng khóa công khai đã lưu để kiểm tra xem thông điệp có khớp với khóa riêng của máy khách hay không. Nếu đúng, máy chủ cho phép kết nối.

##### 5. **Mã hóa và Truyền Dữ liệu**
   - Sau khi xác thực, một kênh mã hóa an toàn giữa máy khách và máy chủ được thiết lập.
   - Dữ liệu giữa máy khách và máy chủ được mã hóa bằng thuật toán mà hai bên đã thỏa thuận trước đó. Việc mã hóa giúp bảo mật các thông tin nhạy cảm, tránh bị nghe lén trong quá trình truyền tải.

##### 6. **Chạy Lệnh từ Xa (Remote Command Execution)**
   - Sau khi kết nối được thiết lập và xác thực hoàn tất, người dùng có thể bắt đầu gửi các lệnh từ máy khách đến máy chủ.
   - SSH cho phép người dùng thực thi các lệnh shell trên máy chủ từ xa, điều khiển máy chủ giống như khi người dùng đang làm việc trực tiếp trên đó.
   - Các lệnh này có thể bao gồm thao tác với tệp, quản lý hệ thống, hoặc các tác vụ khác mà người dùng có quyền truy cập.

##### 7. **Chuyển Tiếp Cổng (Port Forwarding)**
   - SSH cũng hỗ trợ tính năng **Chuyển Tiến Cổng (Port Forwarding)**, cho phép chuyển tiếp các kết nối mạng từ cổng này đến cổng khác thông qua kênh SSH mã hóa.
   - Có ba loại chuyển tiếp cổng:
     - **Local Port Forwarding**: Chuyển tiếp cổng từ máy khách đến máy chủ.
     - **Remote Port Forwarding**: Chuyển tiếp cổng từ máy chủ đến máy khách.
     - **Dynamic Port Forwarding**: Sử dụng máy khách SSH như một proxy để truyền tải dữ liệu.

##### 8. **Sao chép và Truyền Tải Tệp (SCP/SFTP)**
   - **SCP (Secure Copy Protocol)** và **SFTP (SSH File Transfer Protocol)** là các giao thức được sử dụng để sao chép và truyền tải tệp an toàn qua kết nối SSH.
   - Máy khách có thể sao chép tệp từ máy chủ sang máy tính cục bộ và ngược lại, hoặc điều hướng và làm việc với các tệp trên máy chủ từ xa một cách an toàn.

##### 9. **Kết Thúc Phiên**
   - Khi công việc hoàn tất, người dùng có thể đóng phiên SSH bằng cách nhập lệnh `exit` hoặc đóng cửa sổ terminal.
   - Kết nối SSH sẽ bị ngắt và mọi thông tin giao tiếp sẽ bị xóa.

#### **1.3 Thực hành vào máy chủ sử dụng password**

Để **SSH vào máy chủ sử dụng mật khẩu**, bạn có thể thực hiện các bước sau, kèm theo ví dụ cụ thể.

##### **Các Bước Kết Nối SSH Sử Dụng Mật Khẩu**

1. **Mở Terminal**
   - Mở ứng dụng Terminal.

2. **Nhập Lệnh SSH**
   Sử dụng lệnh sau để kết nối với máy chủ qua SSH. Bạn cần thay `username` bằng tên người dùng trên máy chủ và `hostname` (hoặc địa chỉ IP của máy chủ) bằng địa chỉ máy chủ mà bạn muốn kết nối.

   Cú pháp:

   ```
   ssh username@hostname
   ```

   Ví dụ, nếu bạn có một máy chủ với địa chỉ IP là `192.168.1.100` và tên người dùng là `root`, lệnh sẽ như sau:

   ```
   ssh root@192.168.1.100
   ```

   Nếu bạn muốn kết nối đến máy chủ qua một cổng khác (ví dụ: cổng 2222 thay vì cổng mặc định 22), bạn có thể chỉ định cổng với tham số `-p`:

   ```
   ssh root@192.168.1.100 -p 2222
   ```

3. **Nhập Mật Khẩu**
   Sau khi bạn gõ lệnh trên và nhấn **Enter**, hệ thống sẽ yêu cầu bạn nhập mật khẩu của người dùng trên máy chủ. Lúc này, bạn chỉ cần nhập mật khẩu và nhấn **Enter**.

   Ví dụ:

   ```
   root@192.168.1.100's password: ********
   ```

   **Lưu ý**: Khi bạn nhập mật khẩu, **không có dấu hiệu gì xuất hiện** (không có dấu asterisk `*` hoặc dấu chấm). Đây là một biện pháp bảo mật để không lộ mật khẩu.

4. **Kết Nối Thành Công**
   Nếu mật khẩu đúng, bạn sẽ được đăng nhập vào máy chủ từ xa và thấy dấu nhắc lệnh (prompt) của máy chủ, ví dụ:

   ```
   root@hostname:~#
   ```

   Bây giờ, bạn có thể thực hiện các lệnh trên máy chủ từ xa như thể bạn đang sử dụng máy tính đó.

5. **Thoát Khỏi SSH**
   Khi bạn làm xong, bạn có thể thoát khỏi phiên SSH bằng lệnh:

   ```
   exit
   ```


##### **Ví Dụ Cụ Thể**

1. Mở **Terminal** (hoặc PowerShell nếu bạn dùng Windows).
2. Nhập lệnh:

   ```
   ssh admin@192.168.1.10
   ```

3. Nhập mật khẩu khi được yêu cầu, ví dụ mật khẩu là `password123`.

4. Sau khi nhập mật khẩu đúng, bạn sẽ thấy dấu nhắc lệnh của máy chủ:

   ```
   admin@192.168.1.10's password: ********
   admin@hostname:~$
   ```

5. Bạn có thể thực hiện các lệnh trên máy chủ từ xa. Ví dụ, kiểm tra danh sách các file:

   ```
   ls -l
   ```

6. Để thoát khỏi phiên SSH, gõ lệnh:

   ```
   exit
   ```

#### **1.4 SSH vào máy chủ sử dụng key**

##### **Bước 1: Tạo Cặp Khóa SSH trên Máy Cục Bộ (Client)**

Trước khi kết nối, bạn cần tạo một cặp khóa SSH (khóa công khai và khóa riêng). Bạn có thể tạo cặp khóa SSH trên máy của mình (máy tính cục bộ) bằng lệnh sau:

1. Mở **Terminal** trên máy của bạn.

2. Chạy lệnh sau để tạo cặp khóa:

   ```
   ssh-keygen -t rsa -b 2048
   ```

   - `-t rsa`: Chọn thuật toán RSA.
   - `-b 2048`: Đặt độ dài khóa là 2048 bit (mức độ bảo mật hợp lý).

3. Sau khi chạy lệnh, bạn sẽ được yêu cầu chỉ định vị trí lưu trữ khóa (mặc định là `~/.ssh/id_rsa`):

   ```
   Enter file in which to save the key (/home/username/.ssh/id_rsa):
   ```

   Nếu bạn nhấn **Enter**, khóa sẽ được lưu tại vị trí mặc định (`~/.ssh/id_rsa`).

4. Bạn cũng có thể chọn nhập **passphrase** để bảo vệ khóa riêng. Đây là một lớp bảo mật bổ sung, nhưng bạn cũng có thể bỏ qua nếu không muốn sử dụng passphrase.


##### **Bước 2: Sao Chép Khóa Công Khai lên Máy Chủ Ubuntu**

Sau khi tạo cặp khóa SSH, bạn cần sao chép **khóa công khai** lên máy chủ Ubuntu để cho phép xác thực mà không cần mật khẩu. Để sao chép khóa công khai, bạn có thể làm theo cách sau:

1. **Sử dụng lệnh `ssh-copy-id`** (đơn giản và tiện lợi):

   Chạy lệnh sau để sao chép khóa công khai lên máy chủ Ubuntu:

   ```
   ssh-copy-id username@hostname
   ```

   Ví dụ: Nếu tài khoản người dùng trên máy chủ Ubuntu của bạn là `ubuntu` và địa chỉ IP của máy chủ là `192.168.1.100`, lệnh sẽ như sau:

   ```
   ssh-copy-id ubuntu@192.168.1.100
   ```

2. **Nếu `ssh-copy-id` không có sẵn** (hoặc bạn đang sử dụng Windows mà không có công cụ này), bạn có thể sao chép khóa thủ công:

   1. **Mở file khóa công khai** trên máy tính của bạn:

      ```
      cat ~/.ssh/id_rsa.pub
      ```

   2. **Đăng nhập vào máy chủ Ubuntu** bằng mật khẩu:

      ```
      ssh ubuntu@192.168.1.100
      ```

   3. **Tạo thư mục `.ssh` (nếu chưa có)** trên máy chủ và thay đổi quyền truy cập:

      ```
      mkdir -p ~/.ssh
      chmod 700 ~/.ssh
      ```

   4. **Mở file `authorized_keys`** và dán nội dung khóa công khai vào:

      ```
      nano ~/.ssh/authorized_keys
      ```

   5. **Dán khóa công khai** (dán nội dung từ file `id_rsa.pub` vào đây).

   6. **Lưu và thoát**: Nhấn **Ctrl + X**, rồi nhấn **Y** để lưu và **Enter** để thoát.

   7. **Cập nhật quyền truy cập**:

      ```
      chmod 600 ~/.ssh/authorized_keys
      ```

##### **Bước 3: Kết Nối vào Máy Chủ Ubuntu Sử Dụng SSH Key**

Khi khóa công khai đã được sao chép lên máy chủ, bạn có thể kết nối từ máy cục bộ vào máy chủ Ubuntu mà không cần sử dụng mật khẩu nữa. Để kết nối, bạn chỉ cần chạy lệnh SSH sau:

```
ssh username@hostname
```

Ví dụ:

```
ssh ubuntu@192.168.1.100
```

Hệ thống sẽ tự động sử dụng khóa SSH (khóa công khai trên máy chủ và khóa riêng trên máy cục bộ) để xác thực mà không yêu cầu mật khẩu.


##### **Bước 4: (Tùy Chọn) Vô Hiệu Hóa Đăng Nhập Bằng Mật Khẩu trên Máy Chủ Ubuntu**

Để tăng cường bảo mật, bạn có thể vô hiệu hóa đăng nhập bằng mật khẩu và chỉ cho phép đăng nhập qua khóa SSH.

1. **Mở file cấu hình SSH** trên máy chủ Ubuntu:

   ```
   sudo nano /etc/ssh/sshd_config
   ```

2. **Tìm và thay đổi các dòng sau**:

   ```
   PasswordAuthentication no
   ChallengeResponseAuthentication no
   ```

3. **Lưu và thoát**: Nhấn **Ctrl + X**, rồi nhấn **Y** và **Enter** để lưu.

4. **Khởi động lại dịch vụ SSH** để áp dụng thay đổi:

   ```
   sudo systemctl restart sshd
   ```

Sau khi thay đổi này, máy chủ Ubuntu sẽ chỉ cho phép đăng nhập qua SSH key và sẽ không yêu cầu mật khẩu nữa.


##### **Lưu Ý Quan Trọng**

- **Bảo mật**: Luôn bảo vệ khóa riêng của bạn, vì ai có được khóa riêng có thể truy cập vào máy chủ. Nếu bạn sử dụng passphrase để bảo vệ khóa riêng, nó sẽ cung cấp một lớp bảo mật bổ sung.
- **Sao lưu**: Hãy sao lưu khóa riêng của bạn để tránh mất khả năng truy cập vào máy chủ nếu khóa bị mất.
- **Cập nhật Khóa**: Nếu bạn thay đổi máy tính hoặc thay đổi khóa SSH, nhớ cập nhật lại khóa công khai trên máy chủ.

**Ví dụ**

**Bước 1: Tạo SSH Key trên Máy Khách (Máy thật Ubuntu)**

1. **Tạo SSH Key Pair trên máy khách**:
   Nếu bạn chưa có SSH key trên máy khách (máy thật), bạn cần tạo một cặp key mới. Sử dụng lệnh sau trên máy thật:

   ```bash
   ssh-keygen -t rsa -b 4096
   ```

   - **`-t rsa`**: Chỉ định loại key (RSA).
   - **`-b 4096`**: Chỉ định chiều dài của key (4096 bit).
   
   Lệnh trên sẽ yêu cầu bạn nhập **đường dẫn** để lưu file key và **passphrase** (nếu bạn muốn bảo vệ key của mình bằng mật khẩu). Mặc định, key sẽ được lưu tại `~/.ssh/id_rsa`.

2. **Kiểm tra các files key đã tạo**:
   Sau khi tạo, bạn sẽ có hai file trong thư mục `~/.ssh/`:
   - **`id_rsa`**: Đây là private key (khóa riêng) của bạn.
   - **`id_rsa.pub`**: Đây là public key (khóa công khai) của bạn.

**Bước 2: Cấu hình SSH Key trên Máy Chủ (Máy ảo Ubuntu Server)**

1. **Sao chép Public Key vào Máy Chủ**:
   Để cấu hình SSH key cho phép đăng nhập vào máy ảo Ubuntu Server, bạn cần sao chép public key từ máy thật vào máy ảo. Bạn có thể sử dụng lệnh `ssh-copy-id` hoặc sao chép thủ công.

   **Sử dụng `ssh-copy-id`:**
   
   ```bash
   ssh-copy-id user@IP_of_VM
   ```

   Trong đó:
   - `user` là tên người dùng trên máy ảo Ubuntu Server.
   - `IP_of_VM` là địa chỉ IP của máy ảo.

   Lệnh trên sẽ yêu cầu bạn nhập mật khẩu của người dùng trên máy ảo để sao chép public key vào máy ảo.

2. **Sao chép thủ công (nếu không sử dụng `ssh-copy-id`)**:
   Nếu bạn không thể sử dụng `ssh-copy-id`, bạn có thể sao chép thủ công public key vào máy ảo. Làm như sau:

   - Mở file `id_rsa.pub` trên máy thật:

     ```bash
     cat ~/.ssh/id_rsa.pub
     ```

   - Đăng nhập vào máy ảo Ubuntu Server (bằng mật khẩu) và mở file `~/.ssh/authorized_keys` (nếu thư mục `~/.ssh` chưa tồn tại, bạn có thể tạo mới nó):

     ```bash
     mkdir -p ~/.ssh
     nano ~/.ssh/authorized_keys
     ```

   - Dán nội dung của `id_rsa.pub` vào file `authorized_keys` và lưu lại.

   - Đảm bảo rằng file `authorized_keys` có quyền truy cập đúng:

     ```bash
     chmod 600 ~/.ssh/authorized_keys
     chmod 700 ~/.ssh
     ```

**Bước 3: Cấu hình SSH Server (Trên Máy Ảo Ubuntu Server)**

1. **Kiểm tra SSH server trên máy ảo**:
   Đảm bảo rằng SSH server đang chạy trên máy ảo Ubuntu. Bạn có thể kiểm tra và khởi động dịch vụ SSH nếu cần:

   ```bash
   sudo systemctl status ssh
   ```

   Nếu dịch vụ chưa chạy, bạn có thể khởi động nó bằng:

   ```bash
   sudo systemctl start ssh
   ```

2. **Cấu hình để chỉ sử dụng key (tùy chọn)**:
   Để đảm bảo rằng SSH chỉ cho phép đăng nhập qua SSH key (và không qua mật khẩu), bạn có thể sửa cấu hình trong file `/etc/ssh/sshd_config`:

   Mở file cấu hình SSH:

   ```bash
   sudo nano /etc/ssh/sshd_config
   ```

   Tìm các dòng sau và đảm bảo chúng được cấu hình như sau:

   ```bash
   PasswordAuthentication no
   PubkeyAuthentication yes
   ```

   Sau đó, khởi động lại dịch vụ SSH để áp dụng thay đổi:

   ```bash
   sudo systemctl restart ssh
   ```

**Bước 4: SSH vào Máy Ảo từ Máy Khách**

1. **Kiểm tra kết nối SSH**:
   Bây giờ, từ máy thật, bạn có thể sử dụng SSH để đăng nhập vào máy ảo Ubuntu Server mà không cần mật khẩu:

   ```bash
   ssh user@IP_of_VM
   ```


### **1.5 ssh-add**

Lệnh `ssh-add` được sử dụng để thêm khóa SSH vào **SSH agent**, một chương trình giúp quản lý và lưu trữ các khóa SSH trong suốt phiên làm việc, giúp bạn không phải nhập passphrase mỗi khi sử dụng khóa SSH. SSH agent giữ các khóa đã được thêm vào bộ nhớ để tự động xác thực khi bạn kết nối tới máy chủ từ xa.

#### **Cấu trúc Câu Lệnh**

```
ssh-add [options] [file]
```

#### **Các Tham Số Thường Dùng của `ssh-add`**

- **Không tham số**: Nếu bạn không cung cấp tham số, lệnh `ssh-add` sẽ thêm khóa riêng mặc định (thường là `~/.ssh/id_rsa`) vào SSH agent.
  
  ```bash
  ssh-add
  ```

- **Thêm khóa SSH cụ thể**: Bạn có thể chỉ định khóa riêng cụ thể cần thêm vào SSH agent.

  ```bash
  ssh-add ~/.ssh/my_private_key
  ```

- **Liệt kê các khóa đã được thêm**: Dùng `-l` để liệt kê các khóa đã được SSH agent lưu trữ.

  ```bash
  ssh-add -l
  ```

- **Xóa tất cả các khóa khỏi SSH agent**: Dùng `-D` để xóa tất cả các khóa đã được thêm vào SSH agent.

  ```bash
  ssh-add -D
  ```

- **Xóa khóa cụ thể**: Dùng `-d` để xóa một khóa cụ thể khỏi SSH agent.

  ```bash
  ssh-add -d ~/.ssh/my_private_key
  ```

- **Chạy lệnh trong nền (background)**: Dùng `-A` để yêu cầu `ssh-add` tự động tải tất cả các khóa từ các agent đã được lưu trữ.

  ```bash
  ssh-add -A
  ```

#### **Cách Sử Dụng `ssh-add`**

##### **Bước 1: Kiểm Tra SSH Agent**
Trước khi sử dụng lệnh `ssh-add`, bạn cần đảm bảo rằng SSH agent đã được chạy. Để kiểm tra xem SSH agent có đang chạy không, bạn có thể dùng lệnh sau:

```bash
eval $(ssh-agent -s)
```

Nếu SSH agent chưa chạy, lệnh trên sẽ khởi động nó. Câu lệnh `ssh-agent` tạo ra một tiến trình và xuất ra các biến môi trường cần thiết cho các lệnh SSH.

##### **Bước 2: Thêm Khóa vào SSH Agent**
Sau khi SSH agent đang chạy, bạn có thể thêm khóa riêng vào SSH agent bằng lệnh `ssh-add`.

Ví dụ, để thêm khóa mặc định `id_rsa` vào SSH agent:

```bash
ssh-add ~/.ssh/id_rsa
```

Nếu khóa có passphrase, bạn sẽ được yêu cầu nhập passphrase cho khóa đó.

##### **Bước 3: Kiểm Tra Khóa Đã Được Thêm**
Để kiểm tra các khóa hiện tại trong SSH agent, bạn có thể sử dụng lệnh sau:

```bash
ssh-add -l
```

Lệnh này sẽ hiển thị danh sách các khóa đã được thêm vào SSH agent.

##### **Bước 4: Xóa Khóa**
Nếu bạn muốn xóa khóa ra khỏi SSH agent, bạn có thể dùng lệnh:

```bash
ssh-add -d ~/.ssh/id_rsa
```

Hoặc để xóa tất cả các khóa khỏi agent:

```bash
ssh-add -D
```

##### **Ví Dụ Cụ Thể**

1. **Khởi động SSH agent và thêm khóa**:

   ```bash
   eval $(ssh-agent -s)
   ssh-add ~/.ssh/id_rsa
   ```

2. **Liệt kê các khóa đã được thêm vào SSH agent**:

   ```bash
   ssh-add -l
   ```

3. **Xóa tất cả các khóa khỏi SSH agent**:

   ```bash
   ssh-add -D
   ```

4. **Xóa một khóa cụ thể khỏi SSH agent**:

   ```bash
   ssh-add -d ~/.ssh/my_private_key
   ```

##### **Tại sao Sử Dụng `ssh-add`?**
- **Tiết kiệm thời gian**: Khi bạn sử dụng `ssh-add`, SSH agent sẽ nhớ và tự động cung cấp khóa khi kết nối tới máy chủ SSH mà không yêu cầu bạn phải nhập passphrase mỗi lần.
- **Bảo mật**: Nếu bạn có nhiều khóa SSH, việc sử dụng `ssh-add` giúp bạn quản lý các khóa một cách hiệu quả, không phải nhập passphrase nhiều lần.
- **Dễ dàng khi làm việc với nhiều server**: Nếu bạn cần kết nối đến nhiều máy chủ khác nhau, `ssh-add` sẽ giúp bạn quản lý các khóa SSH mà không phải nhập passphrase nhiều lần trong phiên làm việc.


#### **1.6 Public key và Private key**



--------------------------------------------------



### **2. rsync và scp**


