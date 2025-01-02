### **Khái niệm**

#### **1. Ansible là gì?**

- Là 1 công cụ mã nguồn mở dùng để tự động hóa việc quản lý cấu hình, triển khai ứng dụng.
- Ansible sử dụng các script đơn giản, dễ đọc, được gọi là playbook để tự động hóa các tác vụ.
- 1 Playbook bao gồm 1 hoặc nhiều play. Mỗi play ánh xạ một nhóm máy chủ (hosts) tới các tác vụ (tasks) cần thực hiện trên các máy chủ đó. Các play cũng xác định thứ tự thực hiện các tác vụ


#### **2. YAML**

##### **2.1 Cú pháp cơ bản của YAML:**

a. Dòng đầu tiên trong playbook phải bắt đầu bằng "---"
- Dấu ba gạch ngang này biểu thị sự bắt đầu của tài liệu YAML.

b. Danh sách trong YAML được biểu diễn bằng dấu gạch ngang (hyphen) theo sau là một khoảng trắng.
- Một playbook chứa danh sách các play và mỗi play được biểu diễn bằng ký hiệu "-".
- Mỗi play là một mảng liên kết (associative array), dictionary, hoặc map, sử dụng cặp key-value.

c. Thụt đầu dòng (Indentation) rất quan trọng.
- Tất cả các thành phần trong danh sách phải có cùng mức thụt đầu dòng.
- Các cặp key-value được phân tách bằng dấu ":"

d. Dùng để biểu thị các thành phần như hosts, variables, roles, tasks, v.v.



```yaml

---
- hosts: all
  remote_user: vagrant
  sudo: yes
  tasks:
    - name: Tạo nhóm devops
      group:
        name: devops
        state: present

    - name: Tạo người dùng devops với quyền admin
      user:
        name: devops
        comment: "Devops User"
        uid: 2001
        group: devops

    - name: Cài đặt gói htop
      action: apt name=htop state=present update_cache=yes

- hosts: www
  user: vagrant
  sudo: yes
  tasks:
    - name: Thêm kho lưu trữ Nginx chính thức
      apt_repository:
        repo: 'deb http://nginx.org/packages/ubuntu/ lucid nginx'

    - name: Cài đặt máy chủ web Nginx và đảm bảo ở phiên bản mới nhất
      apt:
        name: nginx
        state: latest

    - name: Khởi động dịch vụ Nginx
      service:
        name: nginx
        state: started

```

#### **2. 2 Inventory**

- Inventory: Nơi định nghĩa danh sách các hosts mà Ansible sẽ quản lý hoặc thực thi module lệnh.

**Các loại inventory:**

- Static inventory: là 1 file văn bản dạng `.ini` hoặc `.yaml`. Tệp mặc định của Ansible là `/etc/ansible/hosts`.
- Dynamic inventory: Dùng trong cloud hoặc nơi mà các host thay đổi thường xuyên.

a. Inventory sử dụng cấu trúc dạng INI:
- Inventory tuân theo kiểu cấu hình INI, bao gồm các khối cấu hình bắt đầu bằng tên nhóm hoặc lớp máy chủ được đặt trong `[ ]`.
- Điều này cho phép bạn thực thi tác vụ một cách chọn lọc trên các lớp hệ thống, ví dụ: `[namenodes]`.

b. Một máy chủ có thể thuộc nhiều nhóm:
- Một máy chủ có thể nằm trong nhiều nhóm khác nhau. Trong trường hợp này:
  - Các biến (variables) của máy chủ từ cả hai nhóm sẽ được gộp lại.
  - Nếu có xung đột biến, quy tắc thứ tự ưu tiên sẽ được áp dụng. (Chi tiết về biến và ưu tiên sẽ được giải thích sau).

c. Danh sách máy chủ và chi tiết kết nối trong mỗi nhóm:
- Mỗi nhóm chứa:
  - Danh sách máy chủ.
  - Thông tin kết nối như:
    - Người dùng SSH để kết nối.
    - Cổng SSH nếu không dùng cổng mặc định.
    - Thông tin xác thực SSH (mật khẩu, khóa SSH). 
    - Thông tin về quyền sudo, nếu cần.

d. Sử dụng mẫu tên máy chủ (hostname pattern):
- Tên máy chủ có thể sử dụng:
  - Glob pattern: Ký tự đại diện (như `*`).
  - Ranges: Phạm vi số (như `host[1:10]`).
- Điều này giúp bạn dễ dàng thêm nhiều máy chủ cùng loại có chung mẫu tên.

#### **2.3 Patterns**

![image](https://github.com/user-attachments/assets/ae577b95-ad33-4909-b27e-13e546a0a3ac)


**Giải thích các loại Patterns:**

1. **Tên nhóm (Group name):**  
   - Ví dụ: `namenodes` sẽ chọn tất cả các máy chủ thuộc nhóm `namenodes`.

2. **Tất cả (Match all):**  
   - Ví dụ: `all` hoặc `*` sẽ chọn tất cả các máy chủ trong inventory.

3. **Phạm vi (Range):**  
   - Ví dụ: `namenode[0:100]` sẽ chọn tất cả các máy chủ từ `namenode0` đến `namenode100`.

4. **Tên máy chủ hoặc địa chỉ máy chủ (Hostnames/hostname globs):**  
   - Ví dụ: `*.example.com` sẽ chọn tất cả các máy chủ có tên miền kết thúc bằng `.example.com`.

5. **Loại trừ (Exclusions):**  
   - Ví dụ: `namenodes:!secondarynamenodes` sẽ chọn tất cả máy chủ trong nhóm `namenodes`, ngoại trừ các máy chủ trong nhóm `secondarynamenodes`.

6. **Giao nhau (Intersection):**  
   - Ví dụ: `namenodes:&zookeeper` sẽ chọn những máy chủ nằm trong cả nhóm `namenodes` và `zookeeper`.

7. **Biểu thức chính quy (Regular expressions):**  
   - Ví dụ: `~(nn|zk).*\.example\.org` sẽ chọn tất cả máy chủ có tên bắt đầu bằng `nn` hoặc `zk` và kết thúc với `.example.org`.

#### **2.4 Tasks**

Mỗi play trong một playbook của Ansible ánh xạ một nhóm các máy chủ (được chọn bằng các mẫu) với một chuỗi các hành động, gọi là tasks. Các task này xác định các hành động cụ thể mà sẽ được thực hiện trên mỗi máy chủ trong nhóm.

Các task trong một play sẽ được thực thi tuần tự trên mỗi máy chủ khớp với mẫu hosts trong play.

**Cách mà Plays và Tasks hoạt động:**
- Play ánh xạ một nhóm máy chủ tới một chuỗi các tasks.
- Mỗi task sẽ được thực thi tuần tự trên mỗi máy chủ trong nhóm, đảm bảo rằng các hành động được thực hiện theo thứ tự.

##### **2.5 Modules** 

**Modules** là các quy trình đóng gói chịu trách nhiệm quản lý các thành phần hệ thống cụ thể trên các nền tảng nhất định.

Ví dụ về module:

- **apt**: Dùng cho Debian để quản lý các gói hệ thống.  
- **yum**: Dùng cho RedHat để quản lý các gói hệ thống.  
- **user**: Thêm, xóa hoặc chỉnh sửa người dùng trên hệ thống.  
- **service**: Khởi động/dừng các dịch vụ hệ thống.  

Chức năng của module:

- **Trừu tượng hóa**: Module giúp trừu tượng hóa các thao tác thực tế khỏi người dùng.  
- **Khai báo**: Người dùng chỉ cần khai báo trạng thái mong muốn của thành phần hệ thống (ví dụ: tên, trạng thái, UID, nhóm, shell, v.v.).  
- **Thực thi**: Các quy trình thực tế sẽ được Ansible xử lý thông qua module và chạy ở chế độ nền.  

Modules tương tự như **providers** trong các phần mềm như **Chef/Puppet**, nhưng Ansible chỉ yêu cầu bạn khai báo trạng thái thay vì viết các quy trình chi tiết.  


Module đặc biệt: `Command` và `Shell`

- Không nhận các cặp key-value làm tham số.  
- Không có tính **idempotence** (không đảm bảo trạng thái ổn định nếu lặp lại).  


Thư viện module:

- Ansible đi kèm với một thư viện module phong phú, bao gồm từ các module quản lý tài nguyên hệ thống cơ bản đến các module tích hợp cloud, gửi thông báo, v.v.  
- Bạn có thể sử dụng module để:
  - Khởi tạo instance EC2.
  - Tạo cơ sở dữ liệu trên PostgreSQL từ xa.
  - Nhận thông báo trên IRC.  

Ansible giúp bạn tiết kiệm công sức tích hợp với các nhà cung cấp cloud hoặc tìm kiếm plugin bên ngoài.

- Danh sách các module có sẵn: [Danh sách module Ansible](http://docs.ansible.com/list_of_all_modules.html).  


Mở rộng module:
- Nếu không tìm thấy module phù hợp, bạn có thể dễ dàng tạo một module mới.  
- Module này không nhất thiết phải viết bằng Python—bạn có thể viết bằng ngôn ngữ mà mình chọn.  

Chi tiết về cách phát triển module: [Phát triển module Ansible](http://docs.ansible.com/developing_modules.html).

**tính idempotence**  

Tính **idempotence** là một đặc điểm quan trọng của các module trong Ansible. Nó cho phép thực hiện cùng một tác vụ nhiều lần trên hệ thống nhưng luôn trả về kết quả nhất quán, không gây ra lỗi hoặc thay đổi không cần thiết.  

Nguyên tắc hoạt động:

Ví dụ, nếu bạn sử dụng module **apt** để cài đặt và đảm bảo Nginx luôn được cập nhật, thì các hành vi sẽ như sau:
1. **Lần chạy đầu tiên**:
   - Module apt sẽ so sánh trạng thái đã khai báo trong playbook với trạng thái hiện tại của gói trên hệ thống.
   - Nếu Nginx chưa được cài đặt, Ansible sẽ tiến hành cài đặt.
2. **Các lần chạy sau**:
   - Ansible sẽ bỏ qua bước cài đặt nếu phát hiện Nginx đã được cài đặt và không có bản cập nhật nào mới.
   - Nếu có phiên bản mới trong kho lưu trữ, Ansible sẽ tiến hành cập nhật.  

Lợi ích của tính idempotence:

- Giúp thực hiện cùng một tác vụ nhiều lần mà không gây lỗi.
- Đảm bảo trạng thái hệ thống luôn đồng nhất với định nghĩa trong playbook.  

Ngoại lệ:
Hầu hết các module trong Ansible đều có tính idempotence. **Tuy nhiên, module `command` và `shell` không idempotent**, do đó người dùng phải tự đảm bảo chúng không gây thay đổi không cần thiết nếu được chạy nhiều lần.  

Ví dụ YAML:
```yaml
- name: Install and update Nginx
  apt:
    name: nginx
    state: latest
```

Trong ví dụ trên:  
- Lần chạy đầu tiên: Ansible cài đặt Nginx nếu chưa có.  
- Lần chạy tiếp theo: Không làm gì nếu Nginx đã cài đặt và cập nhật.  


##### **2.6 Chạy playbook**

```bash
$ ansible-playbook simple_playbook.yml -i customhosts
```

Giải thích:

1. ansible-playbook
- Là lệnh để thực thi playbook.
- Nó nhận tên của playbook làm tham số và chạy các play được định nghĩa bên trong.

2. `simple_playbook.yml`

- Tên của file playbook chứa các plays đã được viết.
- Trong ví dụ này, file `simple_playbook.yml` có hai play:
  - Play thực hiện các tác vụ chung, ví dụ như tạo người dùng và nhóm.
  - Play cài đặt Nginx trên các máy chủ web.

3. `-i customhosts`
- Là tham số chỉ định tệp inventory tùy chỉnh, trong đó liệt kê các máy chủ hoặc nhóm máy chủ mà các play sẽ được thực thi.
- Trong trường hợp này, tệp customhosts chứa danh sách các máy chủ và thông tin kết nối.

Kết quả:

Khi chạy lệnh trên, Ansible sẽ thực hiện các bước sau:
- Gọi các play được khai báo trong playbook theo thứ tự đã mô tả.
- Kết nối tới các máy chủ trong tệp inventory (customhosts).
- Thực hiện tuần tự từng tác vụ trong từng play trên các máy chủ đã chọn.

![image](https://github.com/user-attachments/assets/65acdb1f-ab98-48d8-838a-834b21995bb6)

**Phân tích những gì đã xảy ra khi chạy Playbook:**

- **Ansible đọc playbook được chỉ định** làm tham số của lệnh `ansible-playbook` và bắt đầu thực thi các play theo thứ tự đã định.

- **Play đầu tiên chạy trên tất cả các host:**  
  - Từ khóa `all` là một mẫu đặc biệt sẽ khớp với tất cả các host (tương tự như ký tự đại diện `*`).  
  - Do đó, các tác vụ trong play đầu tiên sẽ được thực thi trên tất cả các host có trong tệp inventory được truyền vào làm tham số.  

- **Gathering Facts:**  
  - Trước khi chạy bất kỳ tác vụ nào, Ansible thu thập thông tin về các hệ thống mà nó sẽ cấu hình. Thông tin này được gọi là **facts**.

- **Tác vụ trong play đầu tiên:**  
  - Play này bao gồm việc tạo nhóm `devops`, tạo người dùng `devops`, và cài đặt gói `htop`.  
  - Vì có ba host trong inventory, bạn sẽ thấy một dòng thông báo trạng thái cho mỗi host.  
    - Nếu trạng thái của thực thể không thay đổi, sẽ hiển thị `ok`.
    - Nếu có thay đổi, sẽ hiển thị `changed`.

- **Chuyển sang play tiếp theo:**  
  - Play thứ hai chỉ thực thi trên một host vì nó được định nghĩa với `hosts:www`.  
  - Inventory chỉ chứa một host thuộc nhóm `www`.  

- **Tác vụ trong play thứ hai:**  
  - Thêm kho lưu trữ của Nginx.  
  - Cài đặt gói Nginx.  
  - Khởi động dịch vụ Nginx.  

- **PLAY RECAP:**  
  - Sau khi hoàn thành tất cả các play, Ansible in ra bản tóm tắt kết quả.  
  - Bản tóm tắt này cho biết:  
    - Số lượng thay đổi đã thực hiện.  
    - Các host không thể kết nối.  
    - Các hệ thống xảy ra lỗi khi thực thi.  

-----------------------------------------------

### **3. Role**
- Là các thư mục được sắp xếp theo cấu trúc chuẩn. Tuân thủ các quy ước về bố cục thư mục mỗi thành phần nằm trong vị trí thích hợp.

```plaintext
roles/
└── nginx/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    │   └── main.yml
    ├── templates/
    │   └── nginx.conf.j2
    ├── files/
    │   └── static_file.txt
    ├── vars/
    │   └── main.yml
    ├── defaults/
    │   └── main.yml
    ├── meta/
    │   └── main.yml
    └── tests/
        ├── inventory
        └── test.yml
```

**Cách tổ chức thư mục cho vai trò (Roles) trong Ansible**

Roles thực chất là các thư mục được sắp xếp theo cấu trúc chuẩn. Chúng tuân thủ các quy ước về bố cục thư mục và kỳ vọng mỗi thành phần nằm trong vị trí thích hợp. Dưới đây là chi tiết cấu trúc thư mục và vai trò của từng thành phần:  

---

### **Ví dụ về cấu trúc thư mục của vai trò "Nginx":**
```plaintext
roles/
└── nginx/
    ├── tasks/
    │   └── main.yml
    ├── handlers/
    │   └── main.yml
    ├── templates/
    │   └── nginx.conf.j2
    ├── files/
    │   └── static_file.txt
    ├── vars/
    │   └── main.yml
    ├── defaults/
    │   └── main.yml
    ├── meta/
    │   └── main.yml
    └── tests/
        ├── inventory
        └── test.yml
```

1. **Tên thư mục role:**
   - Mỗi role có một thư mục với tên của nó (ví dụ: `nginx`).
   - Thư mục cha luôn là `roles/`.

2. **Thư mục con thường dùng:**
   - **`tasks/`:**
     - Chứa logic chính, như cài đặt gói, khởi động dịch vụ, quản lý tệp.
     - Mỗi thư mục `tasks/` thường có tệp mặc định là `main.yml`.
     - Đây là **"nhân vật chính"** của vai trò.

   - **`handlers/`:**
     - Kích hoạt các hành động dựa trên sự thay đổi trạng thái, ví dụ: khởi động lại dịch vụ sau khi tệp cấu hình thay đổi.

   - **`templates/`:**
     - Quản lý các tệp cấu hình động.
     - Sử dụng biến để tạo nội dung tệp cấu hình, ví dụ: `nginx.conf.j2`.

   - **`files/`:**
     - Chứa các tệp tĩnh, như trình cài đặt ứng dụng hoặc tệp văn bản cố định, để sao chép vào máy đích.

   - **`vars/` và `defaults/`:**
     - **`vars/`:** Định nghĩa biến cụ thể cho vai trò.
     - **`defaults/`:** Định nghĩa các giá trị mặc định (có thể ghi đè).

   - **`meta/`:**
     - Chứa siêu dữ liệu của role, như các vai trò phụ thuộc.

   - **`tests/`:**
     - Dùng để kiểm thử role, bao gồm tệp inventory và playbook kiểm thử.

-----------------------------------------

### **4. Jinja2**

- Jinja2 là 1 template engine dựa trên Python. 

**Hình thành Template**

Templates trông rất giống với các file văn bản thông thường, ngoại trừ việc chứa các **biến** hoặc **mã lệnh** được bao quanh bởi các thẻ đặc biệt. Những thẻ này sẽ được xử lý và thay thế bằng giá trị thực tại thời điểm chạy (runtime), tạo thành một file văn bản hoàn chỉnh, sau đó được sao chép đến máy đích.


**Hai loại thẻ trong template Jinja2**:

1. **Thẻ `{{ }}`**:
   - Dùng để **chèn biến** vào trong template và in giá trị của biến đó vào file kết quả.
   - Đây là cách sử dụng phổ biến nhất của template.
   - **Ví dụ**:  
     ```jinja
     {{ nginx_port }}
     ```
     Trong file kết quả, thẻ này sẽ được thay thế bằng giá trị của biến `nginx_port`.

2. **Thẻ `{% %}`**:
   - Dùng để **chèn các câu lệnh** vào trong template, như vòng lặp hoặc câu lệnh điều kiện `if-else`.
   - Những câu lệnh này được đánh giá tại runtime nhưng **không được in ra** file kết quả.
   - **Ví dụ**:  
     ```jinja
     {% if environment == 'production' %}
     server_name production.example.com;
     {% else %}
     server_name staging.example.com;
     {% endif %}
     ```
     Trong file kết quả, chỉ dòng `server_name` tương ứng với điều kiện sẽ xuất hiện, còn các thẻ `{% %}` sẽ không được in ra.

#### **4.1 Facts và Variables**

**Facts và Variables (Biến)**

Sau khi đã tìm hiểu về mã lệnh trong các template Jinja2, chúng ta sẽ tìm hiểu nguồn dữ liệu được chèn vào template trong quá trình runtime. Dữ liệu này có thể xuất phát từ **facts** hoặc **variables**.



**Facts và Variables là gì?**

- **Facts**:  
  - Là một loại biến, nhưng được tự động **phát hiện** và cung cấp sẵn tại thời điểm runtime.
  - Facts chứa thông tin hệ thống của máy chủ đích, ví dụ như địa chỉ IP, tên máy chủ, thông tin về hệ điều hành, và nhiều thông tin khác.
  - Ansible tự động thu thập các facts thông qua việc "gathering facts" khi bắt đầu thực thi một playbook.

- **Variables (Biến)**:  
  - Là dữ liệu được **định nghĩa bởi người dùng**, dùng để cung cấp thông tin cụ thể cho playbook hoặc template.
  - Biến được khai báo trong các file, như `group_vars`, `host_vars`, playbook, hoặc thậm chí từ dòng lệnh khi chạy Ansible.


**Sự khác biệt giữa Facts và Variables**

| **Thuộc tính**     | **Facts**                                   | **Variables**                        |
|---------------------|--------------------------------------------|---------------------------------------|
| **Nguồn gốc**       | Tự động được Ansible phát hiện.            | Người dùng định nghĩa.               |
| **Thời điểm tạo**   | Tại runtime (trong quá trình "gather facts"). | Trước hoặc trong khi chạy playbook.  |
| **Ví dụ**           | `ansible_facts['os_family']`, `ansible_default_ipv4['address']` | `nginx_port`, `app_user`, `log_path` |


**Sử dụng trong Jinja2 Template**

Cả facts và variables đều có thể được sử dụng trong template Jinja2 theo cùng một cách:

1. **Ví dụ sử dụng facts**:  
   ```jinja
   OS family: {{ ansible_facts['os_family'] }}
   Default IP: {{ ansible_default_ipv4['address'] }}
   ```

2. **Ví dụ sử dụng variables**:  
   ```jinja
   Nginx Port: {{ nginx_port }}
   Log Path: {{ log_path }}
   ```

##### **a. Facts**

**Automatic variables – facts (biến tự động)**
Nhiều dữ liệu trong hệ thống của chúng ta được tự động phát hiện và cung cấp cho Ansible bởi các máy chủ được quản lý trong quá trình kết nối. Dữ liệu này rất hữu ích và cung cấp cho chúng ta mọi thông tin về hệ thống, chẳng hạn như:
- Tên máy chủ, giao diện mạng, và địa chỉ IP
- Kiến trúc hệ thống
- Hệ điều hành
- Các ổ đĩa
- Bộ xử lý và dung lượng bộ nhớ
- Liệu hệ thống có phải là máy ảo hay không; nếu có, nó là một nhà cung cấp ảo hóa/cloud nào?

Các facts được thu thập ngay từ đầu khi Ansible chạy. Bạn sẽ thấy dòng thông báo "GATHERING FACTS *******" trong kết quả khi điều này xảy ra.

Có thể xem các facts về hệ thống bằng cách chạy lệnh sau cùng với một phần kết quả ngắn gọn:

```bash
$ ansible -i customhosts www -m setup | less
```

##### **b. Variables**
