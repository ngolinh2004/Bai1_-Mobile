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
   
   <img width="799" height="426" alt="{2F202381-6E75-404D-B7AC-06D522B71B61}" src="https://github.com/user-attachments/assets/99df0fc2-2db7-4ce2-ae29-9a1f746ab5a7" />

   <img width="1585" height="622" alt="image" src="https://github.com/user-attachments/assets/39d0bcca-df54-4a09-afc2-29a0b8b8f383" />

   <img width="1585" height="622" alt="image" src="https://github.com/user-attachments/assets/624240e1-e8a2-4253-ba07-c1e2c09a2aaa" />

   <img width="811" height="209" alt="{6950C75B-F80A-4506-B41B-D3A75B7AB31E}" src="https://github.com/user-attachments/assets/d7eb814a-9489-479b-9670-756b4d89dd3e" />

7. Sửa file ./myweb/index.html : thêm code html+js để sử dụng được api đã khai báo proxy_pass (thực ra là sử dụng nodered http_in hoặc sử dụng service myapi)

   <img width="768" height="536" alt="{294E5AA2-4AD0-4B50-A715-04E8FC539B9F}" src="https://github.com/user-attachments/assets/3c7fbcca-ebdf-41d1-ac0d-4d180e3958ee" />

   <img width="662" height="387" alt="{89885917-CDFD-4325-9A00-68F1C72586D1}" src="https://github.com/user-attachments/assets/bb9ccf09-8f23-4cf5-b7f9-b834acdc0ba4" />

   <img width="960" height="442" alt="{7818BADF-CEB2-4155-8188-B2507D158AAA}" src="https://github.com/user-attachments/assets/dfb14e12-438d-45dd-85c9-d1c91953a857" />


