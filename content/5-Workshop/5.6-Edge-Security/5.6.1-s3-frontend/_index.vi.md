---
title: "Lưu trữ Frontend (Amazon S3)"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.6.1. </b> "
---

### Triển khai Static Website Hosting

Thay vì phải duy trì một máy chủ (Server) chỉ để chạy giao diện web, kiến trúc Serverless tận dụng **Amazon S3** để lưu trữ các file tĩnh (HTML, CSS, JS) của Frontend (ví dụ: bộ code ReactJS hoặc VueJS sau khi đã `build`).

#### 1. Khởi tạo S3 Bucket cho Frontend
*   Tạo một Bucket mới với tên miền của dự án (ví dụ: `app.finvantage.com`).
*   Khác với các hướng dẫn cũ thường yêu cầu mở Public Access cho S3, chúng ta áp dụng tư duy bảo mật hiện đại: **Giữ nguyên cài đặt Block all public access**.
*   Không ai từ Internet có thể truy cập thẳng vào đường link S3 này để tải source code của chúng ta.

#### 2. Cấu hình phân phối tĩnh
*   Tải toàn bộ thư mục `build/` hoặc `dist/` của mã nguồn Frontend lên Bucket.
*   Thiết lập file trang chủ là `index.html` và file báo lỗi (Error document) cũng là `index.html` (để hỗ trợ định tuyến Client-side của các framework SPA như React/Vue).

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình thư mục các file tĩnh (index.html, static/css, static/js) đã được upload thành công lên Amazon S3 Bucket.
> *Mã Markdown:* `![Upload Frontend lên S3](../../../images/s3-frontend-files.png)`