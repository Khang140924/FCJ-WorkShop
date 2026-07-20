---
title: "Worklog Tuần 9"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

* Phối hợp nhóm xây dựng kiến trúc hệ thống phân tích tài chính thông minh FinVantage.
* Nghiên cứu lý thuyết và cấu hình phân hệ cảnh báo bằng Amazon SNS và giám sát hệ thống qua Amazon CloudWatch.
* Đảm nhận nhiệm vụ Thành viên 4: Thiết kế luồng phản hồi cho người dùng và quản lý quy chuẩn sơ đồ hệ thống.
* Sử dụng công cụ Draw.io và bộ Icon AWS để tổng hợp, chuẩn hóa sơ đồ kiến trúc tổng thể nằm trong khung Region/VPC.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Phối hợp làm việc nhóm để triển khai dự án FinVantage sử dụng công nghệ AWS và Generative AI. <br> - Trao đổi với các thành viên để làm rõ luồng đi của dữ liệu từ cổng vào đến lớp cảnh báo đầu ra. | 29/06/2026   | 29/06/2026      | Nhóm dự án |
| 3   | - Nghiên cứu lý thuyết, kiến trúc phân hệ thông báo Amazon SNS và công cụ giám sát Amazon CloudWatch. <br> - Đọc tài liệu quy chuẩn thiết kế sơ đồ hạ tầng trên hệ thống Platform Bootcamp. | 30/06/2026   | 30/06/2026      | Platform Bootcamp & Youtube AWS Study Group |
| 4   | - **Thực hành:** Thiết kế và cấu hình phân hệ thông báo đầu ra sử dụng Amazon SNS. <br> - Cấu hình các bộ lọc log và thiết lập ngưỡng cảnh báo trên Amazon CloudWatch. | 01/07/2026   | 01/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Sử dụng công cụ Draw.io kết hợp bộ Icon chính thức của AWS để thiết kế và chuẩn hóa sơ đồ kiến trúc tổng thể. | 02/07/2026   | 02/07/2026      | Draw.io |
| 6   | - Thực hiện sắp xếp thẳng hàng các khối chức năng, bao bọc toàn bộ dịch vụ trong các khung Region, mạng ảo VPC và gắn nhãn chính xác cho từng thành phần. | 03/07/2026   | 03/07/2026      | Draw.io |


### Kết quả đạt được tuần 9:

* Nắm vững nguyên lý hoạt động của dịch vụ thông báo Amazon SNS theo kiến trúc gửi/nhận (Publish/Subscribe) để gửi Email hoặc SMS tự động tới người dùng khi có cảnh báo tài chính.

* Hiểu sâu về vai trò của Amazon CloudWatch trong việc thu thập số liệu metrics, giám sát hiệu năng phần cứng và phát hiện kịp thời các lỗi phát sinh (logs) từ các hàm AWS Lambda.

* Nắm chắc quy chuẩn thiết kế sơ đồ hạ tầng đám mây chuyên nghiệp, bao gồm cách phân vùng hệ thống bằng khung mạng ảo Amazon VPC, phân chia các lớp Subnet và cách vẽ mũi tên một chiều theo đúng luồng xử lý dữ liệu.

* Thiết kế và cấu hình thành công phân hệ thông báo đầu ra sử dụng Amazon SNS để gửi các cảnh báo tiêu dùng vượt ngưỡng hoặc lời khuyên tài chính cá nhân hóa đến thiết bị của người dùng.

* Cấu hình các bộ lọc log và thiết lập các ngưỡng cảnh báo tự động trên Amazon CloudWatch nhằm tối ưu hóa hoạt động vận hành (Ops) của hệ thống.

* Hoàn thiện sơ đồ kiến trúc tổng thể cho dự án FinVantage trên Draw.io; thực hiện sắp xếp thẳng hàng các khối chức năng, bao bọc toàn bộ dịch vụ trong các khung Region và mạng ảo VPC theo đúng tiêu chuẩn thiết kế.

* Thực hiện gắn nhãn chính xác cho từng thành phần trong sơ đồ (ví dụ: gán nhãn chức năng cụ thể cho các hàm Lambda xử lý) giúp sơ đồ trở nên trực quan, dễ đọc.

* Tích lũy được kinh nghiệm làm việc nhóm (Teamwork) thực tế trong một dự án công nghệ, biết cách kết nối cấu phần của mình với phần việc của các thành viên khác để tạo ra một sản phẩm hoàn chỉnh.

* Nâng cao tư duy thiết kế hệ thống tổng thể (System Architecture Design) - một kỹ năng cực kỳ cao cấp và giá trị đối với một Kỹ sư Backend / Cloud Engineer khi bước vào các dự án lớn của doanh nghiệp.