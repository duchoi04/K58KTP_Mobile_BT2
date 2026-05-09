MÔN: PHÁT TRIỂN ỨNG DỤNG VỚI MÃ NGUỒN MỞ - TEE0421

Họ và tên: HOÀNG ĐỨC HỘI

MSSV: K225480106085	

Lớp: 58KTPM

Bài tập 02:

SỬ DỤNG DJANGO ĐỂ TẠO WEB QUẢN LÝ TIỆM CẦM ĐỒ

deadline : 23h59 ngày 09 tháng 5 năm 2026.

Link gửi bài: Tại đây

1.TỔ CHỨC CSDL CHO HỆ THỐNG QUẢN LÝ TIỆM CẦM ĐỒ: viết tay ra giấy, lấy điện thoại chụp lại, upload ảnh lên github (đã nói về các nghiệp vụ trên lớp, ghi bảng)

2.SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ:

Mariadb : chứa csdl của hệ thống này

Phpmyadmin: để soi được csdl (chỉ để xem, ko cần tạo bảng từ đây, django sẽ làm hết)

Django: build 1 docker container (dùng Dockerfile): trên nền python, sử dụng django, nhớ mount thư mục để dễ edit, edit dùng: sudo nano ten_file

sau khi có 3 service này trong file docker-compose.yml :

- run nó, cấu hình để Django nhận csdl mariadb (sửa file settings.py), cấu hình user login ban đầu, mô tả các bảng trong models.py, ....(đc phép sử dụng AI để làm) => KQ được trang admin, y/c đăng nhập, vào trang admin: cho phép thêm sửa xoá dữ liệu các bảng. các trường là khoá ngoại chỉ việc chọn text (mặc dù là csdl tại trường FK đó lưu ID của PK mà nó tham chiếu : sử dụng phpmyadmin để kiểm chứng)

- chú ý kết hợp ssh để chạy lệnh tác động vào django và sudo nano để edit file.

- sử dụng template (file html, sử dụng cú pháp jinja2), lấy context từ 1 view home_page, để tạo trang liệt kê các con nợ đến hạn mà chưa trả tiền!

- sử dụng cloudflare tunnel để public kết quả lên 1 sub-domain => chụp kết quả

Hướng dẫn:

- Tạo thư mục để chứa image tự buid cho django

- Vào thư mục đó tạo file tên: Dockerfile (nội dung hỏi AI xem file này cần có nội dung gì, full comment cho từng dòng lệnh trong file này => mục tiêu kép: để hiểu và để hệ thống chạy được)

- AI sẽ nói cần thêm file requirements.txt để cài các thư viện cho python (cài qua lệnh pip)
=> tạo file requirements.txt với nội dung tưng ứng, trong file này cũng comment được
=> comment xem thư viện nào dùng để làm gì
- Sau mỗi lần sửa đỏi có thể phải chạy lệnh dạng : docker compose exec TÊN_SERVICE_DJANGO_CỦA_BẠN python manage.py migrate để tác động vào django (còn nhiều lệnh khác chứ ko luôn như này), để django thay đổi csdl hoặc thay đổi cấu hình.

                                                     BÀI LÀM
TỔ CHỨC CSDL CHO HỆ THỐNG QUẢN LÝ TIỆM CẦM ĐỒ

<img width="1920" height="2560" alt="image" src="https://github.com/user-attachments/assets/0b308709-af06-41c9-8ec8-c3e6902d8105" />


1: CHUẨN BỊ UBUNTU

Kiểm tra phiên bản Docker docker --version

Kiểm tra phiên bản Docker Compose docker compose version

<img width="1077" height="635" alt="Screenshot 2026-05-08 213842" src="https://github.com/user-attachments/assets/e0c2efbf-e731-4511-8fb1-4b2282147df2" />


2: TẠO PROJECT

Bước 1: Tạo thư mục mkdir camdo_project

Bước 2: Vào thư mục cd camdo_project

<img width="668" height="152" alt="Screenshot 2026-05-08 225042" src="https://github.com/user-attachments/assets/fa275020-e592-45ab-b7b0-375966c0540f" />

Bước 3: Tạo thư mục django trong camdo_project

<img width="668" height="152" alt="Screenshot 2026-05-08 225042" src="https://github.com/user-attachments/assets/fa275020-e592-45ab-b7b0-375966c0540f" />

3: TẠO DOCKERFILE

Bước 1: Vào thư mục Django: cd django

Bước 2: Tạo file DockerFile nano Dockerfile

Bước 3: Thêm nội dung cho File dockerfile

<img width="1920" height="1080" alt="Screenshot 2026-05-08 214353" src="https://github.com/user-attachments/assets/37820763-75f7-4ea2-8886-25a6dccb91ed" />


4: TẠO FILE requirements.txt

Bước 1: Tạo file requirements.txt nano requirements.txt

Bước 2: Dán nội dung sau

<img width="1920" height="1080" alt="Screenshot 2026-05-08 214337" src="https://github.com/user-attachments/assets/f84a7a17-222c-4aeb-9cb0-6d4a27a65c0d" />

5: TẠO FILE DOCKER - COMPOSE.YML

Bước 1: Quay lại thư mục gốc cd ..

Bước 2: Tạo file docker - compose.yml nano docker-compose.yml

Bước 3: Dán nội dung sau


<img width="1920" height="1080" alt="Screenshot 2026-05-08 214404" src="https://github.com/user-attachments/assets/dce54d7a-d458-4da4-8354-36c6b1d885e7" />


6: TIẾN HÀNH BUILD CONTAINER

Bước 1: Build bằng lệnh docker compose up -d --build

Bước 2: Kiểm tra container bằng lệnh docker ps

<img width="1920" height="1080" alt="Screenshot 2026-05-08 222615" src="https://github.com/user-attachments/assets/e3ecb245-d987-4d9e-afc0-5b1726fd913e" />

👉 Kết quả phải thấy 3 service: mariadb + phpmyadmin + django_app

7: TẠO DJANGO PROJECT

Bước1: chạy lệnh docker compose exec web python manage.py startapp management .

<img width="1920" height="1080" alt="Screenshot 2026-05-08 230138" src="https://github.com/user-attachments/assets/92fb5250-3921-4166-96fd-15705c06eed0" />


Bước 2: Kiểm tra file ls django

<img width="1920" height="1080" alt="Screenshot 2026-05-08 230138" src="https://github.com/user-attachments/assets/95487d02-0fa0-48ef-9a77-c60e72967f8d" />

👉 Kết quả phải thấy:

manage.py

core

Dockerfile

requirements.txt

9: CẤU HÌNH DATABASE

Bước 1: Mở settings.py nano django_app/core/settings.py

Bước 2: Tìm DATABASES -> Trong nano bấm Ctrl + M -> Gõ DATABASES

Bước 3: Tìm đến và sửa thành như sau

<img width="594" height="378" alt="Screenshot 2026-05-09 215839" src="https://github.com/user-attachments/assets/12d7eca6-1b93-4bdb-a450-fe0472351fbd" />


Bước 4: Thêm app -> tìm INSTALLED_APPS -> Thêm 'app_quanly',

<img width="493" height="202" alt="Screenshot 2026-05-09 230358" src="https://github.com/user-attachments/assets/806f6804-912b-4150-ab5b-2a77964d0b67" />


10: TẠO DATABASE MODEl

Bước 1: Mở model.py bằng lệnh nano django_app/app_quanly/models.py

Bước 2: Thêm nội dung

<img width="978" height="386" alt="Screenshot 2026-05-09 230523" src="https://github.com/user-attachments/assets/1905d25e-5ccb-4ea3-afae-1fab03a31bef" />


Bước 3: Đăng ký model vào admin bằng lệnh nano django_app/app_quanly/admin.py

<img width="721" height="215" alt="Screenshot 2026-05-09 230627" src="https://github.com/user-attachments/assets/d86971ae-e0a7-4793-b2ab-dc828499f17d" />


11: TẠO MIGRATION

Chạy lệnh: docker compose exec web python manage.py makemigrations

<img width="1920" height="1080" alt="Screenshot 2026-05-08 233747" src="https://github.com/user-attachments/assets/aad31f2d-94ea-41ae-9257-065e55f57693" />


APPLY DATABASE bằng lệnh docker compose exec web python manage.py migrate

<img width="890" height="612" alt="Screenshot 2026-05-08 231100" src="https://github.com/user-attachments/assets/5ce92d64-8d98-4184-b78f-7700fab99bcb" />


12: TẠO SUPERUSER

Chạy lệnh docker compose exec web python manage.py createsuperuser

<img width="1920" height="1080" alt="Screenshot 2026-05-08 231243" src="https://github.com/user-attachments/assets/662004e6-24fc-40be-b514-4a51dc7a2c41" />

👉 Thực hiện điền các thông tin username & password

13: CHẠY WEB

Truy cập django admin bằng địa chỉ: http://192.168.1.136:8000/admin

<img width="1920" height="1080" alt="Screenshot 2026-05-08 233833" src="https://github.com/user-attachments/assets/5b4aa30c-adad-436c-a418-71de8f456a75" />


👉 Lưu ý: Nếu không truy cập được có thể là do cơ chế bảo mật của django, ip sử dụng chưa được khai báo trong danh sách người quen (allowed Hosts). Để khắc phục tình trạng này cần phải khai báo ip trong file settings.py hoặc để dễ dàng cho việc học tập có thể cho phép tất cả.

<img width="602" height="116" alt="image" src="https://github.com/user-attachments/assets/93f528c6-9101-4b1f-93d0-96fe18d40810" />


14: TEST CRUD

Bước 1: Thêm dữ liệu

Thêm khách hàng

<img width="1188" height="996" alt="Screenshot 2026-05-09 221118" src="https://github.com/user-attachments/assets/04df79f8-afd2-4580-b465-90fce0386f2c" />

Thêm hợp đồng

<img width="1920" height="1080" alt="Screenshot 2026-05-09 220951" src="https://github.com/user-attachments/assets/7766b37d-250a-4206-88ac-d8917962d409" />

15: TEST PHPMYADMIN

Truy cập địa chỉ http://192.168.1.136:8081

Kiểm tra các bảng

a) Bảng khách hàng

<img width="1920" height="1080" alt="Screenshot 2026-05-09 001253" src="https://github.com/user-attachments/assets/2e6d0252-503a-46d1-8376-1cc047671172" />

Bảng app_quanly_khachhang dùng để lưu thông tin khách hàng:

Tên khách hàng

Số điện thoại

b) Bảng hợp đồng

<img width="1920" height="1080" alt="Screenshot 2026-05-09 001248" src="https://github.com/user-attachments/assets/6cd1ada1-5be1-46e6-8a38-d4b349d78049" />

Bảng app_quanly_hopdong dùng để quản lý:

Khách hàng cầm đồ

Tài sản thế chấp

Số tiền vay

Deadline trả nợ

Trạng thái đã trả/chưa trả

16: TẠO TEMPLATE HTML

Bước 1: Tạo thư mục template mkdir -p django_app/app_quanly/templates

Bước 2: Tạo file home.html nano django_app/app_quanly/templates/home.html

Bước 3: Thêm nội dung

<img width="1581" height="929" alt="Screenshot 2026-05-09 221958" src="https://github.com/user-attachments/assets/8a8cbb82-daea-479c-ba4d-286e30b359e4" />


Bước 4: Tạo file views.py nano django_app/app_quanly/views.py

<img width="675" height="231" alt="Screenshot 2026-05-09 222129" src="https://github.com/user-attachments/assets/cfaf6623-356a-4de8-90f4-7e7e978aeb72" />


Bước 5: Tạo file urls.py nano django_app/app_quanly/urls.py

<img width="693" height="192" alt="Screenshot 2026-05-09 222206" src="https://github.com/user-attachments/assets/03bef6fa-459d-468e-b121-b667d9ca4ae9" />


17: TEST WEB

Truy cập địa chỉ 'http://192.168.1.136:8000/`

<img width="1920" height="1080" alt="Screenshot 2026-05-09 004535" src="https://github.com/user-attachments/assets/e8757dad-1a61-4a5c-8149-264c10b93d0b" />


18: PUBLIC DJANGO LÊN SUBDOMAIN BẰNG CLOUDFLARE TUNNEL

Bước 1: Dowload claudfare tunnel bằng lệnh wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb

<img width="1920" height="1080" alt="Screenshot 2026-05-08 235932" src="https://github.com/user-attachments/assets/de1da6c3-5905-4abe-a71b-116a73e4286d" />

Bước 2: Cài đặt sudo dpkg -i cloudflared-linux-amd64.deb

Bước 3: Kiểm tra cloudflared --version

<img width="1920" height="1080" alt="Screenshot 2026-05-09 000013" src="https://github.com/user-attachments/assets/f4de2bf0-58a9-42bd-af09-a73da0e0c1ab" />

19: LOGIN CLOUDFLARE

Chạy lệnh 'cloudflared tunnel login` sẽ sinh ra 1 địa chỉ để login vào claudfare tunnel

Truy cập địa chỉ đó trên trình duyệt

<img width="1829" height="170" alt="Screenshot 2026-05-09 002659" src="https://github.com/user-attachments/assets/549147cb-4ff5-4ff5-a575-07fb6f9e903c" />

Chọn đúng domain -> Chọn Authorize

👉 Sau khi click sẽ hiện thông báo đồng thời trên ubuntu cũng thông báo You have successfully logged in và sinh ra file .pem

<img width="1920" height="1080" alt="Screenshot 2026-05-09 002735" src="https://github.com/user-attachments/assets/a4db50a6-d08c-4299-a6ba-1c99712b9df5" />

<img width="1318" height="177" alt="Screenshot 2026-05-09 002807" src="https://github.com/user-attachments/assets/04c7eb08-687f-4c95-b78f-59530dd0db7b" />


20: TẠO TUNNEL

Chạy lệnh: cloudflared tunnel create camdo-tunnel sẽ ra 1 dãy id

<img width="1734" height="153" alt="Screenshot 2026-05-09 002848" src="https://github.com/user-attachments/assets/9b39cf9d-c76c-4630-8d86-9d209e21742a" />


Tạo file config.yml bằng lệnh nano ~/.cloudflared/config.yml

Thêm nội dung sau ( Vì dùng chung đường hầm với web cũ nên không cần thêm id, có thể dùng chung ip với web cũ)

<img width="1920" height="1080" alt="Screenshot 2026-05-09 003749" src="https://github.com/user-attachments/assets/e91e27a3-473b-4ae8-a436-eabc86742872" />

21: CHẠY TUNNEL

Chạy lệnh cloudflared tunnel run camdo-tunnel

<img width="1920" height="1080" alt="Screenshot 2026-05-09 003729" src="https://github.com/user-attachments/assets/b060192d-a01b-4704-8bcc-6c2674e9cf13" />


Truy cập http://camdo.duchoi.io.vn

<img width="1920" height="1080" alt="Screenshot 2026-05-09 223656" src="https://github.com/user-attachments/assets/2d869afc-0b01-4232-9b6a-798300b9a029" />

<img width="1920" height="1080" alt="Screenshot 2026-05-09 004544" src="https://github.com/user-attachments/assets/86fcca0e-7372-49e1-8e7b-5369f00e168a" />

TEST TRÊN THIẾT BỊ KHÁC KHÔNG SỬ DỤNG WIFI

<img width="1179" height="2556" alt="image" src="https://github.com/user-attachments/assets/38ae0f61-8e72-405a-adcf-cd1a7c78dec4" />

<img width="1179" height="2556" alt="image" src="https://github.com/user-attachments/assets/11213119-d985-4d90-8c7e-6dbb346e5668" />






