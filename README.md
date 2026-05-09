Môn: Phát triển ứng dụng với mã nguồn mở-TEE0421

MSSV: K225480106085	

Lớp: 58KTPM

Bài tập 02:

SỬ DỤNG DJANGO ĐỂ TẠO WEB QUẢN LÝ TIỆM CẦM ĐỒ

deadline : 23h59 ngày 09 tháng 5 năm 2026.

Link gửi bài: Tại đây

1.TỔ CHỨC CSDL CHO HỆ THỐNG QUẢN LÝ TIỆM CẦM ĐỒ: viết tay ra giấy, lấy điện thoại chụp lại, upload ảnh lên github (đã nói về các nghiệp 
vụ trên lớp, ghi bảng)

2.SỬ DỤNG DOCKER TRÊN UBUNTU ĐỂ:

Mariadb : chứa csdl của hệ thống này

Phpmyadmin: để soi được csdl (chỉ để xem, ko cần tạo bảng từ đây, django sẽ làm hết)

Django: build 1 docker container (dùng Dockerfile): trên nền python, sử dụng django, nhớ mount thư mục để dễ edit, edit dùng: sudo nano
ten_file

sau khi có 3 service này trong file docker-compose.yml :

run nó, cấu hình để Django nhận csdl mariadb (sửa file settings.py), cấu hình user login ban đầu, mô tả các bảng trong models.py, ....

(đc phép sử dụng AI để làm) => KQ được trang admin, y/c đăng nhập, vào trang admin: cho phép thêm sửa xoá dữ liệu các bảng. các trường

là khoá ngoại chỉ việc chọn text (mặc dù là csdl tại trường FK đó lưu ID của PK mà nó tham chiếu : sử dụng phpmyadmin để kiểm chứng)

chú ý kết hợp ssh để chạy lệnh tác động vào django và sudo nano để edit file.

sử dụng template (file html, sử dụng cú pháp jinja2), lấy context từ 1 view home_page, để tạo trang liệt kê các con nợ đến hạn mà chưa

trả tiền!

sử dụng cloudflare tunnel để public kết quả lên 1 sub-domain => chụp kết quả

Hướng dẫn:

Tạo thư mục để chứa image tự buid cho django

Vào thư mục đó tạo file tên: Dockerfile (nội dung hỏi AI xem file này cần có nội dung gì, full comment cho từng dòng lệnh trong file

này => mục tiêu kép: để hiểu và để hệ thống chạy được)

AI sẽ nói cần thêm file requirements.txt để cài các thư viện cho python (cài qua lệnh pip) => tạo file requirements.txt với nội dung

tưng ứng, trong file này cũng comment được => comment xem thư viện nào dùng để làm gì

Sau mỗi lần sửa đỏi có thể phải chạy lệnh dạng : docker compose exec TÊN_SERVICE_DJANGO_CỦA_BẠN python manage.py migrate để tác động

vào django (còn nhiều lệnh khác chứ ko luôn như này), để django thay đổi csdl hoặc thay đổi cấu hình.

BÀI LÀM
1: CHUẨN BỊ UBUNTU
Kiểm tra phiên bản Docker docker --version

Kiểm tra phiên bản Docker Compose docker compose version

<img width="1077" height="635" alt="Screenshot 2026-05-08 213842" src="https://github.com/user-attachments/assets/e0c2efbf-e731-4511-8fb1-4b2282147df2" />


2: TẠO PROJECT

Bước 1: Tạo thư mục mkdir camdo_project


Bước 2: Vào thư mục cd camdo_project

<img width="1077" height="635" alt="Screenshot 2026-05-08 213842" src="https://github.com/user-attachments/assets/f441f09b-2ff2-4be2-ba31-db4b62b00cc2" />


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

👉 Kết quả phải thấy


manage.py


pawnshop


Dockerfile


requirements.txt


9: CẤU HÌNH DATABASE

Bước 1: Mở settings.py nano django_app/core/settings.py

Bước 2: Tìm DATABASES -> Trong nano bấm Ctrl + M -> Gõ DATABASES

Bước 3: Tìm đến và sửa thành như sau

<img width="594" height="378" alt="Screenshot 2026-05-09 215839" src="https://github.com/user-attachments/assets/12d7eca6-1b93-4bdb-a450-fe0472351fbd" />


Bước 4: Thêm app -> tìm INSTALLED_APPS -> Thêm '',

<img width="493" height="202" alt="Screenshot 2026-05-09 230358" src="https://github.com/user-attachments/assets/806f6804-912b-4150-ab5b-2a77964d0b67" />


10: TẠO DATABASE MODEl

Bước 1: Mở model.py bằng lệnh nano django/management/models.py

Bước 2: Thêm nội dung

<img width="978" height="386" alt="Screenshot 2026-05-09 230523" src="https://github.com/user-attachments/assets/1905d25e-5ccb-4ea3-afae-1fab03a31bef" />


Bước 3: Đăng ký model vào admin bằng lệnh nano django/management/admin.py

<img width="721" height="215" alt="Screenshot 2026-05-09 230627" src="https://github.com/user-attachments/assets/d86971ae-e0a7-4793-b2ab-dc828499f17d" />


11: TẠO MIGRATION

Chạy lệnh: docker compose exec django python manage.py makemigrations

<img width="1920" height="1080" alt="Screenshot 2026-05-08 233747" src="https://github.com/user-attachments/assets/aad31f2d-94ea-41ae-9257-065e55f57693" />



APPLY DATABASE bằng lệnh docker compose exec django python manage.py migrate

<img width="890" height="612" alt="Screenshot 2026-05-08 231100" src="https://github.com/user-attachments/assets/5ce92d64-8d98-4184-b78f-7700fab99bcb" />


12: TẠO SUPERUSER

Chạy lệnh docker compose exec django python manage.py createsuperuser

<img width="1920" height="1080" alt="Screenshot 2026-05-08 231243" src="https://github.com/user-attachments/assets/662004e6-24fc-40be-b514-4a51dc7a2c41" />


👉 Thực hiện điền các thông tin username & password

13: CHẠY WEB

Truy cập django admin bằng địa chỉ: http://IP_UBUNTU:8000/admin

<img width="1920" height="1080" alt="Screenshot 2026-05-08 233833" src="https://github.com/user-attachments/assets/5b4aa30c-adad-436c-a418-71de8f456a75" />


👉 Lưu ý: Nếu không truy cập được có thể là do cơ chế bảo mật của django, ip sử dụng chưa được khai báo trong danh sách người quen (allowed Hosts). Để khắc phục tình trạng này cần phải khai báo ip trong file settings.py hoặc để dễ dàng cho việc học tập có thể cho phép tất cả.

<img width="602" height="116" alt="image" src="https://github.com/user-attachments/assets/93f528c6-9101-4b1f-93d0-96fe18d40810" />


14: TEST CRUD

Bước 1: Thêm dữ liệu

Thêm khách hàng

<img width="1188" height="996" alt="Screenshot 2026-05-09 221118" src="https://github.com/user-attachments/assets/04df79f8-afd2-4580-b465-90fce0386f2c" />

Thêm Giao dịch

<img width="1920" height="1080" alt="Screenshot 2026-05-09 220951" src="https://github.com/user-attachments/assets/7766b37d-250a-4206-88ac-d8917962d409" />

15: TEST PHPMYADMIN

Truy cập địa chỉ http://IP_UBUNTU:8888



Kiểm tra các bảng

a) Bảng khách hàng


Bảng management_khachhang dùng để lưu thông tin khách hàng:

Tên khách hàng

CCCD

Địa chỉ

Số điện thoại

Khóa chính (Primary Key):

id

{A88A45EB-F1ED-4B42-BFEA-FDA83C88C432}

b) Bảng giao dịch

{F57847B3-F13B-4651-B077-E455C71635BC}

Bảng management_giaodich dùng để quản lý:

Khách hàng cầm đồ

Tài sản thế chấp

Số tiền vay

Deadline trả nợ

Lãi suất

Trạng thái đã trả/chưa trả

Foreign Key:

khach_hang_id

chi_tiet_tai_san_id

Database thực tế lưu ID khóa ngoại thay vì text.

{7A7C3940-E3EC-4557-BD5A-85D5E675A78C}

c) Bảng Mô tả tài sản

{A18F0037-4DA6-4C50-BFC3-7C384E6DB141}

Bảng management_motataisan dùng để lưu mô tả chi tiết tài sản thế chấp.

Khóa chính:

id
{277F16E4-F2E9-46F9-B512-93E8EADE933E}

d) Kiểm chứng Foreign Key

Trong Django Admin người dùng chọn bằng tên,

nhưng trong MariaDB hệ thống lưu bằng ID khóa ngoại.

Ví dụ:

khach_hang_id = 1
chi_tiet_tai_san_id = 1
{2CEB0188-AB8E-4850-A628-A0171B425662}

16: TẠO TEMPLATE HTML
Bước 1: Tạo thư mục template mkdir -p django/management/templates

Bước 2: Tạo file home.html nano django/management/templates/home.html

Bước 3: Thêm nội dung

{5976C949-B8AA-4640-BEBA-DAFB1E7E6559}

Bước 4: Tạo file views.py nano django/management/views.py
{73596296-700A-4F23-B51F-232CE9D428F7}

Bước 5: Tạo file urls.py nano django/pawnshop/urls.py
{842DF8CC-CC9D-4896-9D3C-3AB791B4BF53}

17: TEST WEB
Truy cập địa chỉ 'http://<ip_ubuntu>:8000/`
{50C5AA8C-E753-4E64-A331-C358D3D4D7E3}

18: PUBLIC DJANGO LÊN SUBDOMAIN BẰNG CLOUDFLARE TUNNEL
Bước 1: Dowload claudfare tunnel bằng lệnh wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
image

Bước 2: Cài đặt sudo dpkg -i cloudflared-linux-amd64.deb

Bước 3: Kiểm tra cloudflared --version

{810FF189-36A5-4CC8-8F51-A17ABC56EBE5}

19: LOGIN CLOUDFLARE
Chạy lệnh 'cloudflared tunnel login` sẽ sinh ra 1 địa chỉ để login vào claudfare tunnel

Truy cập địa chỉ đó trên trình duyệt

{CA1C8789-0390-475A-A8D8-DBF4E66E441D}

Chọn đúng domain -> Chọn Authorize
{4A182B01-1A62-4CB8-BEFD-27E95C016FF4}

👉 Sau khi click sẽ hiện thông báo đồng thời trên ubuntu cũng thông báo You have successfully logged in và sinh ra file .pem

image

{581C8B6F-168F-43BA-B53E-A033F9BB80EE}

20: TẠO TUNNEL
Chạy lệnh: cloudflared tunnel create camdo-tunnel sẽ ra 1 dãy id
{C8CE2927-5BEA-4EB0-A962-4894914EA46A}

Tạo file config.yml bằng lệnh nano ~/.cloudflared/config.yml
{366841DA-4FB7-4FFB-AFF4-EAA9EF845C75}

Thêm nội dung sau ( Vì dùng chung đường hầm với web cũ nên không cần thêm id, có thể dùng chung ip với web cũ)
{C3765F71-80C9-41AE-9A3B-260C458973CB}

21: CHẠY TUNNEL
Chạy lệnh cloudflared tunnel run camdo-tunnel
{78CE7D21-BF3A-4AE4-B399-CFFC0FCC4E9A}

Truy cập http://camdo.ducduong.id.vn
{B978C107-B9F9-4303-8BAF-955C9C19EA54}

👉 Sau khi truy cập domain -> login bằng tài khoản admin -> có thể tiến hành ( thêm + sửa + xoá ) -> có thể quản lý bằng cách "xem danh sách con nợ"







