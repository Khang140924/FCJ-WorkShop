---
title: "Worklog Tuần 7"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu tuần 7:

* Nghiên cứu lý thuyết tổng quan về mô hình kiến trúc không máy chủ (Serverless Architecture).
* Tìm hiểu nguyên lý hoạt động của AWS Lambda, Amazon API Gateway, Amazon SQS và SNS.
* Thực hành khởi tạo hàm Lambda, thiết lập cơ chế kích hoạt tự động dựa trên sự kiện (Event Triggers).
* Triển khai cấu hình REST API qua API Gateway để tạo cổng kết nối an toàn cho ứng dụng Backend.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu lý thuyết về mô hình điện toán không máy chủ (Serverless Architecture) trên nền tảng AWS. <br> - Theo dõi bài giảng chuyên sâu về Serverless Services và Message Queue. | 15/06/2026   | 15/06/2026      | Youtube AWS Study Group |
| 3   | - Tìm hiểu AWS Lambda, cơ chế kích hoạt (Triggers), Amazon SQS, SNS và API Gateway. <br> - Đọc tài liệu hướng dẫn cách đóng gói mã nguồn, quản lý biến môi trường và thiết lập thời gian chạy (Runtime). | 16/06/2026   | 16/06/2026      | Platform Bootcamp |
| 4   | - **Thực hành:** Khởi tạo hàm Lambda cơ bản và cấu hình môi trường Runtime tương thích. <br> - Cấu hình REST API trên Amazon API Gateway để tạo điểm cuối (Endpoint) tiếp nhận yêu cầu từ người dùng. | 17/06/2026   | 17/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Thực hành:** Thiết lập cơ chế kích hoạt (Triggers) để hàm Lambda tự động chạy khi có sự kiện xuất hiện (ví dụ: có file ảnh mới tải lên S3 Bucket). | 18/06/2026   | 18/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành:** Khởi tạo hàng đợi Amazon SQS để thử nghiệm cơ chế gửi và nhận thông điệp giữa hai dịch vụ độc lập. | 19/06/2026   | 19/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 7:

* Nắm vững tư duy thiết kế Serverless: Hiểu rõ lợi ích của việc không cần quản lý hạ tầng máy chủ, hệ thống tự động mở rộng theo lượng request và chỉ tính phí trên thời gian chạy thực tế.

* Phân biệt rõ cơ chế truyền thông điệp bất đồng bộ: Amazon SQS (mô hình hàng đợi Pull giải tải hệ thống) và Amazon SNS (mô hình Pub/Sub đẩy thông báo Push tới nhiều nơi).

* Hiểu cách API Gateway hoạt động như một lớp bảo vệ vòng ngoài, tiếp nhận và điều hướng an toàn các luồng traffic từ Internet vào các hàm xử lý bên trong.

* Khởi tạo thành công AWS Lambda Function, cấu hình Runtime tương thích và tự viết đoạn mã xử lý logic ngắn.

* Cấu hình thành công REST API trên Amazon API Gateway, tích hợp với hàm Lambda để tiếp nhận các phương thức HTTP (GET/POST) và trả kết quả cho Client.

* Thực hành thiết lập Triggers tự động hóa quy trình khi có sự kiện trên Amazon S3.

* Triển khai hàng đợi Amazon SQS thành công, giúp hệ thống không bị nghẽn dữ liệu khi giao tiếp giữa các dịch vụ độc lập.

* Học hỏi tư duy xây dựng kiến trúc hướng sự kiện (Event-driven Architecture) và Microservices, giúp giảm thiểu sự phụ thuộc lẫn nhau (Loose Coupling) cho các dịch vụ Backend.

* Nhận thức được cách Serverless tối ưu hóa chi phí doanh nghiệp: Thay thế máy chủ EC2 bật 24/7 bằng AWS Lambda cho các tác vụ chạy ngắn hạn hoặc ít tần suất.