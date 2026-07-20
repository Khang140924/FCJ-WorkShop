---
title: "Worklog Tuần 11"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

* Triển khai (Deploy) toàn bộ mã nguồn Backend Serverless của dự án FinVantage lên hạ tầng AWS (Lambda, API Gateway).
* Cấu hình các biến môi trường và thiết lập quyền bảo mật IAM Role cho các dịch vụ giao tiếp chéo.
* Phối hợp nhóm thực hiện kiểm thử toàn trình (End-to-End Testing) và sử dụng CloudWatch để theo dõi, gỡ lỗi hệ thống.
* Hợp nhất mã nguồn trên kho chứa GitHub, hoàn thiện tài liệu và chính thức nghiệm thu dự án nhóm.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - **Triển khai hạ tầng:** Sử dụng giao diện AWS Management Console để đưa mã nguồn Node.js lên AWS Lambda và cấu hình điểm cuối kết nối trên Amazon API Gateway. | 13/07/2026   | 13/07/2026      | Nhóm dự án |
| 3   | - **Cấu hình bảo mật:** Thiết lập các chính sách (Policies) trong IAM để cấp quyền tối thiểu (Least Privilege), cho phép Lambda tương tác an toàn với các dịch vụ khác. | 14/07/2026   | 14/07/2026      | AWS Documentation |
| 4   | - **Kiểm thử toàn trình:** Đóng vai trò người dùng cuối để tải tệp tin thực tế lên hệ thống và kiểm tra luồng phản hồi. | 15/07/2026   | 15/07/2026      | Hệ thống FinVantage |
| 5   | - **Giám sát và gỡ lỗi:** Theo dõi toàn bộ luồng xử lý từ lúc đẩy file lên đến khi xuất ra kết quả thông qua Amazon CloudWatch để phát hiện và xử lý lỗi kịp thời. | 16/07/2026   | 16/07/2026      | Amazon CloudWatch |
| 6   | - **Quản lý dự án:** Rà soát mã nguồn (Code Review) lần cuối cùng các thành viên, xử lý xung đột code (nếu có) và đóng gói phiên bản phát hành chính thức trên GitHub. | 17/07/2026   | 17/07/2026      | GitHub |


### Kết quả đạt được tuần 11:

* Nắm vững quy trình đưa một ứng dụng phần mềm từ giai đoạn phát triển (Development) sang giai đoạn vận hành thực tế (Production) trên môi trường điện toán đám mây.

* Hiểu sâu sắc tầm quan trọng của nguyên tắc cấp quyền tối thiểu (Least Privilege) khi thiết lập IAM Role, đảm bảo kiến trúc Backend Serverless vận hành bảo mật và khép kín.

* Triển khai thành công toàn bộ kiến trúc Backend của dự án FinVantage lên môi trường AWS thực tế, thiết lập thành công API Gateway để điều hướng yêu cầu đến các hàm xử lý Lambda.

* Phát hiện và xử lý thành công các lỗi phát sinh trên môi trường Cloud (như lỗi quyền truy cập, lỗi bất đồng bộ dữ liệu) thông qua công cụ giám sát Amazon CloudWatch.

* Hoàn thành xuất sắc nhiệm vụ của Thành viên 4, đẩy (push) và hợp nhất (merge) thành công toàn bộ mã nguồn lên kho chứa GitHub, đóng gói tài liệu nghiệm thu dự án nhóm đúng hạn.

* Trải nghiệm thực tế toàn bộ vòng đời phát triển của một sản phẩm công nghệ hoàn chỉnh: từ lúc lên ý tưởng, chuẩn hóa sơ đồ kiến trúc, lập trình Backend cho đến khi vận hành thực tế trên đám mây.

* Nâng cao tư duy làm việc nhóm và giải quyết vấn đề, thấy rõ được hiệu quả to lớn của việc phối hợp chuyên nghiệp và quản lý dự án bài bản.