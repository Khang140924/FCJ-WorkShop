---
title: "Logic cốt lõi (AWS Lambda)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### Triển khai các Hàm xử lý phi máy chủ

Dựa theo nguyên tắc Microservices, thay vì viết một cục code khổng lồ, chúng ta chia nhỏ logic ra thành các hàm **AWS Lambda** độc lập, mỗi hàm đảm nhận một nhiệm vụ duy nhất (Single Responsibility).

#### 1. Import Lambda & Payment Lambda
*   **Payment Lambda:** Xử lý các giao dịch người dùng tự nhập bằng tay. Nó kết nối qua RDS Proxy để ghi dữ liệu trực tiếp vào MySQL.
*   **Import Lambda:** Nhận luồng dữ liệu (Base64 hoặc binary) từ API Gateway. Nhiệm vụ của nó rất nhẹ nhàng: upload file hóa đơn lên S3 Bucket (Raw Files).

#### 2. Cấu hình Mạng (VPC Configuration) cho Lambda
Đây là bước cực kỳ quan trọng để Lambda có thể nhìn thấy Database:
*   Trong cấu hình của hàm Lambda, bật tính năng **VPC**.
*   Gán hàm Lambda vào **2 Private Subnets** đã tạo ở Phần 5.3.
*   Gắn **Lambda-SG** (Security Group) cho nó để cho phép gọi ra ngoài và chui vào RDS/ElastiCache.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình phần cấu hình **VPC** bên trong giao diện cấu hình của một hàm Lambda (ví dụ `Payment Lambda`), hiển thị rõ Subnets và Security Group đang được gán.
> *Mã Markdown:* `![Cấu hình VPC cho Lambda](../../../images/lambda-vpc-config.png)`