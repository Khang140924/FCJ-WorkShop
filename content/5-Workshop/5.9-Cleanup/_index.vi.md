---
title: "Dọn dẹp Tài nguyên"
date: 2026-07-20
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

### Phá hủy Hạ tầng (FinOps Mindset)

Trong môi trường Cloud, việc quên tắt tài nguyên sau khi làm Lab là nguyên nhân hàng đầu dẫn đến các khoản phí khổng lồ phát sinh ngoài ý muốn (Đặc biệt là với NAT Gateway, RDS Multi-AZ và ElastiCache tính phí theo giờ).

Dưới đây là thứ tự dọn dẹp an toàn để không bị vướng lỗi "Resource in use":

1.  **Xóa Tầng Biên (Edge):** Vô hiệu hóa (Disable) và sau đó xóa (Delete) CloudFront Distribution. Xóa các luật trong AWS WAF.
2.  **Làm sạch Lưu trữ:** Truy cập Amazon S3, phải ấn "Empty bucket" (Xóa sạch toàn bộ file hóa đơn và code Frontend bên trong) thì mới có thể "Delete bucket".
3.  **Hủy Máy chủ & AI:** Xóa các REST API trong API Gateway. Xóa toàn bộ các hàm AWS Lambda, hàng đợi SQS và ngắt kết nối Amazon Bedrock.
4.  **Xóa Tầng Dữ liệu (Database):** Xóa RDS Proxy trước. Kế tiếp xóa Amazon ElastiCache Cluster. Cuối cùng, tiến hành xóa Amazon RDS Database (Có thể bỏ qua bước chụp Snapshot cuối cùng để tiết kiệm thời gian).
5.  **Dọn dẹp Hạ tầng Mạng (VPC):** Cực kỳ quan trọng: Xóa **NAT Gateway** trước tiên và **Release Elastic IP** trả lại cho AWS. Sau khi các dịch vụ bên trong đã sạch, tiến hành Delete VPC (AWS sẽ tự động xóa các Subnets, IGW và Route Tables đi kèm).
6.  **Xóa Quyền hạn:** Truy cập IAM Console để xóa các Roles đã tạo (Core-Lambda-Role, AI-Processing-Role).

Hoàn tất quy trình này, tài khoản AWS của bạn đã trở về trạng thái sạch sẽ, đánh dấu sự thành công trọn vẹn của Workshop FinVantage!