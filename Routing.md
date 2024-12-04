### **1. Giao thức định tuyến (Routing Protocol)**

**Giao thức định tuyến** (Routing Protocol) là một tập hợp các quy tắc, quy trình và phương pháp mà các router hoặc thiết bị mạng sử dụng để quyết định con đường tối ưu (tuyến đường) để chuyển tiếp các gói tin từ nguồn 
đến đích trong mạng máy tính. Các giao thức này cho phép các router trao đổi thông tin về các tuyến đường khả dụng, từ đó cập nhật và duy trì bảng định tuyến của mình để đảm bảo dữ liệu được gửi đến đúng đích qua con đường tối ưu.

**Lý do cần giao thức định tuyến:**
- **Tối ưu hóa lưu lượng mạng**: Giao thức định tuyến giúp các router chọn lựa con đường tối ưu cho việc chuyển tiếp gói tin, từ đó giảm độ trễ và tăng hiệu suất mạng.
- **Khả năng phục hồi và chịu lỗi**: Khi một liên kết mạng bị hỏng, giao thức định tuyến có thể giúp tìm ra con đường thay thế để đảm bảo sự tiếp tục của việc truyền tải dữ liệu.
- **Quản lý mạng động**: Mạng máy tính không phải lúc nào cũng có cấu trúc cố định. Giao thức định tuyến giúp mạng thích nghi với sự thay đổi của cấu trúc mạng, thêm hoặc bớt các router, liên kết mới mà không cần cấu hình thủ công.
- **Khả năng mở rộng**: Khi mạng phát triển lớn hơn, các giao thức định tuyến giúp quản lý các tuyến đường và duy trì hiệu suất mạng mà không cần điều chỉnh thủ công.

**1.1 Định tuyến tĩnh (Static Routing)**

- phương pháp định tuyến trong đó các tuyến đường được cấu hình thủ công và không thay đổi trừ khi người quản trị mạng thay đổi chúng. Các router sử dụng bảng định tuyến tĩnh để chuyển tiếp gói tin từ nguồn đến đích dựa trên các tuyến đường mà quản trị viên đã chỉ định.

**Đặc điểm của Định tuyến Tĩnh**

- **Cấu hình thủ công**: Tất cả các tuyến đường phải được cấu hình thủ công, tức là người quản trị phải xác định các tuyến đường từ mỗi router tới các mạng khác trong hệ thống.
- **Không thay đổi tự động**: Bảng định tuyến tĩnh không tự động thay đổi khi có sự thay đổi trong mạng, ví dụ như khi một liên kết bị hỏng hoặc khi có sự thay đổi trong cấu trúc mạng.
- **Tính ổn định**: Định tuyến tĩnh cung cấp sự ổn định cao vì không có sự thay đổi tự động, phù hợp với các mạng không có sự thay đổi thường xuyên.

**Ưu điểm của Định tuyến Tĩnh**
- **Đơn giản và dễ quản lý**: Trong các mạng nhỏ và không thay đổi, việc cấu hình định tuyến tĩnh rất dễ dàng và dễ kiểm soát.
- **Tiết kiệm tài nguyên**: Không cần nhiều tài nguyên hệ thống vì không có quá trình tính toán phức tạp như trong định tuyến động.
- **Hiệu suất cao**: Định tuyến tĩnh giúp tiết kiệm băng thông và giảm tải cho router vì không cần trao đổi thông tin định tuyến giữa các router.
- **Bảo mật**: Vì không có giao thức định tuyến động để truyền tải thông tin định tuyến, định tuyến tĩnh có thể an toàn hơn trong các môi trường mạng nhỏ và có mức độ bảo mật cao.

**Nhược điểm của Định tuyến Tĩnh**
- **Không linh hoạt**: Khi có sự thay đổi trong mạng (như một liên kết bị hỏng), quản trị viên phải cập nhật lại cấu hình thủ công. Điều này có thể làm mạng không khả dụng tạm thời cho đến khi thay đổi được thực hiện.
- **Khó mở rộng**: Trong các mạng lớn, việc cấu hình và duy trì định tuyến tĩnh trở nên khó khăn và mất thời gian, vì mỗi router cần được cấu hình riêng biệt.
- **Không hỗ trợ tính năng phục hồi tự động**: Nếu một liên kết bị hỏng, các router không thể tự động tìm ra tuyến đường thay thế, yêu cầu người quản trị can thiệp.

**Ứng dụng của Định tuyến Tĩnh**
- **Mạng nhỏ hoặc đơn giản**: Định tuyến tĩnh thường được sử dụng trong các mạng nhỏ, nơi cấu trúc mạng không thay đổi nhiều và không cần tính linh hoạt.
- **Mạng với các liên kết cố định**: Trong các môi trường có các kết nối mạng cố định, không có thay đổi lớn trong cấu trúc mạng, định tuyến tĩnh sẽ giúp giảm tải cho các router.
- **An ninh và kiểm soát**: Định tuyến tĩnh có thể được sử dụng trong các mạng yêu cầu kiểm soát chặt chẽ hơn về cách thức các gói tin đi qua mạng, ví dụ như trong các tổ chức yêu cầu tính bảo mật cao.

**Khi nào nên sử dụng Định tuyến Tĩnh?**
- **Mạng nhỏ**: Nếu bạn quản lý một mạng nhỏ với ít router và không có nhiều thay đổi, định tuyến tĩnh là một lựa chọn phù hợp.
- **Mạng ổn định**: Khi các kết nối trong mạng không thay đổi thường xuyên và không có sự thay đổi lớn trong cấu trúc mạng.
- **Yêu cầu bảo mật cao**: Định tuyến tĩnh giúp ngăn ngừa việc chia sẻ thông tin định tuyến qua các giao thức động, làm cho mạng an toàn hơn.
- **Mạng với yêu cầu kiểm soát nghiêm ngặt**: Định tuyến tĩnh cho phép người quản trị kiểm soát chính xác các tuyến đường và cách thức các gói tin được chuyển tiếp.

- Định tuyến tĩnh bảo mật cao vì không trao đổi thông tin (địa chỉ mạng, gateway, đoạn đường...) giữa các router. Mỗi router chỉ biết tuyến đường mà nó đã được cấu hình cụ thể. 

**1.2 Định tuyến động (Dynamic Routing)**
Định tuyến động là phương pháp mà các router sử dụng giao thức định tuyến để tự động trao đổi thông tin và xác định các tuyến đường tối ưu. Các giao thức định tuyến động chia sẻ thông tin giữa các router, giúp tự động cập nhật bảng định tuyến.
