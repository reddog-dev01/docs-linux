### **Khái niệm**

#### **1. Ansible là gì?**

- Là 1 công cụ mã nguồn mở dùng để tự động hóa việc quản lý cấu hình, triển khai ứng dụng.
- Ansible sử dụng các script đơn giản, dễ đọc, được gọi là playbook để tự động hóa các tác vụ.
- 1 Playbook bao gồm 1 hoặc nhiều play. Mỗi play ánh xạ một nhóm máy chủ (hosts) tới các tác vụ (tasks) cần thực hiện trên các máy chủ đó. Các play cũng xác định thứ tự thực hiện các tác vụ
#### **2. YAML**

Cú pháp cơ bản của YAML:

a. Dòng đầu tiên trong playbook phải bắt đầu bằng "---"
- Dấu ba gạch ngang này biểu thị sự bắt đầu của tài liệu YAML.

b. Danh sách trong YAML được biểu diễn bằng dấu gạch ngang (hyphen) theo sau là một khoảng trắng.
- Một playbook chứa danh sách các play và mỗi play được biểu diễn bằng ký hiệu "-".
- Mỗi play là một mảng liên kết (associative array), dictionary, hoặc map, sử dụng cặp key-value.

c. Thụt đầu dòng (Indentation) rất quan trọng.
- Tất cả các thành phần trong danh sách phải có cùng mức thụt đầu dòng.
- Các cặp key-value được phân tách bằng dấu ":"

d. Dùng để biểu thị các thành phần như hosts, biến số, vai trò, tác vụ, v.v.
