---
title: "Amazon SNS Alerts"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.7.3. </b> "
---

### Amazon SNS Alerts (Thành phần đề xuất)

> ⚠️ **LƯU Ý QUAN TRỌNG:**  
> **Thành phần mở rộng/đề xuất, chưa xác nhận đã được triển khai trong hệ thống production hiện tại.**  
> Để giảm thiểu độ phức tạp khi cấu hình Email SMTP/SNS và tránh việc bắn spam thông báo thử nghiệm trong giai đoạn phát triển lab, hệ thống cảnh báo tự động qua Amazon SNS và CloudWatch Alarms hiện tại chưa được cấu hình. Phần dưới đây mô tả giải pháp thiết kế lý thuyết để triển khai hệ thống thông tin cảnh báo tự động trên môi trường vận hành thực tế.

---

### Mục tiêu
Trang này sẽ giới thiệu giải pháp lý thuyết về việc cấu hình **Amazon SNS (Simple Notification Service)** và **CloudWatch Alarms** (các cảnh báo vượt ngưỡng chỉ số) để tự động gửi thông báo khẩn cấp đến DevOps (đội ngũ phát triển và vận hành hệ thống) khi FinVantage gặp sự cố.

### Giới thiệu ngắn
Thay vì bắt quản trị viên phải túc trực và làm mới bảng điều khiển CloudWatch 24/7, chúng ta thiết lập cơ chế giám sát chủ động. Khi phát hiện các chỉ số sức khỏe của ứng dụng vượt ngưỡng an toàn, CloudWatch sẽ tự động gửi tín hiệu kích hoạt Amazon SNS để chuyển tiếp tin nhắn cảnh báo về hòm thư Email hoặc các kênh chat Slack/Telegram của bạn.

---

### Các bước thiết lập lý thuyết hệ thống cảnh báo

#### 1. Khởi tạo Amazon SNS Topic

*   **Tạo SNS Topic (chủ đề thông báo):** Khởi tạo một chủ đề thông báo dạng Standard với tên `FinVantage-System-Alerts`.
*   **Thiết lập Subscription (đăng ký nhận thông báo):** 
    *   Tạo một Subscription mới liên kết với Topic.
    *   *Protocol (Giao thức):* Chọn `Email`.
    *   *Endpoint:* Điền địa chỉ email của quản trị viên (ví dụ: `admin@finvantage.com`).
    *   *Xác thực:* Hệ thống AWS sẽ gửi một email confirm. Người dùng bắt buộc phải click vào liên kết **Confirm Subscription** trong hòm thư thì trạng thái đăng ký mới chuyển sang Active.

---

![Hình 5.7.3a. Cấu hình Amazon SNS Topic finvantage-alert-topic và Email Subscription đang ở trạng thái chờ xác nhận.](../../../images/finvantage-sns-subscription-email.jpg)

---

#### 2. Thiết lập bộ CloudWatch Alarms kích hoạt SNS

Chúng ta cấu hình hai bộ cảnh báo quan trọng nhất để giám sát hệ thống:

*   **Cảnh báo lỗi vận hành (Technical Alarm):**
    *   *Metric:* `AWS/Lambda` > `Errors` của các hàm core (như `analyzeInvoice` hoặc `ocrInvoice`).
    *   *Ngưỡng kích hoạt:* Nếu tổng số lỗi thực thi lớn hơn `5` lần trong vòng `5 phút`.
    *   *Hành động:* Khi trạng thái chuyển sang **In Alarm** (Màu đỏ), tự động bắn message (tin nhắn) thông báo lỗi chi tiết vào SNS Topic để gửi email cảnh báo DevOps.
*   **Cảnh báo vượt ngân sách (Billing Alarm):**
    *   *Metric:* `AWS/Billing` > `EstimatedCharges` (Chi phí dự kiến phát sinh).
    *   *Ngưỡng kích hoạt:* Chi phí ước tính vượt quá `$10` USD.
    *   *Mục đích:* Phòng tránh việc code bị lặp vô hạn (Infinite Loop), API bị tấn công spam cuộc gọi dẫn đến hóa đơn AWS tăng đột biến ngoài tầm kiểm soát.

---

![Hình 5.7.3b. Danh sách bộ cảnh báo finvantage-lambda-errors khởi tạo thành công trên Amazon CloudWatch Alarms.](../../../images/finvantage-cloudwatch-alarms.jpg)

---

### Các lỗi thường gặp và cách xử lý
*   **Lỗi: `Alarm ở trạng thái INSUFFICIENT_DATA`**
    *   *Nguyên nhân:* Do hệ thống chưa thu thập đủ số liệu (metrics) trong chu kỳ cấu hình (ví dụ: chưa có lượt gọi Lambda nào phát sinh lỗi). Đây là trạng thái bình thường khi hệ thống mới hoạt động và chưa có dữ liệu đầu vào.
    *   *Cách xử lý:* Chờ đợi hệ thống ghi nhận lưu lượng traffic thực tế, hoặc kiểm tra lại cấu hình chu kỳ đo lường của Alarm.

### Kết luận ngắn
Giải pháp tích hợp CloudWatch Alarms và Amazon SNS Alerts giúp tăng cường khả năng phản ứng nhanh với sự cố, bảo đảm tính sẵn sàng cao cho toàn bộ hạ tầng FinVantage.
