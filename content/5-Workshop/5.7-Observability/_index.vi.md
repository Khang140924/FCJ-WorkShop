---
title: "Giám sát và Quan sát hệ thống"
date: 2026-07-20
weight: 7
chapter: true
pre: " <b> 5.7. </b> "
---

### Khả năng giám sát và quan sát hệ thống (Observability)

Chào các bạn! Đối với một hệ thống phân tán Serverless chạy đa dịch vụ như FinVantage, các request (yêu cầu) đi xuyên qua API Gateway, kích hoạt Lambda backend, gọi sang AI (Textract/Bedrock) rồi cuối cùng mới lưu dữ liệu xuống RDS Proxy và PostgreSQL. Nếu có bất kỳ mắt xích nào bị lỗi hoặc chạy chậm, việc tìm nguyên nhân (debug) sẽ vô cùng phức tạp.

Vì không có máy chủ EC2 truyền thống chạy 24/7 để chúng ta "SSH vào xem log", chúng ta phải xây dựng năng lực **Observability (khả năng giám sát và quan sát hệ thống)** tập trung dựa trên 3 trụ cột: Metrics (các chỉ số đo lường hiệu năng), Logs (nhật ký ghi nhận hoạt động) và Traces (vết tích luồng thực thi cuộc gọi).

---

### Các nội dung thực hành trong chương này:

Chúng ta sẽ lần lượt tìm hiểu và thực hành qua 3 bài viết chi tiết:

1.  **Bài 5.7.1. Amazon CloudWatch:** Dịch vụ ghi log và thu thập metrics thực tế của dự án. Hướng dẫn cách tra cứu CloudWatch Logs của các hàm Lambda và cách tạo Dashboard (bảng điều khiển) trực quan theo dõi lượng API calls.
2.  **Bài 5.7.2. AWS X-Ray và CloudTrail (Thành phần đề xuất):** Tìm hiểu giải pháp truy vết (tracing) luồng đi của request và ghi nhận nhật ký thao tác API toàn hệ thống.
3.  **Bài 5.7.3. Cảnh báo tự động qua Amazon SNS (Thành phần đề xuất):** Tìm hiểu giải pháp thiết lập CloudWatch Alarm (cảnh báo chỉ số vượt ngưỡng) để tự động gửi thông báo email cho quản trị viên qua SNS topic (chủ đề thông báo).

Hãy cùng bắt đầu bài thực hành thực tế đầu tiên với Amazon CloudWatch ngay sau đây!
