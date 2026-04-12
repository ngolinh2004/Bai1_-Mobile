## C. Cấu hình docker compose:
1. Tạo thư mục: ~/myapp
2. Chuyển vào trong thư mục ~/myapp
3. Tạo thư mục: ./myweb
   <img width="364" height="64" alt="{75BD6084-3417-4D2B-B97B-1F5B02050AF3}" src="https://github.com/user-attachments/assets/61181d39-6308-411c-91a6-f62b11cca6d9" />

4. Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)

   <img width="675" height="177" alt="{53E8733A-E224-490A-9AD8-373461E06ADC}" src="https://github.com/user-attachments/assets/b26249d1-3dde-4c99-bef2-a76c5dfdcc72" />

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
    
7. Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập Chạy docker-compose lần đầu để Node-RED tự sinh file cấu hình trong thư mục ./nodered, sau đó mới tiến hành sửa settings.js và restart lại container
