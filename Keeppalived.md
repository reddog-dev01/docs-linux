### **1. Khái niệm**

**Keepalived** là một phần mềm mã nguồn mở được thiết kế để cung cấp **High Availability (HA)** và **Load Balancing** cho các dịch vụ mạng và máy chủ. Nó chủ yếu được sử dụng trong các hệ thống yêu cầu độ tin cậy cao, như các hệ thống web, các ứng dụng dịch vụ và các hạ tầng mạng, nơi yêu cầu luôn duy trì kết nối hoặc dịch vụ mà không có sự gián đoạn.

**Keepalived** thường được triển khai để:

- **Cung cấp tính năng chuyển đổi dự phòng (Failover):** Khi một máy chủ hoặc một dịch vụ gặp sự cố, Keepalived sẽ tự động chuyển quyền sở hữu của một địa chỉ IP ảo (VIP) sang một máy chủ khác để đảm bảo dịch vụ không bị gián đoạn.

- **Cung cấp Load Balancing:** Keepalived cũng có thể làm nhiệm vụ phân tải (load balancing) giữa nhiều máy chủ, đảm bảo rằng các yêu cầu được phân phối đồng đều và tối ưu giữa các máy chủ thực.

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

**Cơ chế hoạt động của Keepalived** chủ yếu dựa vào **Virtual Router Redundancy Protocol (VRRP)** để duy trì tính khả dụng cao (High Availability - HA) cho các dịch vụ mạng, cũng như thực hiện **Load Balancing**. Keepalived có thể được cấu hình để tự động chuyển đổi giữa các máy chủ trong một hệ thống khi một máy chủ gặp sự cố, đồng thời phân phối tải giữa các máy chủ thực để tối ưu hiệu suất.

Dưới đây là mô tả chi tiết về cơ chế hoạt động của Keepalived:

### 1. **Quản lý Virtual IP (VIP)**
Keepalived sử dụng **Virtual IP (VIP)**, là một địa chỉ IP ảo mà các client sẽ kết nối tới. VIP không phải là địa chỉ IP cố định của một máy chủ, mà thay vào đó là địa chỉ mà nhiều máy chủ có thể chia sẻ. Các máy chủ có thể sở hữu VIP này tùy thuộc vào trạng thái của hệ thống.

- **Master (Chủ)**: Máy chủ chính sở hữu VIP và phục vụ các yêu cầu từ client.
- **Backup (Dự phòng)**: Các máy chủ backup theo dõi tình trạng của máy chủ chủ (Master) và chỉ sở hữu VIP khi Master không thể hoạt động.

### 2. **Virtual Router Redundancy Protocol (VRRP)**
Keepalived sử dụng giao thức **VRRP** để quản lý VIP và đảm bảo tính khả dụng cao. **VRRP** giúp xác định máy chủ nào là **Master** và máy chủ nào là **Backup**, thông qua các **Priority** và **State**. Quy trình hoạt động của VRRP như sau:

- **Master** (Máy chủ chính) có **Priority cao hơn** và sở hữu VIP. Nó sẽ gửi các thông điệp VRRP cho các máy chủ khác trong mạng để thông báo rằng nó đang là máy chủ chủ.
- **Backup** (Máy chủ dự phòng) có **Priority thấp hơn** và không sở hữu VIP cho đến khi Master không còn khả năng hoạt động. Máy chủ dự phòng sẽ theo dõi thông điệp VRRP từ Master để biết khi nào cần tiếp nhận VIP.

### 3. **Kiểm Tra Sức Khỏe (Health Checks)**
Keepalived có khả năng thực hiện **Health Checks** đối với các máy chủ thực (real servers) để kiểm tra xem các dịch vụ có hoạt động bình thường không. Các kiểm tra sức khỏe có thể bao gồm:

- **TCP Health Checks**: Kiểm tra kết nối TCP tới một cổng cụ thể (ví dụ, kiểm tra kết nối tới cổng HTTP/HTTPS).
- **HTTP GET Health Checks**: Kiểm tra xem một trang web hoặc API có thể truy cập được không.
- **Custom Scripts**: Sử dụng các script tùy chỉnh để kiểm tra trạng thái của dịch vụ.

Nếu một máy chủ không phản hồi hoặc gặp sự cố, Keepalived sẽ loại bỏ nó khỏi nhóm máy chủ thực đang nhận tải và không gửi yêu cầu tới máy chủ đó.

### 4. **Cân Bằng Tải (Load Balancing)**
Keepalived có thể thực hiện **Load Balancing** giữa các máy chủ thực để phân phối tải (traffic) một cách đồng đều và tối ưu hóa hiệu suất. Cấu hình cân bằng tải bao gồm các tham số như:

- **Thuật toán cân bằng tải**: Keepalived hỗ trợ các thuật toán như **Round Robin**, **Least Connections**, và **Weighted Round Robin** để phân phối yêu cầu.
- **Load balancing kiểu NAT**: Keepalived có thể sử dụng **Network Address Translation (NAT)** để chuyển tiếp yêu cầu đến các máy chủ thực.

### 5. **Failover**
Khi một máy chủ chủ (Master) gặp sự cố và không thể tiếp nhận yêu cầu, Keepalived sẽ tự động chuyển quyền sở hữu VIP cho một máy chủ dự phòng (Backup) có **Priority cao**. Quá trình này diễn ra rất nhanh, đảm bảo rằng dịch vụ không bị gián đoạn.

- **Master node failure**: Nếu máy chủ Master không còn hoạt động, các máy chủ Backup sẽ tranh giành quyền sở hữu VIP. Máy chủ Backup có **Priority cao hơn** sẽ trở thành Master và tiếp nhận VIP.
- **Failback**: Khi máy chủ Master trở lại hoạt động, Keepalived có thể cho phép Master tiếp nhận lại VIP và trở thành máy chủ chính một lần nữa.

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


Cấu hình **Load Balancing** với **Keepalived** giúp phân phối tải đến các máy chủ backend một cách hiệu quả. Keepalived cung cấp khả năng cân bằng tải (load balancing) thông qua các thuật toán như **Round Robin**, **Weighted Round Robin**, và **Least Connections**. Dưới đây là hướng dẫn chi tiết về cách cấu hình **Load Balancing** trong **Keepalived**.

##### 1. **Cài Đặt Keepalived**

Trước tiên, hãy chắc chắn rằng **Keepalived** đã được cài đặt trên hệ thống của bạn:

```bash
sudo apt update
sudo apt install keepalived
```

##### 2. **Cấu Hình Load Balancing với Keepalived**

###### Cấu hình cơ bản cho Keepalived

Giả sử bạn có một địa chỉ IP ảo (VIP) là `172.16.1.100` và bạn có 2 máy chủ backend (real servers) có địa chỉ IP lần lượt là `172.16.1.200` và `172.16.1.201`. Bạn muốn sử dụng **Keepalived** để cân bằng tải HTTP trên cổng `80`.

**Cấu hình Keepalived (keepalived.conf)**:

```bash
vrrp_instance VI_1 {
    state MASTER                          # Trạng thái MASTER cho máy chủ chính
    interface ens33                        # Giao diện mạng
    virtual_router_id 51                   # ID của Virtual Router (phải giống trên máy chủ BACKUP)
    priority 101                           # Mức độ ưu tiên
    advert_int 1                           # Thời gian quảng bá trạng thái của router
    virtual_ipaddress {
        172.16.1.100                       # Địa chỉ VIP (Virtual IP)
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
        protocol TCP                        # Giao thức kết nối

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

##### 3. **Giải Thích Cấu Hình:**

- **`virtual_server 172.16.1.100 80`**:
  - Đây là địa chỉ IP ảo (VIP) mà các client sẽ kết nối vào (trong trường hợp này là `172.16.1.100`).
  - Cổng `80` là cổng mà dịch vụ web (HTTP) đang chạy.

- **`lb_algo rr`**:
  - Thuật toán cân bằng tải **Round Robin** (RR): Các yêu cầu sẽ được phân phối đều giữa các máy chủ backend theo vòng tròn.

- **`lb_kind NAT`**:
  - Sử dụng NAT (Network Address Translation) để điều hướng lưu lượng đến các máy chủ backend.

- **`persistence_timeout 50`**:
  - Thiết lập thời gian lưu kết nối (session persistence) trong 50 giây.

- **`real_server 172.16.1.200 80`**:
  - Cấu hình cho máy chủ backend đầu tiên (IP là `172.16.1.200` và cổng là `80`).
  - `weight 1`: Trọng số của máy chủ này. Các máy chủ có trọng số cao sẽ nhận được nhiều yêu cầu hơn.

- **`HTTP_GET`**:
  - **Health Check** cho máy chủ backend. Keepalived sẽ gửi một yêu cầu HTTP GET đến đường dẫn `/health_check` để kiểm tra tình trạng của máy chủ.
  - **`status_code 200`**: Mã trạng thái HTTP hợp lệ khi máy chủ hoạt động bình thường.
  - **`connect_timeout 10`**: Thời gian tối đa để kết nối với máy chủ backend.
  - **`nb_get_retry 3`**: Số lần thử lại nếu không nhận được phản hồi từ máy chủ backend.

##### 4. **Kiểm Tra Trạng Thái của Keepalived:**

Sau khi cấu hình xong, bạn cần kiểm tra trạng thái của **Keepalived** để đảm bảo dịch vụ đang chạy.

```bash
sudo systemctl status keepalived
```

##### 5. **Kiểm Tra IP Ảo (VIP) trên Giao Diện Mạng:**

Kiểm tra xem VIP đã được gán thành công trên giao diện mạng chưa:

```bash
ip a show ens33
```

Bạn sẽ thấy địa chỉ VIP (`172.16.1.100`) được gán vào giao diện mạng của máy chủ.

##### 6. **Kiểm Tra Cân Bằng Tải:**

Sau khi Keepalived đã được cấu hình và chạy, bạn có thể kiểm tra hoạt động của load balancing bằng cách sử dụng **curl** hoặc **wget** từ một máy khác để gửi yêu cầu đến VIP và kiểm tra các phản hồi từ các máy chủ backend.

```bash
curl http://172.16.1.100/health_check
```

Các yêu cầu sẽ được phân phối qua các máy chủ backend (real servers) theo thuật toán **Round Robin**.

**Lưu ý**: phải cài nginx

##### 7. **Kiểm Tra Failover và Redundancy:**

Nếu bạn muốn kiểm tra tính năng **failover**, bạn có thể tắt dịch vụ **Keepalived** trên máy chủ **Master**:

```bash
sudo systemctl stop keepalived
```

Sau khi dịch vụ trên máy chủ **Master** bị tắt, **Keepalived** sẽ chuyển VIP sang máy chủ **Backup**.

- Kiểm tra lại VIP và khả năng truy cập.
- Bật lại dịch vụ Keepalived trên máy chủ **Master** để xác nhận rằng VIP sẽ quay lại máy chủ **Master**.

##### 8. **Tóm Tắt Các Tham Số Quan Trọng:**

- **`virtual_server <VIP> <port>`**: Địa chỉ IP ảo và cổng dịch vụ cần cân bằng tải.
- **`real_server <IP> <port>`**: Các máy chủ backend.
- **`weight`**: Trọng số của các máy chủ backend.
- **`HTTP_GET`**: Cấu hình kiểm tra tình trạng sức khỏe (health check) của các máy chủ backend.
- **`lb_algo`**: Thuật toán cân bằng tải, ví dụ: `rr` (Round Robin), `wrr` (Weighted Round Robin), `lc` (Least Connections).
- **`lb_kind`**: Loại cân bằng tải, ví dụ: `NAT`, `DR` (Direct Routing).
