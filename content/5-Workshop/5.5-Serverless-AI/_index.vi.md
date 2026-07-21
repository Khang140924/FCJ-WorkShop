---
title: "Serverless và trí tuệ nhân tạo"
date: 2026-07-20
weight: 5
chapter: true
pre: " <b> 5.5. </b> "
---

### Trái tim của FinVantage: Serverless và Trí tuệ nhân tạo (AI)

Chào các bạn! Sau khi đã dựng xong hạ tầng mạng an toàn và cơ sở dữ liệu ở các chương trước, giờ là lúc chúng ta tiến vào xây dựng "phần hồn" của FinVantage. Đây chính là tầng xử lý logic nghiệp vụ và tích hợp Trí tuệ nhân tạo để tự động hóa quy trình bóc tách hóa đơn.

FinVantage ứng dụng hoàn toàn kiến trúc **Serverless (phi máy chủ)**. Thay vì tốn tiền thuê máy chủ EC2 truyền thống chạy 24/7 gây lãng phí tài nguyên, chúng ta sử dụng các dịch vụ tính toán theo sự kiện của AWS. Hệ thống sẽ tự động co giãn theo lượng request (yêu cầu) thực tế và bạn chỉ phải trả tiền cho từng mili-giây mà code thực sự chạy.

---

### Các thành phần chính trong tầng này:

1.  **Amazon API Gateway:** Cổng tiếp nhận toàn bộ các HTTP requests từ Frontend gửi lên, đóng vai trò định tuyến lưu lượng vào các hàm Lambda tương ứng.
2.  **AWS Lambda (Node.js 24):** Nơi chứa toàn bộ mã nguồn backend xử lý logic nghiệp vụ (Auth, CRUD hóa đơn, phân tích AI, tính toán ngân sách, v.v.).
3.  **Amazon Textract:** Dịch vụ AI bóc tách thông tin chữ viết thô từ hóa đơn do người dùng tải lên.
4.  **Amazon Bedrock (Claude 3.5 Sonnet):** Mô hình AI giúp phân tích dữ liệu, tự động phân loại danh mục chi tiêu và đưa ra lời khuyên tài chính cá nhân thông minh.

Đặc biệt, hệ thống FinVantage của chúng ta triển khai một cơ chế nâng cao rất phổ biến ở các doanh nghiệp: **Cross-account Bedrock Invoke (gọi Bedrock chéo tài khoản)**. Lambda backend ở tài khoản hiện tại sẽ thực hiện AssumeRole (ủy quyền vai trò) sang một tài khoản AWS khác (nơi chứa tài nguyên Bedrock và model Claude 3.5 Sonnet) để thực thi phân tích dữ liệu, giúp tối ưu hóa quản lý tài nguyên tập trung.

---

### Lộ trình thực hành trong chương này:

Chúng ta sẽ lần lượt xác minh và tìm hiểu cách triển khai qua 4 trang chi tiết:

1.  **Bài 5.5.1. Amazon API Gateway:** Kiểm tra cấu hình API Routes, stage prod và CORS.
2.  **Bài 5.5.2. Thiết kế Lambda theo chức năng:** Đi sâu vào cấu hình chi tiết, biến môi trường, tài nguyên mạng và IAM Role của từng Lambda function (hàm xử lý Lambda) nghiệp vụ.
3.  **Bài 5.5.3. Tích hợp AI (Textract & Bedrock):** Phân tích mã nguồn gọi Textract, cấu hình vai trò liên tài khoản (cross-account IAM role) cho Bedrock và xem log kết quả CloudWatch.
4.  **Bài 5.5.4. Amazon SQS và Worker Lambda (Thành phần mở rộng):** Tìm hiểu giải pháp kiến trúc đề xuất sử dụng SQS Queue và DLQ để xử lý tác vụ bất đồng bộ trong tương lai.

Hãy cùng bước vào bài viết đầu tiên về API Gateway ngay sau đây!
