# Bài 3: Đóng gói trang Web HTML tĩnh với Dockerfile

## 1. Giới thiệu
Mục tiêu của bài tập là viết Dockerfile ngắn gọn để đóng gói một trang web HTML tĩnh vào trong Docker image sử dụng web server Nginx (phiên bản gọn nhẹ `alpine`).

---

## 2. Cấu trúc thư mục

```text
homework/session_09/ex3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp tin

### 3.1. `index.html`
```html
<h1>Hello Docker Session 09!</h1>
```

### 3.2. `Dockerfile`
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

**Giải thích:**
- `FROM nginx:alpine`: Sử dụng base image Nginx chạy trên Alpine Linux để tối ưu dung lượng (nhẹ, bảo mật).
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ máy host vào thư mục phục vụ web mặc định của Nginx trong container.

---

## 4. Hướng dẫn chạy và kiểm tra

### Bước 1: Build Docker Image
Chạy lệnh sau tại thư mục chứa Dockerfile:
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy Container
Chạy container ở chế độ nền (detached) và ánh xạ cổng máy host `8081` sang cổng `80` của container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra kết quả
Sử dụng `curl` hoặc mở trình duyệt web:
```bash
curl http://localhost:8081
```

Hoặc truy cập trình duyệt tại địa chỉ: `http://localhost:8081`

### Kết quả mong đợi:
```html
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Dọn dẹp Container sau khi kiểm thử (Tùy chọn)

Để dừng và xóa container sau khi hoàn thành:
```bash
docker stop html-app
docker rm html-app
```
Xóa image nếu không còn sử dụng:
```bash
docker rmi my-html-app:v1
```
