# Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421
## A. Đăng ký tên miền xịn cho cá nhân:
1. Đăng ký domain xịn (có thể dùng của mắt bão, tên miền *.id.vn đang miễn phí cho mọi công dân việt nam <= 23 tuổi, *.io.vn : giá 30k vnđ/năm)
   <img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/40fe05f5-bf9a-4c7c-ae67-42a49b501f0c" />

2. Đăng ký tài khoản cloudflare
3. Thêm domain đã đăng ký vào trong cloudflare : Nhận 2 dòng namespace
4. Nhập 2 dòng namespace của cloudflare vào trong trang quản lý DNS record của tên miền đăng ký (vd trên mắt bão)
## B. Cài đặt Ubuntu + Docker
1. Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
- Sử dụng một trong các công cụ để giả lập: HyperV (có sẵn của windows), VirutualBox (Miễn phí), VM_Ware (bản quyền)
- Download file iso để cài đặt.
- Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows
* Ví dụ:
- để ssh tới ubuntu ở ip 192.168.100.123, user là admin thì mở CMD trên windows,
- gõ lệnh: ssh admin@192.168.100.123
- hệ thống sẽ yêu cầu nhập password (chú ý : password sẽ không hiện ra)
- sau khi login thành công sẽ thấy màn hình chào hỏi của ubuntu
2. Tìm hiểu các lệnh cơ bản của ubuntu
  * Các lệnh cần tìm hiểu:

- Liệt kê các file trong thư mục: ls
- Tạo thư mục: mkdir nameFolder
- Chuyển thư mục làm việc: cd path
- Copy file: cp file_nguồn path/file_đích
- Thay đổi quyền thao tác file: sudo chmod xxx filename
- Edit file: sudo nano tenfile
  + CTRL+o : lưu nội dung sau khi edit
  + CTRL+x : thoát edit file
- Xem ip của máy ubuntu: ip -4 addr
3. Cài đặt docker cho Ubuntu
4. Kiểm tra phiên bản docker vừa cài đặt, kiểm tra phiên bản của docker compose
5. Cấu hình để docker chạy mà không cần tiền tố sudo
6. Tìm hiểu tập lệnh của docker và docker compose
7. Đảm bảo tường lửa trên Ubuntu đã cho phép các cổng 80, 1880, 9630 (Lệnh: sudo ufw allow ...)
## C. Cấu hình docker compose:
1. Tạo thư mục: ~/myapp
2. Chuyển vào trong thư mục ~/myapp
3. Tạo thư mục: ./myweb
4. Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)
5. Tạo file docker-compose.yml để nó sẽ có các dịch vụ sau:
- Khai báo sử dụng nodered/node-red, cổng 1880, dữ liệu nằm tại thư mục ./nodered
- Khai báo sử dụng nginx, cổng 80, cấu hình trong file ./nginx/nginx.conf
- Mount thư mục ./myweb thành thư mục /myweb trong nginx
- Mount file ./nginx/nginx.conf vào file /etc/nginx/nginx.conf trong nginx
6. Edit file ./nginx/nginx.conf để:
- Cấu hình web server cổng 80
- server_name là sub-domain (sub-domain tuỳ ý của em)
- location / trỏ tới root là thư mục /myweb
- location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered
7. Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập
Chạy docker-compose lần đầu để Node-RED tự sinh file cấu hình trong thư mục ./nodered, sau đó mới tiến hành sửa settings.js và restart lại container

## D. (Bonus - không bắt buộc)
1. tạo thư mục ./myapi
2. tạo file ./myapi/app.py sử dụng Python + Flask để làm gì đó funny
3. tạo file ./myapi/requirements.txt chứa các thư viện mà app.py sử dụng (theo như app.py ví dụ thì requirements.txt chỉ cần có nội dung: flask)
4. tạo file ./myapi/Dockerfile để khai báo sử dụng Python 3.9 slim
 ### Sử dụng phiên bản Python nhẹ (alpine) để giảm dung lượng image
 FROM python:3.9-slim

 ### Thiết lập thư mục làm việc bên trong container
 WORKDIR /app

 ### Sao chép file requirements vào và cài đặt thư viện
 COPY requirements.txt .
 RUN pip install --no-cache-dir -r requirements.txt

 ### Sao chép toàn bộ mã nguồn vào container
 COPY . .

 ### Thông báo container sẽ chạy ở cổng 9630
 EXPOSE 9630

 ### Lệnh khởi chạy ứng dụng
 CMD ["python", "app.py"]
5. Sửa đổi docker-compose để sử dụng myapp (xem phần tham khảo ở dưới)
6. Sửa đổi nginx/nginx.conf để /api trỏ tới service myapp cổng 9630
E. Triển khai (level test) ứng dụng
1. Chuyển vào trong thư mục ~/myapp
2. Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
- Lợi ích: Chỉ cần docker-compose up -d là toàn bộ hệ thống (Web + Node-RED + Tunnel) tự chạy,

3. Kiểm tra các container đang chạy trong docker, nếu có cái nào bị restart cần tìm lỗi rồi edit lại docker-compose.yml
4. Kiểm tra kiểm thử các service đang chạy độc lập thông qua ip và port của nó: ví dụ mở trình duyệt ip_ubuntu:1880 để check nodered đã chạy chưa
5. Sử dụng nodered: kéo nodered http_in , http_response, function : để tạo api get đơn giản (dùng cho /api proxy_pass của nginx)
6. Sửa file ./myweb/index.html : thêm code html+js để sử dụng được api đã khai báo proxy_pass (thực ra là sử dụng nodered http_in hoặc sử dụng service myapi)
## F. Gỡ lỗi:
1. nếu có lỗi xẩy ra trong quá trình triển khai docker compose up -d
- Kiểm tra nhanh: docker compose ps giúp biết container nào đang chạy xem log, ví dụ: docker logs mynginx docker logs myapi

2. Thêm healthcheck cho myapi trong file docker-compose.yml
healthcheck:
  test: ["CMD", "curl", "-f", "http://localhost:9630"]
3. giới hạn resource cho một service: (tránh việc 1 service chiếm quá nhiều ram)
deploy:
  resources:
    limits:
      memory: 512M
- sử dụng lệnh: docker compose stats để quan sát lượng ram sử dụng bởi mỗi service
G. Triển khai ứng dụng đến End-user
1. Trong Cloudflare: Tạo tunnel (đường hầm), chọn loại triển khai cho docker
2. Convert lệnh docker run ... sang dạng docker compose
3. Khai báo kết quả convert vào trong file docker-compose.yml
4. Chạy lại docker compose
5. Public ứng dụng bằng cách thêm 1 router trỏ tới container đang chạy trong docker, dữ liệu sẽ đi qua tunnel, url dạng sub-domain
6. Kiểm tra url sub-domain đã hoạt động public cho mọi end-user
- Cấu trúc thư mục:
myapp/
├── docker-compose.yml
├── nginx/
│   └── nginx.conf
├── myweb/
│   └── index.html
└── nodered/ (sẽ tự sinh dữ liệu)
│   └── (có nhiều file tự sinh)
│   └── settings.js (file này cần edit để bắt nodered login)
- Sơ đồ theo góc nhìn của dev:

- Sơ đồ theo góc nhìn ngược lại:

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
