## B. Cài đặt Ubuntu + Docker
1. Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
  - Sử dụng một trong các công cụ để giả lập: VM_Ware (bản quyền)
    <img width="960" height="482" alt="{C13C4A6D-29C1-43D0-B8A2-9013269C9514}" src="https://github.com/user-attachments/assets/13f9a4a8-d1c9-4c83-b397-669e1b648f4a" />

  - Download file iso để cài đặt.
    <img width="589" height="510" alt="{09A3B8F0-761D-4BA9-ABC7-61ECC6C2616F}" src="https://github.com/user-attachments/assets/d01f405d-da74-4dfe-b3b0-ab6938d6fac1" />

  - Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows

2. Tìm hiểu các lệnh cơ bản của ubuntu

  Các lệnh cần tìm hiểu:
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
