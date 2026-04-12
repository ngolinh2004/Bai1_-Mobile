## C. Cấu hình docker compose:
1. Tạo thư mục: ~/myapp
2. Chuyển vào trong thư mục ~/myapp
3. Tạo thư mục: ./myweb
   
   <img width="364" height="64" alt="{75BD6084-3417-4D2B-B97B-1F5B02050AF3}" src="https://github.com/user-attachments/assets/61181d39-6308-411c-91a6-f62b11cca6d9" />

4. Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)

   <img width="675" height="177" alt="{53E8733A-E224-490A-9AD8-373461E06ADC}" src="https://github.com/user-attachments/assets/b26249d1-3dde-4c99-bef2-a76c5dfdcc72" />

5. Tạo file docker-compose.yml để nó sẽ có các dịch vụ sau:

   <img width="385" height="22" alt="{0BE3FFFE-F6BB-4991-9C80-0EDED38D9BF5}" src="https://github.com/user-attachments/assets/ef2ad1f8-9a85-41cb-847a-c96c3d45d4e6" />

  - Khai báo sử dụng nodered/node-red, cổng 1880, dữ liệu nằm tại thư mục ./nodered
  - Khai báo sử dụng nginx, cổng 80, cấu hình trong file ./nginx/nginx.conf
  - Mount thư mục ./myweb thành thư mục /myweb trong nginx
  - Mount file ./nginx/nginx.conf vào file /etc/nginx/nginx.conf trong nginx

    <img width="658" height="349" alt="{67BC463E-FAFD-4FDA-80A4-28F4422584D3}" src="https://github.com/user-attachments/assets/3d4a461f-0316-4b10-b93d-63542524ee00" />

6. Edit file ./nginx/nginx.conf để:

   <img width="472" height="18" alt="{A33089B2-839F-402D-94F7-6A35EBD13E6B}" src="https://github.com/user-attachments/assets/0bfc7ad0-0873-43b1-ac73-5a2c2eaefd77" />

  - Cấu hình web server cổng 80
  - server_name là sub-domain (sub-domain tuỳ ý của em)
  - location / trỏ tới root là thư mục /myweb
  - location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered

    <img width="733" height="389" alt="{BB1A9BBD-9713-46A2-A956-42ED5E1CF60F}" src="https://github.com/user-attachments/assets/5509f90f-7634-4316-80ce-55c503927ebd" />

  - Ảnh kết quả :
    + Truy cập : http://192.168.136.128/
      
      <img width="952" height="341" alt="{FB611126-077F-466B-8AD8-5E68AF519088}" src="https://github.com/user-attachments/assets/3b22bcab-8d08-4075-ac99-bf9c876e8c89" />

    + http in (/hello) nối với function 1 nối với http response
        
      <img width="958" height="413" alt="{30907F26-DFA9-48B1-BE7F-7E07C1877D8D}" src="https://github.com/user-attachments/assets/92fbc2bd-f111-460e-bbc3-6b486f27de74" />

   + Truy cập: http://192.168.136.128:1880/hello

     <img width="793" height="311" alt="{F81CBF63-9731-422D-97A7-15234A28692A}" src="https://github.com/user-attachments/assets/970aea8d-f37a-4a7b-938c-33efa32a5da6" />



7. Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập Chạy docker-compose lần đầu để Node-RED tự sinh file cấu hình trong thư mục ./nodered, sau đó mới tiến hành sửa settings.js và restart lại container

 

