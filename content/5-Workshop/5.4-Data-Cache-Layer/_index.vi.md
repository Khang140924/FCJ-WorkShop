---
title: "Tầng Dữ liệu & Bộ đệm"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

### Thiết kế Tầng Dữ liệu Phân tán (Data Layer)

Trong kiến trúc của FinVantage, việc lưu trữ và truy xuất dữ liệu được phân tách rõ ràng dựa trên đặc thù của từng loại dữ liệu nhằm tối ưu hóa chi phí và hiệu năng. Hệ thống sử dụng ba cơ chế lưu trữ chính:

1.  **Object Storage (Lưu trữ đối tượng):** Sử dụng Amazon S3 để tiếp nhận và lưu trữ các file hóa đơn gốc (ảnh, PDF) do người dùng tải lên.
2.  **Relational Database (Cơ sở dữ liệu quan hệ):** Sử dụng Amazon RDS (MySQL) làm nguồn sự thật duy nhất (Single Source of Truth) để lưu trữ thông tin giao dịch, định danh và danh mục chi tiêu có cấu trúc chặt chẽ.
3.  **In-memory Cache (Bộ nhớ đệm):** Sử dụng Amazon ElastiCache (Redis) để tăng tốc độ truy xuất cho các báo cáo phân tích tài chính thường xuyên được gọi.

Đặc biệt, để giải quyết bài toán cạn kiệt kết nối (Connection Pool Exhaustion) – một "nỗi đau" kinh điển khi kết hợp AWS Lambda với cơ sở dữ liệu truyền thống – chúng ta sẽ triển khai thêm thành phần **Amazon RDS Proxy**.