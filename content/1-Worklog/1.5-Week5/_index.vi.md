---
title: "Worklog Tuần 5"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

### Mục tiêu tuần 5:

* Nghiên cứu lý thuyết nền tảng về dịch vụ mạng ảo Amazon Virtual Private Cloud (Amazon VPC).
* Tìm hiểu các thành phần cấu thành kiến trúc mạng trên AWS bao gồm: Subnet (Public và Private), Route Table, Internet Gateway (IGW) và NAT Gateway.
* Nghiên cứu cơ chế bảo mật mạng đa lớp thông qua Network Access Control Lists (NACLs) và Security Groups.
* Thực hành thiết kế và khởi tạo một hệ thống mạng VPC tùy chỉnh, phân chia các dải mạng hợp lý cho ứng dụng Web và Cơ sở dữ liệu trên giao diện console.
* Hoàn thành các nhiệm vụ bổ sung thực tế để tích lũy AWS Credit phục vụ thử nghiệm hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Nghiên cứu lý thuyết cốt lõi về dịch vụ mạng ảo độc lập Amazon VPC <br> - Theo dõi chuỗi bài giảng trực quan về chủ đề Networking & VPC | 01/06/2026   | 01/06/2026      | Youtube AWS Study Group |
| 3   | - Tìm hiểu cơ chế hoạt động của Subnet, Route Table, Internet Gateway và NAT Gateway <br> - Đọc hướng dẫn cấu hình mạng và phân bổ sơ đồ địa chỉ IP (CIDR Block) | 02/06/2026   | 02/06/2026      | Platform Bootcamp |
| 4   | - **Thực hành:** <br>&emsp; + Thiết lập hệ thống mạng VPC tùy chỉnh <br>&emsp; + Phân chia vùng mạng Public và Private riêng biệt từ con số 0 | 03/06/2026   | 03/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **Thực hành:** <br>&emsp; + Cấu hình các quy tắc bảo mật mạng đa lớp bằng cách kết hợp Network ACLs và Security Groups | 04/06/2026   | 04/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Thực hành nâng cao (Kiếm AWS Credit):** <br>&emsp; + Task 1: Launch EC2 Instance (Tích lũy $20 credit) <br>&emsp; + Task 2: Amazon Bedrock Playground (Tích lũy $20 credit) | 05/06/2026   | 05/06/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 5:

* Nắm vững khái niệm về Amazon VPC, hiểu rõ cách thiết lập một phân vùng mạng độc lập và an toàn trên hạ tầng đám mây toàn cầu của AWS.

* Phân biệt được sự khác nhau giữa Public Subnet (chứa Web Server, kết nối trực tiếp Internet qua Internet Gateway) và Private Subnet (cô lập hoàn toàn, dùng chứa Database hoặc logic Backend nhạy cảm).

* Hiểu rõ cơ chế bảo mật mạng hai lớp: NACLs (tường lửa cấp độ Subnet - Stateless) và Security Groups (tường lửa cấp độ Instance - Stateful) để kiểm soát lưu lượng dữ liệu tối đa.

* Khởi tạo thành công mạng Amazon VPC tùy chỉnh với dải địa chỉ IP theo chuẩn CIDR block, phân chia ổn định các Public/Private Subnet trên nhiều vùng sẵn sàng (Availability Zones) khác nhau.

* Cấu hình chính xác Internet Gateway và NAT Gateway trong Public Subnet, cho phép các máy chủ chạy Backend thuộc vùng Private Subnet có thể kết nối tải bản cập nhật ra ngoài một chiều an toàn.

* Hoàn thành xuất sắc 2 bài thực hành bổ sung bao gồm khởi chạy máy chủ ảo (Task 1: Launch EC2 Instance) và làm quen môi trường thử nghiệm AI (Task 2: Amazon Bedrock Playground), tích lũy thành công tổng cộng $40 AWS Credit.

* Có được tư duy thiết kế hệ thống toàn diện của một Kỹ sư Backend: xây dựng ứng dụng an toàn bằng cách đặt giao diện công khai ở Public Subnet để đón người dùng, đồng thời giấu kín toàn bộ mã nguồn Backend và Cơ sở dữ liệu trong Private Subnet.

* Nâng cao kỹ năng đọc hiểu sơ đồ kiến trúc mạng (Architecture Diagram) và chuyển đổi hóa sơ đồ thiết kế thành hệ thống tài nguyên chạy thực tế trên Cloud.