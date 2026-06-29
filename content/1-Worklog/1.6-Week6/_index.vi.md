---
title: "Worklog Tuần 6"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Nghiên cứu các loại hình dịch vụ cơ sở dữ liệu SQL và NoSQL trên môi trường đám mây AWS.
* Tìm hiểu và thực hành dịch vụ cơ sở dữ liệu quan hệ Amazon RDS (MySQL/PostgreSQL).
* Khám phá và thực hành dịch vụ cơ sở dữ liệu NoSQL hiệu năng cao Amazon DynamoDB.
* Tìm hiểu cơ chế bảo mật, sao lưu tự động và tính năng sẵn sàng cao Multi-AZ cho cơ sở dữ liệu.
* Thực hành cấu hình kết nối an toàn giữa ứng dụng trên máy chủ EC2 tới hệ thống cơ sở dữ liệu.
* Hoàn thành các nhiệm vụ thực hành (Labs) bổ sung để kiếm AWS Credit.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu lý thuyết về các loại dịch vụ cơ sở dữ liệu trên nền tảng AWS: Relational Database (RDS) và Non-relational Database (NoSQL) <br> - Theo dõi các bài giảng về Database on AWS | 08/06/2026   | 08/06/2026      | Youtube AWS Study Group |
| 3   | - Tìm hiểu chi tiết Amazon RDS, DynamoDB và cơ chế Managed Service <br> - Nghiên cứu cơ chế bảo mật, sao lưu dữ liệu (Backup) và tính năng sẵn sàng cao (Multi-AZ Deployment) | 09/06/2026   | 09/06/2026      | Platform Bootcamp |
| 4   | - **Thực hành RDS:** <br>&emsp; + Khởi tạo RDS DB Instance (MySQL/PostgreSQL) trong Private Subnet <br>&emsp; + Cấu hình Security Group cho phép EC2 kết nối tới cơ sở dữ liệu | 10/06/2026   | 10/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Thực hành DynamoDB:** <br>&emsp; + Tạo bảng và tìm hiểu Primary Key (Partition & Sort Key) <br>&emsp; + Thêm dữ liệu (PutItem) và truy vấn trên giao diện Console | 11/06/2026   | 11/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành nâng cao (Kiếm AWS Credit):** <br>&emsp; + Task 3: Set up AWS Budgets (Tích lũy $20 credit) <br>&emsp; + Task 4: Create Lambda Web App (Tích lũy $20 credit) | 12/06/2026   | 12/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 6:

* Nắm vững sự khác biệt giữa Amazon RDS (phù hợp ứng dụng cần tính nhất quán cao, quan hệ phức tạp) và Amazon DynamoDB (phù hợp ứng dụng cần tốc độ truy xuất cực nhanh, dữ liệu linh hoạt, quy mô lớn).

* Hiểu rõ khái niệm Managed Service: AWS sẽ đảm nhận việc cài đặt, vá lỗi hệ điều hành và sao lưu, giúp lập trình viên tập trung hoàn toàn vào thiết kế cấu trúc dữ liệu và viết code Backend.

* Hiểu rõ cơ chế Multi-AZ: Cách AWS tự động chuyển đổi sang một bản sao cơ sở dữ liệu ở Vùng sẵn sàng khác khi có sự cố, đảm bảo ứng dụng không bị gián đoạn.

* Khởi tạo thành công RDS DB Instance chạy hệ quản trị cơ sở dữ liệu MySQL/PostgreSQL an toàn bên trong vùng mạng Private Subnet.

* Thực hành cấu hình Security Group chuẩn xác, cho phép máy chủ Backend (chạy trên EC2) kết nối thông suốt tới cổng 3306 hoặc 5432 của cơ sở dữ liệu.

* Thao tác thành thạo trên Amazon DynamoDB: tạo bảng dữ liệu, thiết lập Primary Key, thêm dữ liệu (PutItem) và thực hiện các truy vấn trên giao diện Console.

* Biết cách sử dụng tính năng Snapshot để sao lưu dữ liệu thủ công và thiết lập lịch sao lưu tự động cho hệ thống cơ sở dữ liệu.

* Tích lũy kinh nghiệm thực tiễn: Kết nối ứng dụng Backend tới Database thông qua các Endpoint thay vì dùng địa chỉ IP tĩnh, giúp hệ thống linh hoạt hơn khi cần nâng cấp hoặc bảo trì.

* Hình thành tư duy kiến trúc: Biết lựa chọn giải pháp lưu trữ dữ liệu tối ưu giữa SQL (đảm bảo tính toàn vẹn) và NoSQL (xử lý lượng truy cập khổng lồ).

* Hoàn thành xuất sắc 2 bài Lab mở rộng (Task 3: Set up AWS Budgets và Task 4: Create Lambda Web App), qua đó kiếm thêm được $40 AWS Credit để phục vụ cho các dự án thực hành tiếp theo.