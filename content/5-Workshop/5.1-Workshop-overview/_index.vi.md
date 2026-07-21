---
title: "Tổng quan Workshop"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

### Giới thiệu bài toán thực tế

Việc quản lý tài chính cá nhân thủ công thường gặp nhiều khó khăn: người dùng phải tự nhập liệu từng hóa đơn, dễ sai sót và mất thời gian. Bên cạnh đó, các hệ thống xử lý hóa đơn truyền thống thường quá tải khi lượng dữ liệu tăng vọt vào những ngày cuối tháng.

Workshop này sẽ hướng dẫn bạn từng bước cách xây dựng **FinVantage** – một giải pháp điện toán đám mây hoàn toàn phi máy chủ (Serverless), có khả năng tự động co giãn, tự động trích xuất dữ liệu hóa đơn bằng Trí tuệ nhân tạo (AI) và bảo mật nhiều lớp trên AWS để giải quyết triệt để bài toán trên.

### Sơ đồ Kiến trúc (Architecture Diagram)

Hệ thống FinVantage được thiết kế với kiến trúc hướng sự kiện (Event-driven Architecture), đảm bảo tính sẵn sàng cao (High Availability) và phân tách rõ ràng luồng dữ liệu.

![Sơ đồ kiến trúc hệ thống FinVantage](../../images/finvantage-architecture.png)

*Hình 5.1.1: Sơ đồ luồng dữ liệu kiến trúc FinVantage trên AWS.*

### Giải thích các thành phần lõi

Dựa vào sơ đồ kiến trúc, hệ thống được chia thành các phân lớp cụ thể sau:

*   **Tầng Biên & Bảo mật (Entry & Security Layer):** Người dùng gửi HTTPS request đi qua AWS WAF (chống tấn công) và Amazon CloudFront (tăng tốc độ tải). Quá trình xác thực được quản lý bởi Amazon Cognito.
*   **Tầng Xử lý API (Compute Layer):** Amazon API Gateway đóng vai trò làm cửa ngõ định tuyến các API calls đến các hàm AWS Lambda tương ứng (`Payment Lambda`, `Import Lambda`, `Analysis Lambda`).
*   **Tầng AI & Xử lý tự động (AI Integration):** Khi có hóa đơn tải lên S3, AWS Lambda sẽ gọi **Amazon Textract** để thực hiện OCR (nhận diện chữ) và truyền sang **Amazon Bedrock** để AI phân loại chi tiêu thông minh.
*   **Tầng Dữ liệu (Data Layer):** Nằm an toàn trong Private Subnet. Sử dụng Amazon RDS (MySQL) lưu trữ dữ liệu người dùng, kết hợp với Amazon RDS Proxy để tránh quá tải kết nối và Amazon ElastiCache (Redis) để làm bộ đệm tốc độ cao.
*   **Tầng Bất đồng bộ (Async Processing):** Sử dụng Amazon SQS để tạo hàng đợi xử lý các tác vụ nặng (như bóc tách nhiều hóa đơn cùng lúc) thông qua `Worker Lambda`, kết hợp Amazon SNS để gửi cảnh báo tài chính.

### Lộ trình thực hành chi tiết

Trong các phần tiếp theo, chúng ta sẽ lần lượt đi sâu vào việc khởi tạo hạ tầng VPC, thiết lập cơ sở dữ liệu, viết code cho các hàm Lambda tích hợp AI và cuối cùng là cấu hình lớp bảo mật bên ngoài.