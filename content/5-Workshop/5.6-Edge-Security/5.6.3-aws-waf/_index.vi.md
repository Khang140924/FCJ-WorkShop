---
title: "Tường lửa Ứng dụng Web (WAF)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.6.3. </b> "
---

### Ngăn chặn các luồng truy cập độc hại

**AWS WAF (Web Application Firewall)** là tấm khiên thép được đính trực tiếp vào CloudFront (hoặc API Gateway). Nó liên tục quét các request (HTTP/HTTPS) đang cố đi vào hệ thống để phát hiện các dấu hiệu bất thường.

#### Thiết lập các bộ quy tắc bảo vệ (Web ACL Rules)
Chúng ta cấu hình một Web ACL (Access Control List) và áp dụng các bộ quy tắc (Rules) sau để bảo vệ hệ thống FinVantage:
1.  **Rate-based Rule (Chống DDoS/Spam):** Giới hạn số lượng request từ một IP (ví dụ: tối đa 500 requests / 5 phút). Nếu vượt quá, IP đó sẽ bị block tạm thời, giúp bảo vệ API và Database không bị quá tải.
2.  **AWS Managed Rules (Core Rule Set):** Kích hoạt bộ quy tắc có sẵn của AWS để chặn đứng các lỗ hổng bảo mật phổ biến nhất của tổ chức OWASP (như SQL Injection, Cross-Site Scripting - XSS, rà quét cổng trái phép).

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình biểu đồ Traffic của AWS WAF (Tab Overview), hoặc danh sách các Rules (Rules tab) đã được kích hoạt trong Web ACL.
> *Mã Markdown:* `![Cấu hình tường lửa AWS WAF](../../../images/aws-waf-rules.png)`