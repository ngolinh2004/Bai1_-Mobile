## B. Cài đặt Ubuntu + Docker
1. Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
  - Sử dụng một trong các công cụ để giả lập: VM_Ware (bản quyền)
    <img width="960" height="482" alt="{C13C4A6D-29C1-43D0-B8A2-9013269C9514}" src="https://github.com/user-attachments/assets/13f9a4a8-d1c9-4c83-b397-669e1b648f4a" />

  - Download file iso để cài đặt.
    
    <img width="589" height="510" alt="{09A3B8F0-761D-4BA9-ABC7-61ECC6C2616F}" src="https://github.com/user-attachments/assets/d01f405d-da74-4dfe-b3b0-ab6938d6fac1" />

  - Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows

<img width="596" height="314" alt="{748505CB-9F0F-4AE9-BAF1-014BB48AAD93}" src="https://github.com/user-attachments/assets/f282e474-af75-4c84-a436-edf8fb5282ce" />

2. Tìm hiểu các lệnh cơ bản của ubuntu

  Các lệnh cần tìm hiểu:
  - Liệt kê các file trong thư mục: ls

    <img width="503" height="69" alt="{ED374048-2D64-4369-8FA6-7F7116012AAA}" src="https://github.com/user-attachments/assets/4eba830b-b856-46de-b218-b794f152a0e1" />

  - Tạo thư mục: mkdir nameFolder

    <img width="360" height="20" alt="{97361E2A-F163-42E0-BC6D-575DB9A97082}" src="https://github.com/user-attachments/assets/87aca8b0-5e0c-4739-b5b6-b11b9f7159f4" />

  - Chuyển thư mục làm việc: cd path

    <img width="332" height="21" alt="{7CC6EC08-3D96-4F37-8954-511D5CD1CF5E}" src="https://github.com/user-attachments/assets/483c8404-677a-43f3-880f-0d873511d17a" />

  - Copy file: cp file_nguồn path/file_đích

    <img width="416" height="30" alt="{2B186E89-0387-4FC8-8A78-934918553F72}" src="https://github.com/user-attachments/assets/c7d3f1a6-eb9f-4329-9791-869ab496e35d" />

  - Thay đổi quyền thao tác file: sudo chmod xxx filename

    <img width="444" height="25" alt="{ECB3F082-E778-44C7-8F89-57F93ED9D49B}" src="https://github.com/user-attachments/assets/8e762679-022b-4382-9833-1d0d37902910" />

  - Edit file: sudo nano tenfile
    + CTRL+o : lưu nội dung sau khi edit
    + CTRL+x : thoát edit file
      
      <img width="677" height="318" alt="{57F1A70B-A220-445D-9EA7-41B4213FFC30}" src="https://github.com/user-attachments/assets/729430dd-e11d-44cd-830d-407e565b027c" />

  - Xem ip của máy ubuntu: ip -4 addr

    <img width="602" height="117" alt="{437C2ECC-CD69-4A8F-8137-83CD1BF56E8B}" src="https://github.com/user-attachments/assets/eac2d730-4449-49e8-a257-63befe701b39" />

3. Cài đặt docker cho Ubuntu
   <img width="661" height="350" alt="{22BDA08F-7565-421E-9408-52ED47647243}" src="https://github.com/user-attachments/assets/22cdb423-4792-48ef-8b59-b9038d0f9a23" />

4. Kiểm tra phiên bản docker vừa cài đặt, kiểm tra phiên bản của docker compose

   <img width="537" height="74" alt="{FF37BFEA-613B-4084-A653-BEE2A57E6659}" src="https://github.com/user-attachments/assets/23fba895-b454-49a6-b8be-e06c0ea65e51" />

5. Cấu hình để docker chạy mà không cần tiền tố sudo

   <img width="609" height="337" alt="{11858C75-1100-4A15-BC9C-DB20EAE6366B}" src="https://github.com/user-attachments/assets/33543f49-e9a0-4892-9e51-0c328d17e391" />

6. Tìm hiểu tập lệnh của docker và docker compose
  - Lệnh Docker
    + docker --version: Kiểm tra phiên bản Docker
    + docker run hello-world: Chạy container để kiểm tra Docker hoạt động
    + docker ps: Xem các container đang chạy
    + docker ps -a: Xem tất cả container (kể cả đã dừng)
    + docker images: Xem danh sách các image
    + docker pull nginx: Tải image từ Docker Hub
    + docker logs <container_name>: Xem log của container
    + docker stop <container_name>: Dừng container
    + docker rm <container_name>: Xóa container
  - Lệnh Docker Compose
    + docker compose up -d: Chạy toàn bộ service trong file docker-compose.yml (chạy nền)
    + docker compose down: Dừng và xóa toàn bộ dịch vụ
    + docker compose ps: Xem trạng thái các container
    + docker compose logs: Xem log các dịch vụ
    + docker compose restart: Khởi động lại dịch vụ
    + docker compose up -d --build: Build lại image và chạy lại container
      
7. Đảm bảo tường lửa trên Ubuntu đã cho phép các cổng 80, 1880, 9630 (Lệnh: sudo ufw allow ...)

<img width="564" height="314" alt="{3D633261-5828-488E-A7DA-65449009B890}" src="https://github.com/user-attachments/assets/a21f3b33-2927-4500-b87d-30b15e4d8c1f" />
