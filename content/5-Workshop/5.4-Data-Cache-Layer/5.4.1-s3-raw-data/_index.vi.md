---
title: "Lưu trữ File thô (Amazon S3)"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.4.1. </b> "
---

### 1. Khởi tạo S3 Bucket cho hóa đơn
Chúng ta tạo một bucket có tên `finvantage-raw-invoices-[random-id]` để làm nơi "đáp" cho các file hóa đơn từ `Import Lambda`.
*   **Bảo mật:** Bật tính năng **Block all public access**. Không ai từ Internet có thể truy cập trực tiếp vào các file này nếu không có IAM Role hợp lệ.
*   **Mã hóa:** Bật mã hóa phía máy chủ (Server-Side Encryption) với chuẩn SSE-S3 để bảo vệ dữ liệu nhạy cảm ở trạng thái nghỉ (Data at rest).

### 2. Cấu hình Event Notifications (Kích hoạt sự kiện)
Kiến trúc Serverless hoạt động dựa trên sự kiện (Event-driven). Khi một file hóa đơn mới được upload lên S3 thành công, S3 sẽ tự động phát ra một sự kiện (Event) để đánh thức hàm `Parse & Categorize Lambda` hoặc `Textract` vào làm việc.
*   Vào tab **Properties** của S3 Bucket.
*   Tạo Event notification: Bắt sự kiện `s3:ObjectCreated:Put`.
*   Đích đến (Destination): Chọn hàm Lambda chịu trách nhiệm xử lý OCR.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình phần thiết lập **Event notifications** trong S3, cho thấy S3 Bucket đang trỏ luồng sự kiện tới một hàm Lambda.
> *Mã Markdown:* `![S3 Event Notification](../../../images/s3-event-notification.png)`