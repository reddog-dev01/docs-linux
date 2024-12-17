### **1. Khái niệm**

**Keepalived** là một phần mềm mã nguồn mở được thiết kế để cung cấp **High Availability (HA)** và **Load Balancing** cho các dịch vụ mạng và máy chủ. Nó chủ yếu được sử dụng trong các hệ thống yêu cầu độ tin cậy cao, như các hệ thống web, các ứng dụng dịch vụ và các hạ tầng mạng, nơi yêu cầu luôn duy trì kết nối hoặc dịch vụ mà không có sự gián đoạn.

**Keepalived** thường được triển khai để:

- **Cung cấp tính năng chuyển đổi dự phòng (Failover):** Khi một máy chủ hoặc một dịch vụ gặp sự cố, Keepalived sẽ tự động chuyển quyền sở hữu của một địa chỉ IP ảo (VIP) sang một máy chủ khác để đảm bảo dịch vụ không bị gián đoạn.

- **Cung cấp Load Balancing:** Keepalived cũng có thể làm nhiệm vụ phân tải (load balancing) giữa nhiều máy chủ, đảm bảo rằng các yêu cầu được phân phối đồng đều và tối ưu giữa các máy chủ thực.

=> Nói chung là 1 phần mềm để xây dựng hệ thống cân bằng tải hoặc dự phòng.

----------------------------------------------------

### **2. Các tính năng chính của Keepalived**

#### 1. **High Availability (HA)**
Keepalived chủ yếu được thiết kế để cung cấp khả năng **High Availability** cho các dịch vụ mạng, đảm bảo rằng các dịch vụ sẽ luôn hoạt động mà không bị gián đoạn, ngay cả khi một hoặc nhiều máy chủ gặp sự cố.

- **Failover tự động:** Nếu một máy chủ gặp sự cố (chẳng hạn như máy chủ chủ bị lỗi), Keepalived sẽ tự động chuyển quyền sở hữu của **Virtual IP (VIP)** sang một máy chủ khác mà không cần can thiệp thủ công.
- **Virtual IP (VIP):** VIP là một địa chỉ IP ảo mà các client kết nối tới. Keepalived quản lý việc chuyển giao VIP giữa các máy chủ trong hệ thống dựa trên tình trạng hoạt động của các máy chủ (Master hoặc Backup).

#### 2. **Load Balancing**
Keepalived có khả năng thực hiện **Load Balancing** giữa các máy chủ trong một hệ thống. Các yêu cầu từ client sẽ được phân phối cho các máy chủ thực (real servers) để tối ưu hiệu suất và sử dụng tài nguyên hệ thống.

- **Cân bằng tải (Load Balancing):** Keepalived hỗ trợ các thuật toán cân bằng tải phổ biến như **Round Robin**, **Least Connections**, và **Weighted Round Robin**.
- **Phân phối tải cho các dịch vụ TCP/UDP:** Ngoài các dịch vụ HTTP(S), Keepalived cũng có thể cân bằng tải cho các dịch vụ khác như MySQL, PostgreSQL, FTP, hoặc bất kỳ dịch vụ nào sử dụng TCP/UDP.

#### 3. **Failover và Redundancy**
- **Redundancy (Dự phòng):** Keepalived triển khai cơ chế **Failover** với các máy chủ dự phòng (Backup). Nếu máy chủ chính (Master) không còn khả năng đáp ứng, một máy chủ Backup sẽ tiếp nhận và tiếp tục cung cấp dịch vụ.
- **Quản lý ưu tiên:** Keepalived sử dụng **VRRP (Virtual Router Redundancy Protocol)** để xác định máy chủ nào là **Master** và máy chủ nào là **Backup**. Máy chủ Master có **priority cao hơn** và sở hữu VIP, trong khi các máy chủ Backup có **priority thấp hơn** và sẽ chỉ tiếp nhận VIP khi Master gặp sự cố.

#### 4. **Health Checks (Kiểm tra sức khỏe)**
- **Kiểm tra trạng thái của các máy chủ thực:** Keepalived thực hiện các **health checks** định kỳ đối với các máy chủ thực (real servers). Nếu một máy chủ không phản hồi hoặc gặp lỗi, Keepalived sẽ loại bỏ nó khỏi danh sách các máy chủ có thể nhận yêu cầu, giúp đảm bảo rằng chỉ các máy chủ còn hoạt động mới nhận tải.
- **Các phương thức kiểm tra sức khỏe:** Keepalived hỗ trợ nhiều loại kiểm tra sức khỏe, bao gồm HTTP GET, TCP check, và script tùy chỉnh để kiểm tra trạng thái của các dịch vụ.

----------------------------------------------------------


### **3. Cơ chế hoạt động**

#### Cơ Chế Hoạt Động của **Keepalived**

**Keepalived** là một công cụ mạnh mẽ và phổ biến trong việc xây dựng các hệ thống **High Availability (HA)** và **Load Balancing** cho các dịch vụ mạng. Nó chủ yếu được sử dụng để cung cấp **dự phòng (failover)** và **cân bằng tải (load balancing)** cho các dịch vụ mạng, đặc biệt là trong các hệ thống **Linux**. Keepalived thực hiện điều này chủ yếu thông qua việc sử dụng **VRRP (Virtual Router Redundancy Protocol)** để tạo ra các **IP ảo** và **health checks** để theo dõi tình trạng của các máy chủ backend.

#### Các Thành Phần Chính trong Keepalived

1. **VRRP (Virtual Router Redundancy Protocol)**:
   - VRRP là giao thức giúp duy trì tính sẵn sàng cao cho các router (hoặc máy chủ) bằng cách sử dụng một **địa chỉ IP ảo**. Trong mô hình VRRP, có một **router chính** (Master) và nhiều **router phụ** (Backup).
   - Nếu router chính (Master) gặp sự cố, một router phụ sẽ được chọn để trở thành Master và tiếp tục cung cấp dịch vụ mà không bị gián đoạn.

2. **Health Check (Kiểm tra sức khỏe)**:
   - Keepalived hỗ trợ việc **kiểm tra sức khỏe** của các máy chủ backend hoặc các dịch vụ qua các phương pháp khác nhau như **HTTP GET**, **TCP Ping**, **Script**, v.v. Nếu một máy chủ backend không phản hồi hoặc gặp sự cố, Keepalived sẽ **loại bỏ** máy chủ đó khỏi danh sách backend hoặc không chuyển IP ảo (VIP) đến nó.

3. **Load Balancing**:
   - Keepalived hỗ trợ **cân bằng tải (load balancing)** thông qua các thuật toán như **Round Robin**, **Weighted Least Connection** và **NAT**. Các máy chủ backend có thể được phân phối tải dựa trên các thuật toán này, giúp cân bằng lưu lượng mạng giữa nhiều máy chủ backend.


#### Quy Trình Hoạt Động của Keepalived

1. **Khởi tạo và Quảng Bá VRRP**:
   - Khi Keepalived được cấu hình, mỗi máy chủ sẽ **quảng bá VRRP** (tức là gửi các thông báo về trạng thái của nó) đến các máy chủ khác trong cùng một nhóm VRRP.
   - Các máy chủ này sẽ sử dụng thông tin từ quảng bá VRRP để quyết định ai sẽ là **MASTER** (máy chủ chính) và ai sẽ là **BACKUP** (máy chủ phụ).
   - Các thông báo VRRP sẽ được gửi định kỳ để đảm bảo rằng các máy chủ đều có thông tin mới nhất về trạng thái của nhau.

2. **Chọn MASTER và BACKUP**:
   - **Máy chủ MASTER** sẽ nhận **IP ảo (VIP)** và sẽ xử lý tất cả các kết nối đến **VIP** đó. Máy chủ MASTER sẽ quảng bá thông qua VRRP với một `priority` cao nhất (có thể được cấu hình).
   - Nếu **MASTER** không còn hoạt động (chết), các máy chủ **BACKUP** sẽ **giành quyền** làm **MASTER** dựa trên giá trị của `priority` trong cấu hình. Máy chủ có **`priority` cao hơn** sẽ trở thành MASTER.
   - Nếu tất cả các máy chủ có cùng mức `priority`, Keepalived sẽ **chọn ngẫu nhiên** một trong số chúng để trở thành **MASTER**.

3. **Health Check và Kiểm Tra Tình Trạng Các Máy Chủ Backend**:
   - Keepalived thực hiện **health check** trên các máy chủ backend (real servers) thông qua các phương thức như **HTTP GET**, **TCP Ping**, **Script** (shell script), v.v.
   - Mỗi máy chủ backend sẽ được kiểm tra theo khoảng thời gian được định nghĩa trong cấu hình. Nếu một máy chủ backend không đáp ứng yêu cầu (ví dụ: không trả về mã trạng thái HTTP 200 hoặc không phản hồi với một ping TCP), Keepalived sẽ loại bỏ máy chủ đó khỏi danh sách các backend khả dụng.
   - Sau khi máy chủ backend phục hồi, Keepalived sẽ đưa máy chủ đó trở lại danh sách các máy chủ backend hoạt động.

4. **Cân Bằng Tải (Load Balancing)**:
   - Keepalived có thể **cân bằng tải** giữa các máy chủ backend sử dụng các thuật toán như **Round Robin**, **Weighted Least Connection**, và **NAT**.
     - **Round Robin**: Phân phối đều các yêu cầu đến tất cả các máy chủ backend.
     - **Weighted Least Connection**: Phân phối các yêu cầu đến các máy chủ backend với số kết nối ít nhất và có thể có trọng số khác nhau cho các máy chủ (dựa trên `weight` trong cấu hình).
     - **NAT (Network Address Translation)**: Địa chỉ IP của client được chuyển đổi để đảm bảo rằng các kết nối luôn đi đến đúng máy chủ backend.


#### Quá Trình Chuyển Đổi Tình Trạng (Failover)

1. **Master Chết**:
   - Nếu **máy chủ MASTER** gặp sự cố (chết), các máy chủ **BACKUP** sẽ nhận diện được điều này qua việc không nhận được quảng bá VRRP từ máy chủ MASTER.
   - Các máy chủ BACKUP sẽ so sánh `priority` của mình và chọn ra máy có `priority` cao nhất để trở thành **MASTER** và tiếp nhận IP ảo (VIP).
   - Máy chủ mới trở thành MASTER sẽ bắt đầu phục vụ lưu lượng mạng và xử lý các yêu cầu từ client.

2. **Máy Chủ Mới Khôi Phục**:
   - Khi **máy chủ MASTER cũ** khôi phục lại, nó sẽ lại gửi quảng bá VRRP và nhận diện rằng nó đã mất **VIP**. Nếu các máy chủ **BACKUP** vẫn hoạt động bình thường, máy chủ **MASTER cũ** sẽ không thể trở lại làm MASTER trừ khi các máy chủ BACKUP có sự thay đổi (ví dụ: hạ `priority`).
   - Keepalived không cho phép một máy chủ cũ trở lại làm MASTER nếu nó đã mất quyền **VIP** trừ khi có sự thay đổi rõ ràng về tình trạng các máy chủ BACKUP.


#### Các Tình Huống Thực Tế

1. **Master bị hỏng**:
   - Máy chủ MASTER không phản hồi hoặc bị hỏng => Các máy chủ BACKUP sẽ kiểm tra và chọn ra máy có `priority` cao nhất để làm MASTER.
   
2. **Máy Chủ MASTER Phục Hồi**:
   - Khi máy chủ MASTER phục hồi, nó không tự động lấy lại **VIP** (nếu các máy chủ BACKUP vẫn đang hoạt động bình thường). Máy chủ MASTER sẽ phải chờ cho đến khi không có máy chủ nào khác làm MASTER hoặc các máy chủ BACKUP có sự thay đổi.

---------------------------------------------------------

### **4. Cách cấu hình**

Để cấu hình **Keepalived** trên Ubuntu, bạn sẽ thực hiện một số bước cơ bản để thiết lập **Virtual Router Redundancy Protocol (VRRP)** cho tính khả dụng cao (High Availability) và **Load Balancing**. Dưới đây là hướng dẫn chi tiết từng bước.

#### 1. **Cài Đặt Keepalived trên Ubuntu**

Trước tiên, bạn cần cài đặt Keepalived trên các máy chủ của bạn.

```bash
sudo apt update
sudo apt install keepalived
```

Sau khi cài đặt xong, dịch vụ **Keepalived** sẽ được cài sẵn, nhưng bạn cần cấu hình nó để sử dụng.

#### 2. **Cấu Hình Keepalived**

Keepalived chủ yếu sử dụng tệp cấu hình **/etc/keepalived/keepalived.conf**. Bạn sẽ chỉnh sửa tệp này để cấu hình các tính năng như **VRRP**, **Health Checks**, và **Load Balancing**.

##### **Cấu Hình VRRP (Virtual Router Redundancy Protocol)**

Để cấu hình **VRRP (Virtual Router Redundancy Protocol)** trong **Keepalived** trên Ubuntu, bạn sẽ thực hiện theo các bước sau. **VRRP** giúp bạn thiết lập một hệ thống router dự phòng, trong đó các router chia sẻ một địa chỉ IP ảo (VIP). Nếu một router chính gặp sự cố, router phụ sẽ thay thế và tiếp tục cung cấp dịch vụ mà không làm gián đoạn kết nối.

###### 1. **Cài Đặt Keepalived**
Trước tiên, bạn cần cài đặt **Keepalived** trên cả máy chủ chính và máy chủ phụ.

```bash
sudo apt update
sudo apt install keepalived
```

###### A. **Cấu Hình Keepalived với VRRP**

**Cấu Hình VRRP trên Máy Chủ Chính (Master)**

1. Mở tệp cấu hình Keepalived:

```bash
sudo nano /etc/keepalived/keepalived.conf
```

2. Thêm cấu hình sau vào tệp để cấu hình VRRP cho máy chủ chính:

```bash
vrrp_instance VI_1 {
    state MASTER                      # Trạng thái MASTER cho máy chủ chính
    interface eth0                    # Giao diện mạng mà VIP sẽ được gán (thay eth0 nếu cần)
    virtual_router_id 51              # ID của Virtual Router (phải giống trên máy chủ Backup)
    priority 101                      # Mức độ ưu tiên (máy chủ có priority cao hơn sẽ là MASTER)
    advert_int 1                      # Thời gian quảng bá trạng thái của router (đơn vị giây)
    virtual_ipaddress {
        192.168.1.100                 # Địa chỉ IP ảo (VIP)
    }
    authentication {
        auth_type PASS                # Loại xác thực (có thể là PASS hoặc AH)
        auth_pass 1234                # Mật khẩu xác thực (phải giống trên máy chủ Backup)
    }
}
```

**Cấu Hình VRRP trên Máy Chủ Dự Phòng (Backup)**

1. Mở tệp cấu hình Keepalived trên máy chủ Backup:

```bash
sudo nano /etc/keepalived/keepalived.conf
```

2. Thêm cấu hình sau vào tệp để cấu hình VRRP cho máy chủ Backup:

```bash
vrrp_instance VI_1 {
    state BACKUP                     # Trạng thái BACKUP cho máy chủ dự phòng
    interface eth0                   # Giao diện mạng mà VIP sẽ được gán (thay eth0 nếu cần)
    virtual_router_id 51             # ID của Virtual Router (phải giống trên máy chủ Master)
    priority 90                      # Mức độ ưu tiên thấp hơn máy chủ chính
    advert_int 1                     # Thời gian quảng bá trạng thái của router (đơn vị giây)
    virtual_ipaddress {
        192.168.1.100                # Địa chỉ IP ảo (VIP)
    }
    authentication {
        auth_type PASS               # Loại xác thực (phải giống trên máy chủ Master)
        auth_pass 1234               # Mật khẩu xác thực (phải giống trên máy chủ Master)
    }
}
```

###### 3. **Khởi Động Dịch Vụ Keepalived**

Sau khi cấu hình xong, bạn cần khởi động lại dịch vụ **Keepalived** trên cả hai máy chủ:

- **Khởi động dịch vụ Keepalived**:

```bash
sudo systemctl start keepalived
```

- **Kích hoạt Keepalived tự động khởi động khi máy chủ khởi động lại**:

```bash
sudo systemctl enable keepalived
```

- **Kiểm tra trạng thái dịch vụ Keepalived**:

```bash
sudo systemctl status keepalived
```

###### 4. **Kiểm Tra VRRP và Tính Năng Failover**

**Kiểm Tra VIP**

1. **Kiểm tra trên máy chủ Master**: Bạn có thể kiểm tra nếu địa chỉ VIP (ví dụ: `192.168.1.100`) đã được gán cho máy chủ Master.

```bash
ip a show eth0
```

2. **Kiểm tra trên máy chủ Backup**: Nếu máy chủ Master bị tắt, máy chủ Backup sẽ tiếp nhận VIP.

```bash
ip a show eth0
```

**Kiểm Tra Failover**

1. **Tắt dịch vụ Keepalived trên máy chủ Master**:

```bash
sudo systemctl stop keepalived
```

2. **Kiểm tra trên máy chủ Backup**: Máy chủ Backup sẽ tự động tiếp nhận VIP và trở thành **MASTER**.

3. **Bật lại dịch vụ Keepalived trên máy chủ Master**:

```bash
sudo systemctl start keepalived
```

###### 5. **Xem Log và Kiểm Tra Lỗi**

Nếu có vấn đề xảy ra, bạn có thể xem log của Keepalived để xác định lỗi.

```bash
sudo journalctl -u keepalived
```

Hoặc xem trong tệp log hệ thống:

```bash
sudo tail -f /var/log/syslog
```

###### 6. **Tùy Chỉnh Thêm Các Tùy Chọn**

Bạn có thể thêm nhiều tùy chọn vào cấu hình VRRP tùy vào yêu cầu của hệ thống, chẳng hạn như:

- **Track Interface**: Để theo dõi trạng thái của các giao diện mạng. Nếu giao diện mạng bị lỗi, Keepalived sẽ thay đổi trạng thái của router.
  
  ```bash
  track_interface {
      eth0
  }
  ```
-------------------------------


#### **B. Cấu hình Load Balancing**


### 1. Cài Đặt Keepalived

Trước tiên, bạn cần cài đặt **Keepalived** trên các máy chủ mà bạn muốn sử dụng để cân bằng tải.

```bash
sudo apt-get update
sudo apt-get install keepalived
```

Cài đặt Keepalived trên tất cả các máy chủ (Master và Backup) mà bạn muốn sử dụng trong mô hình HA.

### 2. Cấu Hình **VRRP** cho Load Balancing

Giả sử bạn có một **Virtual IP (VIP)** và bạn muốn cấu hình Keepalived để cân bằng tải lưu lượng đến các máy chủ backend. Bạn sẽ sử dụng **VRRP** để đảm bảo **high availability** cho VIP và cấu hình **Load Balancing** cho các máy chủ backend.

### 3. Cấu Hình **Keepalived.conf** cho Load Balancing

#### Cấu Hình Trên Máy Chủ **Master**

Mở tệp cấu hình của Keepalived (thường là `/etc/keepalived/keepalived.conf`) và thêm vào nội dung sau:

```bash
vrrp_instance VI_1 {
    state MASTER                          # Trạng thái MASTER cho máy chủ chính
    interface ens33                        # Giao diện mạng (có thể là eth0, ens33, v.v.)
    virtual_router_id 51                   # ID của Virtual Router (phải giống trên máy chủ BACKUP)
    priority 101                           # Mức độ ưu tiên
    advert_int 1                           # Thời gian quảng bá trạng thái của router (1 giây)
    virtual_ipaddress {
        172.16.1.100                       # Địa chỉ IP ảo (VIP) cho cân bằng tải
    }
    authentication {
        auth_type PASS                     # Loại xác thực
        auth_pass 1234                     # Mật khẩu xác thực
    }

    # Cấu hình Load Balancing
    virtual_server 172.16.1.100 80 {
        delay_loop 6                       # Thời gian kiểm tra sức khỏe giữa các lần (6 giây)
        lb_algo rr                         # Thuật toán cân bằng tải (Round Robin)
        lb_kind NAT                         # Loại cân bằng tải (NAT)
        persistence_timeout 50             # Thời gian duy trì kết nối
        protocol TCP                        # Giao thức kết nối (TCP)

        # Cấu hình các máy chủ backend (real servers)
        real_server 172.16.1.200 80 {
            weight 1                        # Trọng số cho máy chủ backend
            HTTP_GET {
                url {
                    path /health_check     # Đường dẫn kiểm tra tình trạng sức khỏe
                }
                status_code 200           # Mã trạng thái HTTP hợp lệ khi máy chủ hoạt động bình thường
                connect_timeout 10        # Thời gian chờ kết nối
                nb_get_retry 3            # Số lần thử lại khi không nhận được phản hồi
                delay_before_retry 3      # Thời gian delay trước khi thử lại
            }
        }

        real_server 172.16.1.201 80 {
            weight 1                        # Trọng số cho máy chủ backend
            HTTP_GET {
                url {
                    path /health_check     # Đường dẫn kiểm tra tình trạng sức khỏe
                }
                status_code 200           # Mã trạng thái HTTP hợp lệ khi máy chủ hoạt động bình thường
                connect_timeout 10        # Thời gian chờ kết nối
                nb_get_retry 3            # Số lần thử lại khi không nhận được phản hồi
                delay_before_retry 3      # Thời gian delay trước khi thử lại
            }
        }
    }
}
```

#### Giải Thích Cấu Hình

- **vrrp_instance VI_1**: Đây là cấu hình cho VRRP instance. Máy chủ này sẽ quảng bá trạng thái của nó như là **MASTER** hoặc **BACKUP**.
- **interface ens33**: Giao diện mạng mà Keepalived sẽ sử dụng.
- **virtual_router_id 51**: Mã số ID của Virtual Router (phải trùng với giá trị ở máy chủ BACKUP).
- **virtual_ipaddress 172.16.1.100**: Địa chỉ IP ảo (VIP) mà các client sẽ kết nối vào. Đây là IP mà các máy chủ backend sẽ nhận lưu lượng và chuyển tiếp tới.
- **authentication**: Xác thực giữa các máy chủ VRRP để đảm bảo tính bảo mật.
- **virtual_server 172.16.1.100 80**: Địa chỉ IP ảo (VIP) và cổng mà các kết nối HTTP sẽ được cân bằng tải.
- **real_server 172.16.1.200 80** và **172.16.1.201 80**: Đây là các máy chủ backend mà Keepalived sẽ chuyển tiếp lưu lượng đến. Bạn có thể cấu hình nhiều máy chủ backend.
- **health check (HTTP_GET)**: Kiểm tra sức khỏe của các máy chủ backend thông qua việc gửi HTTP GET request đến `/health_check`. Nếu mã trạng thái là `200`, máy chủ sẽ được coi là hoạt động bình thường.

### 4. Cấu Hình **Keepalived.conf** trên Máy Chủ **Backup**

Trên máy chủ **BACKUP**, bạn cần cấu hình Keepalived để có thể chuyển sang làm MASTER khi máy chủ chính (MASTER) bị hỏng. Mở tệp `/etc/keepalived/keepalived.conf` và thêm vào nội dung sau:

```bash
vrrp_instance VI_1 {
    state BACKUP                         # Trạng thái BACKUP cho máy chủ phụ
    interface ens33                       # Giao diện mạng
    virtual_router_id 51                  # ID của Virtual Router (phải giống trên máy chủ MASTER)
    priority 100                          # Mức độ ưu tiên (thấp hơn MASTER)
    advert_int 1                          # Thời gian quảng bá trạng thái của router (1 giây)
    virtual_ipaddress {
        172.16.1.100                      # Địa chỉ IP ảo (VIP)
    }
    authentication {
        auth_type PASS                    # Loại xác thực
        auth_pass 1234                    # Mật khẩu xác thực
    }
}
```

Ở đây, máy chủ **BACKUP** có **priority thấp hơn** máy chủ MASTER. Khi MASTER gặp sự cố, máy chủ BACKUP này sẽ nhận VIP và trở thành MASTER.

### 5. Khởi Động và Kiểm Tra

Sau khi đã cấu hình xong Keepalived trên cả hai máy chủ, bạn cần khởi động dịch vụ Keepalived và kiểm tra trạng thái:

- **Khởi động dịch vụ Keepalived**:

```bash
sudo systemctl restart keepalived
```

- **Kiểm tra trạng thái dịch vụ Keepalived**:

```bash
sudo systemctl status keepalived
```

### 6. Kiểm Tra Cân Bằng Tải

Để kiểm tra Load Balancing, bạn có thể sử dụng **curl** hoặc **wget** để kiểm tra địa chỉ VIP và các máy chủ backend.

- **Truy cập VIP** (172.16.1.100):

```bash
curl http://172.16.1.100
```

Kết quả sẽ được phân phối giữa các máy chủ backend (172.16.1.200 và 172.16.1.201) tùy theo thuật toán cân bằng tải mà bạn cấu hình (ví dụ: **Round Robin**).

### 7. Kiểm Tra Failover

Để kiểm tra tính năng **failover**:
1. Tắt dịch vụ Keepalived trên máy chủ **MASTER**:
   ```bash
   sudo systemctl stop keepalived
   ```
2. Máy chủ **BACKUP** sẽ tự động nhận VIP và trở thành MASTER.
3. Khởi động lại dịch vụ Keepalived trên máy chủ MASTER và nó sẽ lấy lại VIP nếu máy chủ BACKUP đã hết thời gian quảng bá.
