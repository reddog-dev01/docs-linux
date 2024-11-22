### **1. Set static IP, DNS, GATEWAY**

**1.1 Cấu hình ip động**

1. Kiểm tra tên interface mạng
```
ip link show
```
2. Kiểm tra quyền file xem được truy cập hay không
```
ls /etc/netplan/
```
3. Sửa file cấu hình
```
sudo vim /etc/netplan/01-netcfg.yaml
```
```
network:
  version: 2
  ethernets:
    ens33: # Thay 'ens33' bằng tên interface mạng của bạn
      dhcp4: true
```
4. Áp dụng cấu hình
```
sudo netplan apply
```
5. Kiểm tra IP được cấp và ping kết nối
```
ip addr show ens33
```
6. 
