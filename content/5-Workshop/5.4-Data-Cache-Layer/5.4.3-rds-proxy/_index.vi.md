---
title: "Cấu hình Amazon RDS Proxy"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### Giải bài toán Connection Pool của Serverless

Các hàm AWS Lambda có thể scale up lên hàng ngàn instance trong vài giây. Nếu mỗi hàm Lambda tự mở một kết nối (connection) trực tiếp đến MySQL, Database sẽ lập tức cạn kiệt Connection Pool và bị treo (Crash).

Để giải quyết, FinVantage sử dụng **Amazon RDS Proxy**.
*   **Chức năng:** RDS Proxy đứng giữa Lambda và RDS. Nó giữ một lượng nhỏ các kết nối cố định tới Database và chia sẻ (multiplex) các kết nối này cho hàng ngàn hàm Lambda đang chạy.
*   **Cấu hình:** 
    *   Khởi tạo RDS Proxy và trỏ Target về con MySQL vừa tạo.
    *   Lưu thông tin đăng nhập (Username/Password) của RDS vào **AWS Secrets Manager**. RDS Proxy sẽ tự động lấy thông tin từ Secrets Manager để đăng nhập, giúp chúng ta không phải hard-code mật khẩu vào mã nguồn Lambda.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện cấu hình của RDS Proxy, hiển thị phần Target database và Secrets Manager đang được liên kết.
> *Mã Markdown:* `![Amazon RDS Proxy](../../../images/rds-proxy-config.png)`