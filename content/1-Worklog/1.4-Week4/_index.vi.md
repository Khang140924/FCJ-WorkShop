---
title: "Worklog Tuần 4"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

### Mục tiêu tuần 4:

* Nghiên cứu lý thuyết về các loại hình lưu trữ cốt lõi trên điện toán đám mây: Block Storage, Object Storage và File Storage.
* Tìm hiểu chi tiết về dịch vụ lưu trữ đối tượng Amazon Simple Storage Service (Amazon S3) và các tính năng nâng cao đi kèm.
* Tìm hiểu giải pháp lưu trữ khối và chia sẻ dữ liệu cho hệ thống máy chủ máy chủ ảo: Amazon Elastic Block Store (Amazon EBS) và Amazon Elastic File System (Amazon EFS).
* Thực hành khởi tạo S3 Bucket, cấu hình phân quyền truy cập an toàn và quản lý vòng đời của dữ liệu trên giao diện console.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| :--- | :--- | :--- | :--- | :--- |
| 2 | - Nghiên cứu lý thuyết về các loại hình lưu trữ trên AWS: Amazon S3, EBS và EFS. <br> - Xem chuỗi bài giảng trực quan về Storage Services. | 25/05/2026 | 25/05/2026 | Youtube AWS Study Group |
| 3 | - Phân biệt bản chất và trường hợp sử dụng của các mô hình: Block Storage, Object Storage và File Storage. <br> - Đọc tài liệu hướng dẫn quản lý dữ liệu và phân biệt các loại ổ đĩa lưu trữ. | 26/05/2026 | 26/05/2026 | Platform Bootcamp |
| 4 | - Thực hành khởi tạo Amazon S3 Bucket, cấu hình chi tiết phân quyền dữ liệu (Public/Private) và tính năng quản lý phiên bản (S3 Versioning). | 27/05/2026 | 27/05/2026 | https://cloudjourney.awsstudygroup.com/ |
| 5 | - Triển khai ứng dụng và cấu hình tính năng Static Website Hosting trực tiếp trên nền tảng Amazon S3. | 28/05/2026 | 28/05/2026 | https://cloudjourney.awsstudygroup.com/ |

### Kết quả đạt được tuần 4:

* Nắm vững khái niệm về Object Storage (Amazon S3), hiểu rõ lý do S3 là giải pháp tối ưu để lưu trữ dữ liệu tĩnh (hình ảnh, video, tài liệu) cho các ứng dụng Web/App nhờ độ bền vững vượt trội lên tới 99.999999999% (11 số 9).
* Phân biệt rõ ràng sự khác nhau giữa Amazon EBS (ổ đĩa hiệu năng cao gắn cố định vào một máy chủ EC2) và Amazon EFS (hệ thống tệp tin dùng chung cho phép nhiều máy chủ đồng thời kết nối và chia sẻ dữ liệu).
* Hiểu rõ cơ chế bảo mật trên lưu trữ S3 thông qua việc cấu hình Bucket Policy, Access Control Lists (ACLs) và tính năng Versioning để tránh các rủi ro bị ghi đè hoặc xóa nhầm dữ liệu.
* Khởi tạo thành công Amazon S3 Bucket, thực hiện thành thục các thao tác upload/download đối tượng dữ liệu trực tiếp thông qua giao diện AWS Management Console.
* Cấu hình chính xác tính năng Static Website Hosting trên Amazon S3, triển khai thành công một trang web tĩnh hoạt động trực tiếp trên môi trường Internet mà không cần tốn chi phí thuê và duy trì máy chủ EC2.
* Thực hành viết và cấu hình thành công các tệp tin S3 Bucket Policy dưới dạng mã JSON để kiểm soát phân quyền truy cập từ bên ngoài một cách chặt chẽ.
* Hiểu rõ cách thức thiết kế tầng lưu trữ (Storage Layer) tối ưu cho một ứng dụng Backend: Thay vì lưu các file media trực tiếp trên ổ cứng cục bộ của máy chủ (gây đầy ổ đĩa), lập trình viên sẽ gọi API để đẩy dữ liệu trực tiếp sang Amazon S3.
* Hình thành tư duy tối ưu hóa chi phí (Cost Optimization) thông qua việc phân loại dữ liệu để áp dụng các Storage Classes phù hợp (Standard cho dữ liệu truy cập thường xuyên và Glacier cho dữ liệu lưu trữ dài hạn).


