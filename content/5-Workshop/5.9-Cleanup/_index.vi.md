---
title: "Dọn dẹp tài nguyên"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Dọn dẹp tài nguyên (Cleanup)

### Mục tiêu
Trang này sẽ hướng dẫn các bạn thực hiện quy trình dọn dẹp toàn bộ tài nguyên AWS đã tạo ra trong suốt Workshop FinVantage theo thứ tự an toàn, tránh phát sinh chi phí ngoài ý muốn và không bị vướng lỗi `Resource in use` (tài nguyên đang được sử dụng bởi dịch vụ khác).

### Tại sao phải dọn dẹp?
Trong môi trường Cloud, các dịch vụ hạ tầng sau sẽ **tính phí theo giờ** ngay cả khi không có lưu lượng truy cập thực tế:
*   **NAT Gateway:** ~$0.045/giờ (~$32/tháng).
*   **RDS PostgreSQL Instance:** Tùy instance class (~$15–$70/tháng).
*   **ElastiCache Valkey/Redis:** Tùy node type (~$12–$50/tháng).
*   **RDS Proxy:** ~$0.015/vCPU/giờ.

> ⚠️ **Cảnh báo:** Quên tắt các dịch vụ trên sau khi hoàn thành Lab là nguyên nhân hàng đầu dẫn đến hóa đơn AWS cuối tháng tăng đột biến.

---

### Quy trình dọn dẹp theo thứ tự an toàn

Thực hiện theo đúng thứ tự dưới đây để tránh lỗi phụ thuộc giữa các tài nguyên:

#### Bước 1: Xóa Backend Serverless (Lambda, API Gateway)
*   Nếu dự án được deploy (triển khai) bằng **Serverless Framework**, chạy lệnh sau trong terminal:
    ```bash
    npx serverless remove --stage prod
    ```
    Lệnh này sẽ tự động xóa: Toàn bộ các hàm Lambda, API Gateway REST API, CloudWatch Log Groups liên kết, và các IAM roles được Serverless Framework tự tạo.
*   Nếu deploy thủ công, xóa từng thành phần theo thứ tự: API Gateway → Lambda Functions → CloudWatch Log Groups.

#### Bước 2: Xóa Tầng Dữ liệu (Database & Cache)
*   **Amazon RDS Proxy:** Truy cập RDS Console → Proxies → Chọn proxy của FinVantage → **Delete**.
*   **Amazon ElastiCache:** Truy cập ElastiCache Console → Chọn cụm cluster Valkey/Redis → **Delete** (có thể bỏ qua bước tạo final snapshot).
*   **Amazon RDS PostgreSQL:** Truy cập RDS Console → Databases → Chọn database → **Delete**. Tắt tùy chọn Deletion protection trước nếu đang bật. Có thể bỏ qua chụp final snapshot nếu đây là môi trường lab.
*   **DB Subnet Group:** Xóa subnet group sau khi database đã bị xóa hoàn toàn.

#### Bước 3: Xóa S3 Bucket hóa đơn
*   Truy cập S3 Console → Chọn bucket `finvantage-invoices-hieu-2026-395840094907`.
*   Click **Empty bucket** (xóa sạch toàn bộ file hóa đơn bên trong bucket trước).
*   Sau khi bucket trống, click **Delete bucket**.

#### Bước 4: Xóa Frontend Hosting (Amplify)
*   Truy cập Amplify Console → Chọn ứng dụng FinVantage → **App settings** → **General** → Click **Delete app**.

#### Bước 5: Xóa Amazon Cognito User Pool
*   Truy cập Cognito Console → User pools → Chọn `ap-southeast-1_HQYkeSq33` → Click **Delete user pool**.

#### Bước 6: Xóa Secrets Manager
*   Truy cập Secrets Manager Console → Xóa các secrets: `finvantage/prod/app-auth` và `finvantage/prod/redis-url`.
*   *Lưu ý:* AWS Secrets Manager có thời gian chờ xóa tối thiểu 7 ngày theo mặc định. Bạn có thể chọn `Schedule deletion` với thời gian tối thiểu cho phép.

#### Bước 7: Dọn dẹp Hạ tầng Mạng (VPC)
*   **NAT Gateway:** Xóa NAT Gateway trước tiên → Chờ trạng thái chuyển thành `Deleted` (mất khoảng 1-2 phút).
*   **Elastic IP:** Truy cập EC2 Console → Elastic IPs → Release (giải phóng) Elastic IP liên kết với NAT Gateway đã xóa.
*   **VPC:** Sau khi tất cả các tài nguyên con đã xóa sạch, truy cập VPC Console → Chọn VPC của dự án → **Delete VPC**. AWS sẽ tự động xóa kèm: Subnets, Internet Gateway, Route Tables, Security Groups.

#### Bước 8: Xóa IAM Roles liên tài khoản
*   Truy cập IAM Console (tài khoản Backend) → Roles → Tìm và xóa các Lambda execution roles của dự án.
*   Truy cập IAM Console (tài khoản Bedrock) → Roles → Tìm và xóa role `FinVantageBedrockInvokeRole`.

---

> ⚠️ **Kiểm tra lần cuối:** Sau khi dọn dẹp xong, truy cập **AWS Billing Console** → **Bills** để xác nhận không còn dịch vụ nào đang tính phí phát sinh. Nếu phát hiện dịch vụ sót, tìm đúng region `ap-southeast-1` và xóa dịch vụ đó.

### Kết luận
Hoàn tất quy trình dọn dẹp này, tài khoản AWS của bạn đã trở về trạng thái sạch sẽ, đánh dấu sự hoàn thành trọn vẹn của Workshop FinVantage! 🎉