---
title: "Worklog Tuần 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

* Hiện thực hóa mã nguồn Backend cho dự án FinVantage theo mô hình kiến trúc không máy chủ (Serverless Architecture).
* Cấu hình kết nối tập trung từ mã nguồn tới hệ sinh thái AWS (S3, Textract) và phân hệ cơ sở dữ liệu (Database) thông qua bộ thư viện AWS SDK.
* Lập trình hoàn thiện luồng API xử lý dữ liệu: Tiếp nhận file, lưu trữ trên S3, trích xuất dữ liệu qua Textract và lưu trữ kết quả vào Database.
* Sử dụng công cụ Git để quản lý phiên bản mã nguồn, thực hiện đóng gói và đẩy (push) commit hoàn chỉnh lên kho chứa trực tuyến GitHub.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Bắt tay vào giai đoạn hiện thực hóa mã nguồn cho phân hệ Backend của dự án FinVantage. <br> - Triển khai cấu trúc thư mục theo mô hình không máy chủ (Serverless). | 06/07/2026   | 06/07/2026      | Nhóm dự án |
| 3   | - Viết các module cấu hình kết nối an toàn từ mã nguồn tới các dịch vụ cốt lõi thông qua bộ thư viện AWS SDK. | 07/07/2026   | 07/07/2026      | AWS Documentation |
| 4   | - **Thực hành:** Lập trình API tiếp nhận tệp tin từ Client, tự động đẩy dữ liệu hóa đơn lên Amazon S3 Bucket bảo mật. | 08/07/2026   | 08/07/2026      | VS Code / Local Environment |
| 5   | - **Thực hành:** Lập trình luồng xử lý gọi API Amazon Textract để đọc, trích xuất thông tin hóa đơn và chuẩn hóa dữ liệu dạng JSON. <br> - Viết hàm kết nối với Database để lưu trữ vĩnh viễn kết quả đã trích xuất. | 09/07/2026   | 09/07/2026      | VS Code / Local Environment |
| 6   | - Sử dụng Git để kiểm soát phiên bản và đẩy (push) toàn bộ mã nguồn phân hệ lên kho chứa GitHub với commit "Hoàn thiện Backend Serverless: API, S3, Textract, Database". | 10/07/2026   | 10/07/2026      | GitHub |


### Kết quả đạt được tuần 10:

* Củng cố sâu sắc kiến trúc Backend Serverless, hiểu rõ cách tổ chức mã nguồn để tối ưu hóa hiệu năng khi chạy trên môi trường đám mây thay vì các máy chủ truyền thống.

* Nắm vững luồng dữ liệu (Data Flow) của một hệ thống xử lý tài liệu tự động: Từ lúc nhận tệp tin, lưu trữ, trích xuất dữ liệu bằng AI cho đến khi lưu trữ kết quả cuối cùng vào cơ sở dữ liệu.

* Hoàn thiện và đẩy (push) thành công toàn bộ mã nguồn phân hệ lên GitHub, thực hiện commit chính thức với nội dung "Hoàn thiện Backend Serverless: API, S3, Textract, Database".

* Hiện thực hóa thành công API tiếp nhận tệp tin từ Client, tự động đẩy (upload) dữ liệu hóa đơn lên Amazon S3 Bucket bảo mật.

* Lập trình luồng xử lý gọi API Amazon Textract để tự động đọc và trích xuất thông tin từ hóa đơn, sau đó chuẩn hóa dữ liệu dạng JSON.

* Viết thành công các hàm kết nối và tương tác với Database để lưu trữ vĩnh viễn các kết quả đã được trích xuất, sẵn sàng cung cấp dữ liệu cho phân hệ Generative AI (Amazon Bedrock).

* Tích lũy kinh nghiệm thực tế quý báu trong việc hiện thực hóa các sơ đồ kiến trúc hạ tầng thành những dòng mã nguồn chạy được trong thực tế.

* Nâng cao kỹ năng làm việc nhóm qua Git/GitHub, biết cách chia nhỏ công việc và tạo các commit rõ ràng, chuyên nghiệp đúng chuẩn môi trường doanh nghiệp.