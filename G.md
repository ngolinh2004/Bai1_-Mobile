## G. Triển khai ứng dụng đến End-user
1. Trong Cloudflare: Tạo tunnel (đường hầm), chọn loại triển khai cho docker
2. Convert lệnh docker run ... sang dạng docker compose
3. Khai báo kết quả convert vào trong file docker-compose.yml
4. Chạy lại docker compose
5. Public ứng dụng bằng cách thêm 1 router trỏ tới container đang chạy trong docker, dữ liệu sẽ đi qua tunnel, url dạng sub-domain
6. Kiểm tra url sub-domain đã hoạt động public cho mọi end-user
  - Cấu trúc thư mục:

  - Sơ đồ theo góc nhìn của dev:

  - Sơ đồ theo góc nhìn ngược lại:

