---
title: "Cảnh báo tự động (Amazon SNS)"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### Thiết lập Cảnh báo với Amazon SNS

Thay vì phải ngồi canh màn hình CloudWatch 24/7, chúng ta sử dụng **Amazon SNS (Simple Notification Service)** kết hợp với CloudWatch Alarms để hệ thống tự động "kêu cứu" khi có sự cố.

#### 1. Tạo Topic Cảnh báo
*   Khởi tạo một SNS Topic mang tên `FinVantage-System-Alerts`.
*   Tạo **Subscription**: Đăng ký email cá nhân (hoặc webhook Telegram/Slack) vào Topic này để nhận thông báo.

#### 2. Gắn CloudWatch Alarms
Chúng ta thiết lập 2 bộ cảnh báo kinh điển:
1.  **Cảnh báo Kỹ thuật:** Đặt Alarm nếu hàm `Worker Lambda` xử lý AI báo lỗi (Errors) lớn hơn 5 lần trong 5 phút. Nếu kích hoạt, Alarm sẽ bắn message vào SNS Topic để gửi email cho đội ngũ DevOps.
2.  **Cảnh báo Chi phí (Billing Alarm):** Đặc thù Serverless là tính tiền theo lưu lượng. Để tránh hóa đơn AWS cuối tháng tăng đột biến do bị tấn công hoặc code lỗi (infinite loop), chúng ta đặt cảnh báo ngay khi ngân sách ước tính vượt quá `$10`.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình một Email cảnh báo từ AWS báo về hòm thư của bạn, HOẶC giao diện CloudWatch hiển thị trạng thái Alarm màu đỏ (In alarm).
> *Mã Markdown:* `![Cảnh báo qua SNS và Email](../../../images/sns-email-alert.png)`