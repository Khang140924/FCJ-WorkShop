---
title: "Bộ nhớ đệm (ElastiCache Redis)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.4.4. </b> "
---

### Tăng tốc truy xuất với ElastiCache

Trong các hệ thống quản lý chi tiêu, việc người dùng liên tục làm mới (refresh) trang để xem tổng chi tiêu trong tháng sẽ tạo ra vô số câu truy vấn (Query) đắt đỏ lên RDS.

Chúng ta sử dụng **Amazon ElastiCache (Redis)** làm lớp bộ nhớ đệm (In-memory Cache) để giảm tải cho RDS và giảm độ trễ (latency).
*   **Khởi tạo Cluster:** Tạo một Redis cluster nằm gọn trong các Private Subnets của dự án. Gắn `Database-SG` để kiểm soát quyền truy cập.
*   **Chiến lược Cache (Luồng hoạt động):**
    1. Khi người dùng gọi API xem thống kê, hàm `Analysis Lambda` sẽ query vào Redis trước.
    2. Nếu có dữ liệu (Cache Hit), trả về ngay lập tức (thường dưới 1ms).
    3. Nếu không có (Cache Miss), Lambda sẽ chui qua RDS Proxy để lấy dữ liệu từ MySQL, sau đó ghi kết quả ngược lại vào Redis với một thời gian sống (TTL) nhất định, và trả về cho người dùng.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện quản lý cụm Amazon ElastiCache đang ở trạng thái "Available", hiển thị Endpoint (Đường dẫn kết nối) để cấu hình cho Lambda.
> *Mã Markdown:* `![Amazon ElastiCache Redis](../../../images/elasticache-redis.png)`