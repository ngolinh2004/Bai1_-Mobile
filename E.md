## E. Triển khai (level test) ứng dụng
1. Chuyển vào trong thư mục ~/myapp

   <img width="418" height="18" alt="{918FF4F7-0851-4F2C-B908-50E9EF94F8BD}" src="https://github.com/user-attachments/assets/50b6aca5-1e49-48f8-bf5d-a9007f4733fb" />

2. Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
  - Lợi ích: Chỉ cần docker-compose up -d là toàn bộ hệ thống (Web + Node-RED + Tunnel) tự chạy,

    <img width="509" height="70" alt="{D13581C4-98A8-42CA-B9C1-373F0A3C5EB9}" src="https://github.com/user-attachments/assets/c7a2ce5f-e44d-4af7-8cf8-fab9c2b326d7" />

3. Kiểm tra các container đang chạy trong docker, nếu có cái nào bị restart cần tìm lỗi rồi edit lại docker-compose.yml

   <img width="675" height="96" alt="{58F3BB64-194C-4576-9C8C-E56BE7B802C8}" src="https://github.com/user-attachments/assets/cfadd6d1-9ae7-4d46-96b3-9e82c1fa9183" />

4. Kiểm tra kiểm thử các service đang chạy độc lập thông qua ip và port của nó: ví dụ mở trình duyệt ip_ubuntu:1880 để check nodered đã chạy chưa

  <img width="957" height="301" alt="{93D34E3F-1334-47A3-918D-BA4AB0347805}" src="https://github.com/user-attachments/assets/8ce7c939-fc79-4035-b001-a280ad7662ed" />

  

5. Sử dụng nodered: kéo nodered http_in , http_response, function : để tạo api get đơn giản (dùng cho /api proxy_pass của nginx)
   
6. Sửa file ./myweb/index.html : thêm code html+js để sử dụng được api đã khai báo proxy_pass (thực ra là sử dụng nodered http_in hoặc sử dụng service myapi)
