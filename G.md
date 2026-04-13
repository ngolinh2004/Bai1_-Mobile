## G. Triển khai ứng dụng đến End-user
1. Trong Cloudflare: Tạo tunnel (đường hầm), chọn loại triển khai cho docker
   
  <img width="958" height="366" alt="{C3830236-60E0-41AD-A46C-C031ABEAE18B}" src="https://github.com/user-attachments/assets/7cdf1f7e-24b2-4b46-b8e0-4425d17324ad" />

2. Convert lệnh docker run ... sang dạng docker compose

   <img width="498" height="334" alt="{36D27167-DC5C-4073-B617-C8D841CCFCDF}" src="https://github.com/user-attachments/assets/5a8b2530-fac8-497e-bc2f-7d80deb097c9" />

3. Khai báo kết quả convert vào trong file docker-compose.yml
   
4. Chạy lại docker compose
   
5. Public ứng dụng bằng cách thêm 1 router trỏ tới container đang chạy trong docker, dữ liệu sẽ đi qua tunnel, url dạng sub-domain
   
   <img width="948" height="386" alt="{4CCB6EAF-8C3F-4301-88DC-58AF814E583A}" src="https://github.com/user-attachments/assets/3e62d83f-ef19-4a0f-8f7c-49bba61af99c" />

   <img width="954" height="391" alt="{7D30ED4D-09E3-45AF-8346-550DD2101AD8}" src="https://github.com/user-attachments/assets/630e4be9-de71-4533-8f9a-5eca9d7b9bce" />

6. Kiểm tra url sub-domain đã hoạt động public cho mọi end-user

   <img width="862" height="460" alt="{FA485A46-74F3-49B8-BB79-F67A5945AD9B}" src="https://github.com/user-attachments/assets/1d4d0cb6-3ebf-41be-99ca-fdbfc36517fc" />

   <img width="720" height="1600" alt="image" src="https://github.com/user-attachments/assets/b6f34c56-f747-42ed-91fc-aea2dc92f43e" />

  
