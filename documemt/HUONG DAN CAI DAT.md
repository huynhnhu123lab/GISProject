# HƯỚNG DẪN CÀI ĐẶT VÀ VẬN HÀNH DỰ ÁN WEB GIS BÁNH KẸO

Tài liệu này hướng dẫn chi tiết các bước để thiết lập môi trường và chạy dự án Website Quản lý hệ thống cửa hàng Bánh kẹo tích hợp bản đồ GIS.

---

## 1. YÊU CẦU MÔI TRƯỜNG
Để dự án chạy ổn định, máy tính cần cài đặt sẵn các thành phần sau:
* **Python:** Phiên bản 3.10 trở lên.
* **PostgreSQL:** Phiên bản 18 (hoặc các bản mới nhất).
* **PostGIS:** Extension hỗ trợ dữ liệu không gian (Cài đặt cùng PostgreSQL).
* **Thư viện hình ảnh:** Pillow (Sẽ được cài đặt qua file requirements).

---

## 2. THIẾT LẬP CƠ SỞ DỮ LIỆU (PGADMIN 4)

1. **Tạo Database:**
   - Mở pgAdmin 4.
   - Chuột phải vào **Databases** -> **Create** -> **Database...**
   - Đặt tên là: `web_banh_keo`.

2. **Kích hoạt tính năng GIS:**
   - Chuột phải vào database `web_banh_keo` vừa tạo -> Chọn **Query Tool**.
   - Nhập lệnh sau và nhấn **F5**:
     ```sql
     CREATE EXTENSION postgis;
     ```

3. **Khôi phục dữ liệu (Restore):**
   - Chuột phải vào database `web_banh_keo` -> Chọn **Restore**.
   - Tại tab **General**, mục **Filename**, trỏ đến file backup đính kèm trong thư mục đồ án.
   - Nhấn **Restore** và đợi thông báo thành công (Process completed).

---

## 3. CÀI ĐẶT MÃ NGUỒN (VS CODE)

1. **Mở dự án:**
   - Mở thư mục chứa code bằng VS Code.


2. **Đồng bộ Database:**
   - Chạy các lệnh sau để đảm bảo cấu trúc bảng khớp với mã nguồn:
     ```bash
     python manage.py makemigrations
     python manage.py migrate
     ```

---

## 4. KHỞI CHẠY VÀ SỬ DỤNG

1. **Chạy Server:**
   - Tại Terminal, gõ lệnh:
     ```bash
     python manage.py runserver
     ```

2. **Truy cập:**
   - **Trang chủ (Bản đồ GIS):** [http://127.0.0.1:8000/](http://127.0.0.1:8000/)

---

## 5. LƯU Ý KỸ THUẬT
* **Lỗi Thư viện GIS:** Nếu chạy trên Windows gặp lỗi "Could not find module 'libgeos_c.dll'", hãy kiểm tra đường dẫn thư mục `bin` của PostgreSQL đã được cấu hình trong `GDAL_LIBRARY_PATH` tại file `settings.py`.