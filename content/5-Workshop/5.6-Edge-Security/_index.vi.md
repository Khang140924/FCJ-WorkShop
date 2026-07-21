---
title: "Tầng Biên & Bảo mật"
date: 2026-07-20
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

### Thiết lập Lớp bảo vệ mặt tiền (Edge Layer)

Bảo mật hạ tầng bên trong (Private Subnets) là chưa đủ. Một hệ thống tài chính như FinVantage cần được bảo vệ ngay từ điểm chạm đầu tiên với người dùng trên Internet. Lớp bảo mật biên (Edge Security) sẽ giúp chúng ta giải quyết ba bài toán lớn:

1.  **Phân phối toàn cầu:** Tải giao diện ứng dụng (Frontend) siêu tốc dù người dùng ở bất kỳ đâu trên thế giới.
2.  **Lọc nhiễu & Chống tấn công:** Ngăn chặn các cuộc tấn công từ chối dịch vụ (DDoS) hoặc các mã độc (SQL Injection, XSS) nhắm vào API.
3.  **Quản lý Danh tính:** Xác thực người dùng an toàn, cấp phát token hợp lệ trước khi cho phép truy cập dữ liệu cá nhân.

Trong phần này, chúng ta sẽ thực hành cấu hình chuỗi dịch vụ bảo mật biên bao gồm: Amazon S3 (Static Hosting), Amazon CloudFront, AWS WAF và Amazon Cognito.