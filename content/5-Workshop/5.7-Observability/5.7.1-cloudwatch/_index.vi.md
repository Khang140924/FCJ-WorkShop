---
title: "Nhật ký & Chỉ số (CloudWatch)"
date: 2026-07-21
weight: 1
chapter: false
pre: " <b> 5.7.1. </b> "
---

### Giám sát với Amazon CloudWatch

Mặc định, tất cả các hàm AWS Lambda đều tự động đẩy log thực thi (những dòng lệnh `print()` hoặc `console.log()`) về **Amazon CloudWatch Logs**.

#### 1. Quản lý Log Groups
*   Mỗi hàm Lambda (như `Parse & Categorize Lambda`) sẽ có một Log Group riêng. 
*   Chúng ta có thể truy cập vào đây để kiểm tra dữ liệu JSON thô mà Amazon Textract hoặc Bedrock trả về, từ đó dễ dàng xác minh AI có đang phân loại chi tiêu chính xác hay không.

#### 2. Xây dựng Dashboard giám sát
Chúng ta tạo một **CloudWatch Dashboard** để theo dõi "sức khỏe" của toàn bộ nền tảng FinVantage trên một màn hình duy nhất. Các chỉ số (Metrics) quan trọng cần đưa lên:
*   **API Gateway:** Số lượng request (Count), Tỷ lệ lỗi (5XX Errors).
*   **Lambda:** Thời gian thực thi (Duration), Số lần gọi (Invocations), Số lần bị bóp băng thông (Throttles).
*   **RDS & ElastiCache:** Mức tiêu thụ CPU (CPU Utilization), Số lượng kết nối (DatabaseConnections) để kiểm chứng hiệu quả của RDS Proxy.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện **CloudWatch Dashboard** hiển thị các biểu đồ (Line chart hoặc Number) của các chỉ số Lambda và RDS mà bạn vừa thiết lập.
> *Mã Markdown:* `![CloudWatch Dashboard](../../../images/cloudwatch-dashboard.png)`