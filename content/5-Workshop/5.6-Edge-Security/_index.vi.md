---
title: "Lớp biên, bảo mật và hosting"
date: 2026-07-20
weight: 6
chapter: true
pre: " <b> 5.6. </b> "
---

### Thiết lập Lớp biên, Bảo mật và Hosting (Edge Security & Hosting)

Chào các bạn! Sau khi đã xây dựng xong tầng Serverless xử lý logic nghiệp vụ và trí tuệ nhân tạo ở chương trước, nhiệm vụ của chúng ta trong chương này là đưa Frontend (giao diện người dùng) của FinVantage lên chạy online, cấu hình định danh Cognito và thiết lập màng bảo vệ biên để hệ thống có thể tiếp cận người dùng một cách an toàn nhất.

Một ứng dụng tài chính cá nhân cần được bảo vệ và tối ưu hóa ngay tại điểm chạm đầu tiên trên Internet (Edge location - điểm phân phối biên mạng toàn cầu). Lớp bảo mật biên giúp giải quyết ba bài toán lớn:

1.  **Hosting & Caching tốc độ cao:** Phân phối giao diện Frontend React/Vite đến người dùng với độ trễ cực thấp thông qua mạng lưới CDN toàn cầu của AWS.
2.  **Quản lý danh tính người dùng:** Đăng ký, đăng nhập và cấp phát phiên làm việc an toàn thông qua Amazon Cognito làm Identity provider (dịch vụ quản lý định danh người dùng).
3.  **Lọc traffic & Chống tấn công (Đề xuất):** Thiết lập AWS WAF để lọc mã độc (SQL Injection, XSS) và giới hạn tần suất truy cập bảo vệ các API endpoints.

---

### Các dịch vụ được kiểm tra và thiết lập trong chương này:

Chúng ta sẽ lần lượt đi qua 4 trang thực hành chi tiết:

1.  **Bài 5.6.1. AWS Amplify Hosting:** Hướng dẫn upload đóng gói mã nguồn Frontend tĩnh lên Amplify Hosting, kiểm tra lịch sử deploy và cấu hình rewrite/redirect (SPA fallback và auth reverse proxy).
2.  **Bài 5.6.2. CloudFront CDN:** Tìm hiểu cách AWS Amplify tích hợp CloudFront CDN để cache và phân phối tài nguyên tĩnh.
3.  **Bài 5.6.3. AWS WAF (Lớp bảo vệ đề xuất):** Tìm hiểu lý thuyết về tường lửa bảo vệ API Gateway và chi phí vận hành.
4.  **Bài 5.6.4. Amazon Cognito:** Xác minh cấu hình User Pool, Hosted UI (giao diện đăng nhập được AWS lưu trữ sẵn), kiểm tra callback URL và quản lý danh sách tài khoản người dùng thực tế.

Hãy cùng bắt đầu với AWS Amplify Hosting ở trang tiếp theo!