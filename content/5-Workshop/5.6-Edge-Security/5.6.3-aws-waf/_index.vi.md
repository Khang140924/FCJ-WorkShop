---
title: "AWS WAF (Tường lửa ứng dụng)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### AWS WAF (Thành phần đề xuất bảo vệ)

> ⚠️ **LƯU Ý QUAN TRỌNG:**  
> **Thành phần mở rộng/đề xuất, chưa xác nhận đã được triển khai trong hệ thống production hiện tại.**  
> AWS WAF là dịch vụ có mức phí duy trì cố định tối thiểu khá cao trên AWS (khoảng $5.00/tháng cho mỗi Web ACL và $1.00/tháng cho mỗi rule được tạo, chưa tính phí theo lượng request). Do đó, đối với môi trường thử nghiệm học tập và chạy lab, chúng ta tạm thời bỏ qua bước khởi tạo thực tế dịch vụ này để tối ưu hóa chi phí. Phần dưới đây mô tả giải pháp thiết kế lý thuyết để bảo mật hệ thống khi đưa vào vận hành thương mại.

---

### Mục tiêu
Trang này sẽ giới thiệu giải pháp lý thuyết về việc tích hợp **AWS WAF (Web Application Firewall)** để bảo vệ cổng API Gateway và CloudFront, giúp ngăn chặn các đợt tấn công mạng phổ biến và bảo đảm an toàn dữ liệu cho hệ thống **FinVantage**.

### Giới thiệu ngắn
AWS WAF là tường lửa bảo vệ ứng dụng web được triển khai ở lớp biên mạng. Khi tích hợp trực tiếp WAF vào Amazon API Gateway hoặc CloudFront Distribution, dịch vụ này sẽ phân tích chi tiết từng request HTTP/HTTPS đi vào để phát hiện và chặn đứng các luồng truy cập độc hại trước khi chúng chạm tới các hàm Lambda backend.

### Thiết lập các bộ quy tắc bảo vệ đề xuất (Web ACL Rules)

Nếu triển khai thương mại, hệ thống FinVantage sẽ cấu hình một **Web ACL (Web Access Control List)** chứa các bộ quy tắc sau:

1.  **Rate-based Rule (quy tắc giới hạn tần suất truy cập):** 
    *   *Chức năng:* Giới hạn số lượng request tối đa được gửi từ một địa chỉ IP duy nhất trong vòng 5 phút (ví dụ: tối đa 300 requests/5 phút).
    *   *Mục đích:* Ngăn chặn các cuộc tấn công brute-force mò mật khẩu, DDoS protection (chống tấn công từ chối dịch vụ phân tán) hoặc các script tự động spam gửi request phá hoại tài nguyên hệ thống.
2.  **AWS Managed Rules (các bộ quy tắc được AWS quản lý và cập nhật sẵn):**
    *   *Chức năng:* Kích hoạt các gói quy tắc bảo mật chuẩn hóa do các chuyên gia AWS cập nhật liên tục (như Core Rule Set, SQL database protection, v.v.).
    *   *Mục đích:* Chặn đứng hoàn toàn các lỗ hổng bảo mật Web phổ biến theo tiêu chuẩn OWASP Top 10 như: SQL Injection (chèn mã lệnh SQL độc hại vào ô tìm kiếm), Cross-Site Scripting (XSS - chèn script độc hại chạy dưới trình duyệt của client), và các hoạt động quét cổng dò tìm lỗ hổng của hacker.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: Sơ đồ hoặc hình vẽ minh họa luồng hoạt động bảo vệ của AWS WAF đứng chặn trước CloudFront và API Gateway để bảo vệ backend Lambda.  
> Tên ảnh đề xuất: `finvantage-waf-architecture.png`  
> Chú thích: “Hình 5.6.3. Sơ đồ lý thuyết kiến trúc bảo vệ biên tích hợp AWS WAF bảo vệ ứng dụng FinVantage.”

---

### Các lỗi thường gặp và cách xử lý khi chạy WAF
*   **Lỗi: `Người dùng thật bị chặn nhầm (HTTP 403 Forbidden)`**
    *   *Nguyên nhân:* Do cấu hình bộ lọc của WAF quá nhạy (False Positive) hoặc do người dùng thực hiện tải nhiều ảnh hóa đơn liên tục kích hoạt bộ giới hạn Rate-based Rule.
    *   *Cách xử lý:* Đưa các IP đáng tin cậy vào Safe Whitelist (Danh sách trắng an toàn), hoặc điều chỉnh nâng mức giới hạn số lượng request tối đa của Rate-based Rule cho phù hợp với hành vi sử dụng thực tế.

### Kết luận ngắn
AWS WAF là chốt chặn bảo mật vững chắc ở tầng biên, đóng vai trò bảo vệ quan trọng cho FinVantage khi ứng dụng tiến hành mở rộng thương mại quy mô lớn.

---

### Danh sách hình ảnh cần chụp cho báo cáo
1.  `finvantage-waf-architecture.png` - Sơ đồ kiến trúc luồng bảo vệ của AWS WAF (Hình minh họa).