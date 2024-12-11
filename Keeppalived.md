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

**VRRP** cho phép nhiều router cùng chia sẻ một địa chỉ IP ảo (VIP). Nếu máy chủ chính gặp sự cố, máy chủ dự phòng sẽ tiếp nhận và duy trì VIP, giúp dịch vụ không bị gián đoạn.

###### **Cấu Hình Keepalived trên Máy Chủ Master**

Đây là máy chủ sẽ có địa chỉ IP ảo (VIP) khi hệ thống hoạt động bình thường.

1. Mở tệp cấu hình Keepalived:

```bash
sudo nano /etc/keepalived/keepalived.conf
```

2. Cấu hình VRRP cho máy chủ Master:

```bash
vrrp_instance VI_1 {
    state MASTER                  # Trạng thái MASTER cho máy chủ chính
    interface eth0                # Giao diện mạng mà VIP sẽ được gán (thay eth0 nếu cần)
    virtual_router_id 51          # ID của Virtual Router (phải giống trên tất cả các máy chủ)
    priority 101                  # Mức độ ưu tiên (máy chủ có priority cao hơn sẽ là Master)
    advert_int 1                  # Thời gian quảng bá trạng thái của router (đơn vị giây)
    virtual_ipaddress {
        192.168.1.100             # Địa chỉ IP ảo (VIP)
    }
    authentication {
        auth_type PASS            # Loại xác thực (có thể là PASS hoặc AH)
        auth_pass 1234            # Mật khẩu xác thực (phải giống trên máy chủ Backup)
    }
}
```

###### **Cấu Hình Keepalived trên Máy Chủ Backup**

Máy chủ Backup sẽ lấy VIP nếu máy chủ Master gặp sự cố.

1. Mở tệp cấu hình Keepalived:

```bash
sudo nano /etc/keepalived/keepalived.conf
```

2. Cấu hình VRRP cho máy chủ Backup:

```bash
vrrp_instance VI_1 {
    state BACKUP                 # Trạng thái BACKUP cho máy chủ dự phòng
    interface eth0               # Giao diện mạng mà VIP sẽ được gán (thay eth0 nếu cần)
    virtual_router_id 51         # ID của Virtual Router (phải giống trên máy chủ Master)
    priority 90                  # Mức độ ưu tiên thấp hơn máy chủ chính
    advert_int 1                 # Thời gian quảng bá trạng thái của router (đơn vị giây)
    virtual_ipaddress {
        192.168.1.100            # Địa chỉ IP ảo (VIP)
    }
    authentication {
        auth_type PASS           # Loại xác thực (phải giống trên máy chủ Master)
        auth_pass 1234           # Mật khẩu xác thực (phải giống trên máy chủ Master)
    }
}
```

#### 3. **Cấu Hình Health Check cho Load Balancing (Optional)**

Nếu bạn muốn thực hiện **Load Balancing** và kiểm tra sức khỏe của các máy chủ thực, bạn cần cấu hình thêm phần này.

Ví dụ, cấu hình để sử dụng **HTTP Health Checks**:

```bash
virtual_server 192.168.1.100 80 {
    delay_loop 6                # Thời gian chờ giữa các lần kiểm tra
    lb_algo rr                  # Thuật toán cân bằng tải (Round Robin)
    lb_kind NAT                 # Loại cân bằng tải (NAT)
    persistence_timeout 50      # Thời gian duy trì phiên làm việc cho client
    protocol TCP                # Giao thức (TCP hoặc UDP)

    real_server 192.168.1.101 80 {
        weight 1                 # Trọng số của máy chủ thực
        HTTP_GET {
            url {
                path /health_check
                digest 123456    # Kiểm tra sức khỏe qua mã băm
            }
        }
    }

    real_server 192.168.1.102 80 {
        weight 1
        HTTP_GET {
            url {
                path /health_check
                digest 654321
            }
        }
    }
}
```

#### 4. **Khởi Động Dịch Vụ Keepalived**

Sau khi đã cấu hình xong **keepalived.conf**, bạn cần khởi động lại dịch vụ **Keepalived** trên các máy chủ.

- **Khởi động Keepalived**:

```bash
sudo systemctl start keepalived
```

- **Kích hoạt Keepalived tự động khởi động khi máy chủ khởi động lại**:

```bash
sudo systemctl enable keepalived
```

- **Kiểm tra trạng thái Keepalived**:

```bash
sudo systemctl status keepalived
```

#### 5. **Kiểm Tra Tính Năng Failover và Load Balancing**

- **Kiểm tra Failover**: Bạn có thể tắt máy chủ **Master** và kiểm tra xem liệu máy chủ **Backup** có tự động tiếp nhận VIP và trở thành máy chủ chính hay không.

  - **Tắt máy chủ Master**: Bạn có thể tắt dịch vụ Keepalived hoặc ngắt kết nối mạng trên máy chủ Master.
  - **Kiểm tra máy chủ Backup**: Xác nhận rằng máy chủ Backup đã trở thành Master và tiếp nhận VIP.

- **Kiểm tra Load Balancing**: Bạn có thể gửi yêu cầu đến VIP và kiểm tra xem các máy chủ thực có nhận yêu cầu phân phối đều hay không.

#### 6. **Xem Log để Kiểm Tra Tình Trạng**

Nếu có bất kỳ vấn đề nào xảy ra trong quá trình cấu hình, bạn có thể xem log của Keepalived để kiểm tra.

```bash
sudo journalctl -u keepalived
```

Hoặc xem log chi tiết trong tệp **/var/log/syslog**.

```bash
sudo tail -f /var/log/syslog
```


