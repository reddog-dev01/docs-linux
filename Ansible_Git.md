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
