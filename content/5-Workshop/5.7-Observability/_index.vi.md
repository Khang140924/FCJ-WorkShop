---
title: "Giám sát & Cảnh báo"
date: 2026-07-20
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

### Khả năng Quan sát hệ thống (Observability)

Đối với một kiến trúc phân tán phi máy chủ (Serverless) kết hợp đa dịch vụ như FinVantage, việc dữ liệu chạy xuyên qua API Gateway, chui vào Lambda, gọi sang AI (Textract/Bedrock) rồi mới lưu xuống RDS khiến quá trình tìm lỗi (Debug) trở nên vô cùng phức tạp. 

Nếu hệ thống chậm hoặc phát sinh lỗi, chúng ta không thể "SSH vào server để xem log" theo cách truyền thống. Thay vào đó, chúng ta phải xây dựng năng lực **Observability (Khả năng quan sát)** toàn diện để thu thập số liệu (Metrics), vết tích (Traces) và nhật ký (Logs).

Trong phần này, chúng ta sẽ thực hành:
1. Thu thập và trực quan hóa Log hệ thống với Amazon CloudWatch.
2. Truy vết độ trễ của từng dịch vụ bằng AWS X-Ray.
3. Thiết lập hệ thống cảnh báo tự động qua Amazon SNS.