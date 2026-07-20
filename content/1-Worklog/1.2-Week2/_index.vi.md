---
title: "Worklog Tuần 2"
date: 2026-05-11
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
---

### Mục tiêu tuần 2:

* Nghiên cứu về mô hình trách nhiệm chung (Shared Responsibility Model) của AWS.
* Tìm hiểu lý thuyết và cấu trúc của dịch vụ AWS Identity and Access Management (IAM).
* Triển khai các biện pháp bảo mật tài khoản cơ bản, bao gồm Xác thực đa yếu tố (MFA) và Chính sách mật khẩu (Password Policy).
* Thiết lập AWS Budgets để quản lý, giám sát và cảnh báo chi phí tài nguyên trong quá trình thực hành.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | - Nghiên cứu mô hình trách nhiệm chung (Shared Responsibility Model) của AWS. <br> - Xem video bài giảng về Security và IAM. | 11/05/2026 | 11/05/2026 | Youtube AWS Study Group |
| 3 | - Tìm hiểu lý thuyết dịch vụ AWS Identity and Access Management (IAM). <br> - Đọc tài liệu "Security Best Practices" để hiểu cấu trúc tệp tin Policy dạng JSON. | 12/05/2026 | 12/05/2026 | Platform Bootcamp |
| 4 | - Cấu hình các biện pháp bảo mật tài khoản cơ bản: <br> &emsp; + Bật Xác thực đa yếu tố (MFA). <br> &emsp; + Thiết lập Password Policy. | 13/05/2026 | 13/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Thiết lập AWS Budgets để quản lý, giám sát và cảnh báo chi phí tài nguyên khi thực hành. | 14/05/2026 | 14/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 2:

* Phân định rõ ràng ranh giới bảo mật giữa AWS (Bảo mật của đám mây) và người dùng (Bảo mật trong đám mây) dựa trên Mô hình trách nhiệm chung.

* Hiểu sâu về cơ chế vận hành của các thành phần cốt lõi trong IAM:
    * IAM User
    * IAM Group
    * Policy (phân quyền bằng JSON)
    * IAM Role

* Nắm vững nguyên tắc cấp quyền tối thiểu (Principle of Least Privilege) trong quản trị và vận hành hệ thống.

* Kích hoạt và cấu hình thành công tính năng xác thực hai lớp (MFA) cho tài khoản Root để ngăn chặn các nguy cơ chiếm quyền.

* Tạo lập thành công các IAM User và IAM Group riêng biệt.

* Viết và gắn các IAM Policy nhằm phân chia quyền hạn chuẩn xác thay vì lạm dụng tài khoản Root.

* Khởi tạo thành công AWS Budgets, cấu hình ngưỡng cảnh báo chi phí qua email cá nhân để chủ động kiểm soát ngân sách và tránh phí phát sinh.

* Hình thành tư duy "Security First" để xây dựng kiến trúc hệ thống an toàn ngay từ đầu.

* Biết cách ứng dụng tư duy phân quyền cho ứng dụng Backend thông qua IAM Role thay vì nhúng trực tiếp Access Key vào mã nguồn một cách thủ công, giúp nâng cao tính bảo mật tuyệt đối cho dự án phần mềm.


