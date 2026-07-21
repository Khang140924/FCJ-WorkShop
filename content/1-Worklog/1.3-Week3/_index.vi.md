---
title: "Worklog Tuần 3"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Mục tiêu tuần 3:

* Nghiên cứu lý thuyết tổng quan về dịch vụ điện toán đám mây Amazon Elastic Compute Cloud (Amazon EC2).
* Tìm hiểu về các loại Instance Type, các mô hình thanh toán chi phí máy chủ và cơ chế bảo mật mạng qua Security Group.
* Tìm hiểu giải pháp tự động mở rộng và cân bằng tải hệ thống: Auto Scaling Group và Elastic Load Balancing (ELB).
* Thực hành khởi tạo, cấu hình và quản lý vòng đời của máy chủ ảo EC2 trên giao diện console.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | - Nghiên cứu lý thuyết tổng quan về dịch vụ máy chủ ảo Amazon EC2. <br> - Xem chuỗi bài giảng trực quan về Compute Services. | 18/05/2026 | 18/05/2026 | Youtube AWS Study Group |
| 3 | - Tìm hiểu cơ chế hoạt động của Security Group, Elastic Load Balancing và Auto Scaling Group. <br> - Đọc tài liệu hướng dẫn cấu hình máy chủ và phân loại AMI. | 19/05/2026 | 19/05/2026 | Platform Bootcamp |
| 4 | - Thực hành khởi tạo, cấu hình Key Pair và kết nối SSH quản trị máy chủ Amazon EC2. | 20/05/2026 | 20/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Cài đặt và cấu hình thử nghiệm Web Server trên nền tảng Linux thông qua tính năng User Data. | 21/05/2026 | 21/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 3:

* Nắm vững khái niệm về Amazon EC2, hiểu rõ cách lựa chọn Instance Type (về CPU, RAM, Network) sao cho tối ưu và phù hợp nhất với từng loại kiến trúc ứng dụng phần mềm.

* Phân biệt được cơ chế hoạt động của Security Group (tường lửa ảo cấp độ Instance - Stateful) để kiểm soát lưu lượng mạng ra/vào máy chủ một cách an toàn.

* Hiểu được nguyên lý vận hành của Elastic Load Balancing (điều phối lưu lượng truy cập) và Auto Scaling Group (tự động tăng/giảm số lượng máy chủ dựa trên hiệu năng thực tế) nhằm đảm bảo tính sẵn sàng cao (High Availability) cho hệ thống.

* Thực hiện cấu hình và khởi chạy thành công một máy chủ Amazon EC2 Instance sử dụng hệ điều hành Amazon Linux 2.

* Cấu hình chính xác Key Pair và sử dụng các công cụ kết nối từ xa (như SSH Terminal/PuTTY) để truy cập trực tiếp vào quản trị máy chủ ảo từ máy tính cá nhân.

* Thiết lập thành công Security Group Rule, mở các cổng mạng cơ bản (Port 22 cho SSH, Port 80/443 cho HTTP/HTTPS) để cho phép máy chủ giao tiếp với môi trường Internet.

* Thực hành cài đặt thử nghiệm một Web Server cơ bản (Apache/Nginx) trên EC2 bằng cách sử dụng tính năng User Data (chạy script tự động khi khởi tạo máy chủ).

* Hiểu rõ cách thức một ứng dụng Backend (Java, PHP, Go) được triển khai và vận hành thực tế trên môi trường máy chủ đám mây thay vì môi trường Localhost thông thường.

* Rèn luyện kỹ năng quản trị hệ điều hành Linux qua giao diện dòng lệnh (CLI) – một kỹ năng bắt buộc và cực kỳ quan trọng đối với một Kỹ sư Backend / Cloud Engineer chuyên nghiệp.


