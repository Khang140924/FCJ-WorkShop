---
title: "AWS X-Ray và CloudTrail"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### AWS X-Ray và CloudTrail (Thành phần đề xuất)

> ⚠️ **LƯU Ý QUAN TRỌNG:**  
> **Thành phần mở rộng/đề xuất, chưa xác nhận đã được triển khai trong hệ thống production hiện tại.**  
> Để giảm thiểu độ phức tạp cấu hình và tiết kiệm dung lượng lưu trữ trên tài khoản AWS thử nghiệm/lab của sinh viên, các dịch vụ truy vết chuyên sâu AWS X-Ray và ghi nhật ký hoạt động AWS CloudTrail tạm thời chưa được kích hoạt trên hệ thống hiện tại. Phần này cung cấp giải pháp lý thuyết để nâng cấp khả năng quan sát hệ thống trong môi trường doanh nghiệp thực tế.

---

### Mục tiêu
Trang này sẽ giới thiệu lý thuyết và vai trò thiết kế của hai dịch vụ **AWS X-Ray** và **AWS CloudTrail** trong việc kiểm toán an ninh mạng, phân tích latency (độ trễ phản hồi của hệ thống) và truy vết luồng thực thi của request xuyên suốt hệ thống **FinVantage**.

---

### 1. Truy vết phân tán với AWS X-Ray

Trong kiến trúc microservices phi máy chủ, khi một người dùng gửi hóa đơn lên, request sẽ đi qua một chuỗi các trạm: Trình duyệt → API Gateway → Lambda `importInvoice` → S3 → Lambda `ocrInvoice` → Textract → Redis → Lambda `analyzeInvoice` → Bedrock → RDS Proxy → PostgreSQL. Nếu API phản hồi chậm mất 10 giây, rất khó để biết chính xác chặng nào đang bị kẹt.

AWS X-Ray giải quyết bài toán này thông qua:
*   **Active tracing (truy vết hoạt động):** Khi kích hoạt trên API Gateway và Lambda, X-Ray tự động đính kèm một mã `X-Amzn-Trace-Id` độc nhất vào tiêu đề (Header) của request. Mã này sẽ đi xuyên suốt qua toàn bộ các dịch vụ AWS.
*   **Service map (bản đồ liên kết dịch vụ):** X-Ray tự động trực quan hóa sơ đồ mạng lưới các thành phần liên kết của FinVantage dưới dạng các nút (node) tròn biểu diễn mối quan hệ gọi nhau và thời gian phản hồi tương ứng.
*   **Traces Timeline (Biểu đồ Gantt phân tích thời gian):** Cung cấp biểu đồ thanh thời gian chi tiết của từng bước chạy. Giúp bạn phát hiện ngay lập tức nguyên nhân chậm trễ: Do câu lệnh truy vấn PostgreSQL bị chậm, do Textract nhận diện ảnh nặng hay do mô hình Bedrock Claude 3.5 Sonnet phản hồi chậm.

---

![Hình 5.7.2a. Bản đồ liên kết dịch vụ (Service Map) trực quan hóa các nút mạng của AWS X-Ray khi thực thi luồng ocrInvoice.](../../../images/finvantage-xray-service-map.jpg)

---

### 2. Nhật ký kiểm toán an ninh với AWS CloudTrail

Bên cạnh việc theo dõi hiệu năng của code (CloudWatch) và truy vết luồng đi (X-Ray), một ứng dụng tài chính bắt buộc phải lưu trữ audit log (nhật ký kiểm toán) để ghi nhận: *"Ai đã thao tác gì, vào lúc nào trên hệ thống AWS?"*. AWS CloudTrail là dịch vụ giải quyết yêu cầu này:
*   **Ghi nhận API calls (các yêu cầu gọi API):** CloudTrail tự động ghi lại lịch sử mọi hành động được thực hiện bởi người dùng IAM, các role của Lambda, hoặc các dịch vụ AWS khác (ví dụ: Lambda gọi API Textract, sửa cấu hình database, thay đổi quyền bucket S3).
*   **Bảo mật an toàn:** Nhật ký kiểm toán CloudTrail sẽ được lưu trữ an toàn trong một S3 Bucket bảo mật được mã hóa và bật chế độ chống ghi đè (Object Lock) để đảm bảo hacker không thể xóa dấu vết sau khi thâm nhập.

---

![Hình 5.7.2b. Nhật ký kiểm toán các thao tác API liên quan tới s3.amazonaws.com được ghi nhận trên AWS CloudTrail.](../../../images/finvantage-cloudtrail-events.jpg)

---

### Các lỗi thường gặp khi chạy X-Ray
*   **Lỗi: `Missing X-Ray daemon connection / Error sending segment`**
    *   *Nguyên nhân:* Lambda được bật Active Tracing nhưng IAM execution role của Lambda thiếu quyền ghi dữ liệu về X-Ray daemon (`xray:PutTraceSegments`).
    *   *Cách xử lý:* Gắn thêm AWS managed policy `AWSXrayWriteOnlyAccess` vào Lambda IAM execution role.

### Kết luận ngắn
AWS X-Ray và CloudTrail là hai công cụ cao cấp giúp nâng cao độ tin cậy và mức độ an toàn thông tin của FinVantage lên chuẩn doanh nghiệp lớn.
