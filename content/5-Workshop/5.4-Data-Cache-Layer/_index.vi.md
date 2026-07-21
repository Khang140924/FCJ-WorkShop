---
title: "Tầng Dữ liệu và Bộ nhớ đệm"
date: 2026-07-20
weight: 4
chapter: true
pre: " <b> 5.4. </b> "
---

### Thiết kế Tầng Dữ liệu và Bộ nhớ đệm (Data Layer & Caching)

Chào các bạn! Trong chương này, chúng ta sẽ cùng đi qua việc thiết lập và xác minh tầng lưu trữ dữ liệu của dự án FinVantage. 

Để một ứng dụng tài chính cá nhân hoạt động mượt mà và an toàn, thiết kế tầng dữ liệu cần phân tách rõ ràng dựa trên đặc tính của từng loại thông tin. FinVantage sử dụng ba cơ chế lưu trữ chính để đạt hiệu năng tốt nhất:

1.  **Object Storage (Lưu trữ đối tượng):** Sử dụng **Amazon S3** để tiếp nhận và lưu trữ lâu dài các file ảnh, PDF hóa đơn gốc do người dùng tải lên.
2.  **Relational Database (Cơ sở dữ liệu quan hệ):** Sử dụng **Amazon RDS PostgreSQL** làm Single Source of Truth (nguồn dữ liệu chính xác duy nhất) để lưu trữ thông tin giao dịch, hạn mức ngân sách, tài khoản người dùng và kết quả phân tích AI có cấu trúc chặt chẽ.
3.  **In-memory Cache (Bộ nhớ đệm trên bộ nhớ trong):** Sử dụng **Amazon ElastiCache Valkey/Redis** để lưu trữ session đăng nhập và cache trung gian dữ liệu OCR của hóa đơn nhằm tối ưu hóa hiệu năng, giảm tải cho database và tăng tốc độ phản hồi.

---

### RDS Proxy - Giải pháp cho bài toán Serverless Connection

Một trong những "nỗi đau" kinh điển khi kết hợp mô hình Serverless Lambda với cơ sở dữ liệu truyền thống là lỗi **Connection Pool Exhaustion (cạn kiệt tài nguyên nhóm kết nối)**. Khi có hàng trăm request đồng thời, AWS Lambda sẽ tự động scale-up (nhân bản) lên hàng trăm instance chạy song song. Mỗi instance lại cố gắng mở một kết nối riêng vào RDS PostgreSQL, dẫn đến việc database bị tràn kết nối và crash (treo hệ thống).

Để giải quyết triệt để vấn đề này, FinVantage triển khai thêm **Amazon RDS Proxy** đóng vai trò làm màng trung gian gom và tái sử dụng các kết nối một cách thông minh, đảm bảo hệ thống luôn hoạt động ổn định bất kể lượng truy cập tăng đột biến.

---

### Lộ trình thiết lập tầng dữ liệu và bộ đệm:
1.  **Amazon S3 lưu hóa đơn:** Cấu hình lưu trữ tệp tin hóa đơn private và thiết lập CORS Rules.
2.  **Amazon RDS PostgreSQL:** Xác minh thông số cấu hình cơ sở dữ liệu quan hệ bảo mật.
3.  **Amazon RDS Proxy:** Kiểm tra màng quản lý kết nối RDS Proxy.
4.  **Amazon ElastiCache Valkey/Redis:** Cấu hình cụm Valkey/Redis lưu trữ session và OCR cache.
5.  **AWS Secrets Manager:** Quản lý an toàn các tài khoản và khóa kết nối nhạy cảm.
6.  **Migration database:** Xác nhận trạng thái nạp lược đồ cơ sở dữ liệu thành công.

Hãy cùng bắt đầu với Amazon S3 ở bài viết tiếp theo!
