mô hình log ELK
- Nó là gì? Làm gì? Làm như thế nào?
- Chức năng nhiệm vụ của từng thành phần
- Mô hình kết nối
- Các vấn đề cần lưu ý khi xây dựng hệ thống này
- Dựng cụm lab để setup được mô hình trên

### **1. ELK là gì?**

Là từ viết tắt của bộ công cụ bao gồm 3 dự án Elasticsearch, Logstash, Kibana. Sử dụng cùng với nhau để 

![image](https://github.com/user-attachments/assets/26eae5a0-9d4c-494a-ace9-d80bb9a272cf)

Được sử dụng để tổng hợp nhật ký từ tất cả các hệ thống và ứng dụng, phân tích chúng và tạo trực quan hóa dữ liệu để giám sát, xử lý sự cố nhanh hơn, phân tích bảo mật...

#### **1.1 Elasticsearch**
 
Elasticsearch là 1 công cụ tìm kiếm (search engine) và phân tích dữ liệu. Được xây dựng bằng Java, với giao diện HTTP có hỗ trợ JSON.

##### **a. Các thành phần của Elasticsearch**


