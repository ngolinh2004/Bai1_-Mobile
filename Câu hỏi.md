
## G. Câu hỏi về bài làm?
1. Tại sao phải dùng Nginx làm Reverse Proxy mà không trỏ thẳng Tunnel vào Node-RED?

Vì Nginx đóng vai trò Reverse Proxy, còn Node-RED chỉ là công cụ xử lý logic.

🔹 Lý do:

- Node-RED không tối ưu để public trực tiếp ra Internet
- Không hỗ trợ:
  + quản lý nhiều route (/, /api, /admin)
  + caching
  + bảo mật nâng cao
🔹 Nginx làm được:

- Điều hướng request:
  + / → web tĩnh
  + /api → Node-RED / Flask
- Ẩn backend (Node-RED không bị lộ)
- Tăng hiệu năng và bảo mật
2. Sự khác biệt giữa việc Mount file và Mount thư mục trong Docker là gì?
  
- Mount file là việc ánh xạ một file cụ thể từ máy host vào container. Khi đó, container chỉ truy cập và sử dụng đúng file đó. Cách này thường dùng cho các file cấu hình (ví dụ như nginx.conf) để đảm bảo container chạy theo cấu hình đã định sẵn.
- Mount thư mục là việc ánh xạ toàn bộ một thư mục từ máy host vào container. Khi đó, tất cả các file bên trong thư mục sẽ được chia sẻ và đồng bộ giữa host và container. Cách này thường dùng cho dữ liệu hoặc mã nguồn (ví dụ như thư mục chứa website) để khi thay đổi trên máy host thì container cập nhật ngay
  
3. Nếu thay đổi file index.html ở máy Ubuntu, nội dung trên web có thay đổi ngay không? Tại sao?

- CÓ : thay đổi ngay lập tức
- Vì:
  + Docker sử dụng volume (mount)
  + File trên máy Ubuntu = file trong container
    
4. docker-compose.yml khai báo các services có phần restart: always hoặc restart: unless-stopped : chúng để làm gì?

* restart: always
  - Container luôn tự chạy lại
  - Kể cả khi:
     + bị crash
     + reboot máy

* restart: unless-stopped
  - Chạy lại trừ khi bạn stop thủ công
    
5. Cách khai báo để tất cả các services đều dùng chung 1 network? lợi ích của việc khai báo này là gì? Sửa đổi file docker-compose để tất cả các service đều dùng chung 1 network.

* Cách khai báo :
  - Bước 1: Khai báo network ở cuối file:
    
    networks:
    
     mynetwork:
  - Bước 2: Gán network cho từng service:
    
    networks:
    
      - mynetwork
* Lợi ích :
  - Giao tiếp giữa các container dễ dàng : Các service có thể gọi nhau bằng tên service
  - Tăng bảo mật
    + Chỉ các container trong cùng network mới truy cập được nhau
    + Không bị lộ ra bên ngoài
  - Dễ quản lý và mở rộng
    + Không cần nhớ địa chỉ IP
    + Khi thêm service mới chỉ cần gán vào network
  - Ổn định hơn
    + Docker tự quản lý kết nối nội bộ
    + Tránh lỗi thay đổi IP
      
6. Tìm cách đưa Cloudflare Token vào trong file .env rồi sau đó thêm .env vào file .gitignore trước khi push code lên github. Tại sao nói đây là điều quan trọng về bảo mật mã nguồn?

* Cách thực hiện
  - Bước 1: Tạo file .env
  - Bước 2: Sử dụng trong docker-compose.yml
  - Bước 3: Thêm .env vào .gitignore
* Tại sao điều này quan trọng về bảo mật?

  - Vì Cloudflare Token thuộc Cloudflare là thông tin nhạy cảm, có quyền truy cập vào hệ thống.
    
7. Tại sao chúng ta nên thêm hậu tố :ro khi mount file cấu hình Nginx?
* Lý do nên sử dụng
  - Bảo vệ file cấu hình
    + Tránh việc container hoặc ứng dụng bên trong tự ý thay đổi cấu hình
    + Giữ cấu hình luôn đúng như thiết lập ban đầu
  - Tăng bảo mật
    + Nếu container bị tấn công, kẻ xấu cũng không thể sửa file cấu hình
    + Giảm nguy cơ bị chèn mã độc hoặc thay đổi cấu hình server
  - Đảm bảo tính ổn định
    + Tránh lỗi do ghi đè file cấu hình
    + Hệ thống hoạt động ổn định hơn
  - Kiểm soát tốt hơn từ phía host
    + Mọi thay đổi phải thực hiện từ máy Ubuntu (host)
    + Dễ quản lý và kiểm soát phiên bản cấu hình
8. Khi dùng Cloudflare Tunnel: có cần thiết phải mở cổng cho các service nữa không?

- Khi sử dụng Cloudflare Tunnel của Cloudflare, không cần thiết phải mở cổng (port) cho các service trên server.

* Giải thích
  
Thông thường, khi triển khai web:
  - Ta phải mở các cổng như:
    + 80 (HTTP)
    + 443 (HTTPS)
  - Để người dùng từ Internet có thể truy cập trực tiếp vào server
