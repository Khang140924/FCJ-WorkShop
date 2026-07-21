---
title: "Amazon RDS Proxy"
date: 2026-07-21
weight: 3
chapter: false
pre: " <b> 5.4.3. </b> "
---

### Amazon RDS Proxy

### Mục tiêu
Trang này sẽ hướng dẫn các bạn cách truy cập **Amazon RDS Proxy Console** trên AWS để kiểm tra và xác minh trạng thái hoạt động của RDS Proxy, địa chỉ proxy endpoint, cấu hình mã hóa TLS, liên kết Secrets Manager và trạng thái target health (sức khỏe kết nối) của hệ thống **FinVantage**.

### Giới thiệu ngắn
Amazon RDS Proxy đóng vai trò làm lớp đệm trung gian quản lý kết nối giữa các hàm AWS Lambda backend và cơ sở dữ liệu quan hệ RDS PostgreSQL, đảm bảo hệ thống không bị gián đoạn khi có lượng request tăng đột biến.

### Vì sao Lambda kết nối RDS Proxy thay vì kết nối trực tiếp database?
1.  **Connection pooling (nhóm tài nguyên kết nối):** RDS Proxy duy trì sẵn một số lượng kết nối vật lý cố định vào PostgreSQL. Khi hàng loạt Lambda được kích hoạt đồng thời, chúng sẽ chia sẻ chung (multiplex) các kết nối này thay vì mỗi Lambda tự chiếm một kết nối riêng.
2.  **Tránh connection exhaustion (cạn kiệt tài nguyên kết nối):** Database PostgreSQL chỉ giới hạn số lượng kết nối tối đa. Nếu không có RDS Proxy, Lambda scale-up (nhân bản) nhanh chóng sẽ gây lỗi treo DB do quá tải kết nối.
3.  **Tăng tính bảo mật:** Ép buộc mã hóa kết nối giữa Lambda và DB Proxy qua chuẩn **Require TLS**.
4.  **Tự động Failover (Chuyển đổi dự phòng):** Nếu PostgreSQL database chính gặp sự cố, RDS Proxy tự động chuyển hướng sang DB standby mà không cần Lambda phải thay đổi endpoint kết nối hay khởi động lại.

---

### Các bước kiểm tra cấu hình trên AWS Console

**Bước 1:** Đăng nhập AWS Console → Tìm kiếm `RDS` → Chọn dịch vụ **RDS** → Nhấn vào mục **Proxies** ở menu bên trái.

**Bước 2:** Click chọn tên RDS Proxy của dự án (thường có tag Name là `finvantage-prod-proxy` hoặc tương đương).

**Bước 3:** Tại tab **Summary** (Tóm tắt) hoặc trang chi tiết chung, kiểm tra và xác minh:
*   **Proxy endpoint:** Ghi nhận địa chỉ kết nối của proxy: `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.
*   **Status:** Trạng thái hiển thị là `Available` (Sẵn sàng hoạt động).
*   **Require TLS:** Cấu hình phải hiển thị là `True` (Bắt buộc mã hóa đường truyền bảo mật).
*   **VPC, Subnets & Security groups:** Đảm bảo Proxy nằm trong VPC của dự án, đặt trong các Private Subnets và được gắn nhóm bảo mật `RDS-Proxy-SG`.

**Bước 4:** Tại phần **Connections** (Kết nối), kiểm tra mục **Secrets Manager secrets**:
*   Xác nhận tên Secrets Manager secret chứa credentials (thông tin đăng nhập) database đã được liên kết chính xác: `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → RDS → Proxies → click chọn Proxy của FinVantage → phần Summary/Connections.  
> Nội dung cần thấy: Proxy Endpoint, trạng thái Available, Require TLS: True và Secrets Manager secret được liên kết.  
> Tên ảnh đề xuất: `finvantage-rds-proxy-details.png`  
> Chú thích: “Hình 5.4.3a. Cấu hình chi tiết RDS Proxy (Endpoint, Require TLS, Secrets Manager) của dự án FinVantage.”

---

**Bước 5:** Tại menu con bên trái của trang Proxy hoặc tab **Targets** (Đích đến):
*   Click chọn target group mặc định `default`.
*   Xác minh **Target type** hiển thị là `Database` và cột **Target** trỏ đúng về RDS PostgreSQL Instance của dự án.
*   Xác minh cột **Target Health** (hoặc Status) hiển thị trạng thái `Available` hoặc `Healthy` (Màu xanh).

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → RDS → Proxies → click chọn Proxy của FinVantage → tab Targets / Target group.  
> Nội dung cần thấy: Target database instance của dự án và cột Target Health hiển thị trạng thái Available / Healthy.  
> Tên ảnh đề xuất: `finvantage-rds-proxy-target-health.png`  
> Chú thích: “Hình 5.4.3b. Trạng thái kết nối Target Group Health kết nối khỏe mạnh của RDS Proxy đến PostgreSQL Database.”

---

### Các lỗi thường gặp và cách xử lý
*   **Lỗi: `RDS Proxy Target status is Unavailable`**
    *   *Nguyên nhân:* Do Secrets Manager liên kết với Proxy có username/password bị sai lệch so với master password của Database PostgreSQL, hoặc do IAM role của RDS Proxy không có quyền truy cập đọc secret này.
    *   *Cách xử lý:* Kiểm tra lại giá trị lưu trong Secrets Manager và kiểm tra IAM Role của RDS Proxy xem đã được gắn Policy cho phép read secret chưa.

### Kết luận ngắn
RDS Proxy đã được cấu hình hoạt động ổn định, bảo đảm luồng kết nối từ các API Lambda xuống PostgreSQL luôn được định tuyến an toàn và chống quá tải.

---

### Danh sách hình ảnh cần chụp cho báo cáo
1.  `finvantage-rds-proxy-details.png` - Proxy Endpoint, Require TLS và Secrets Manager kết nối.
2.  `finvantage-rds-proxy-target-health.png` - Target Health kết nối giữa Proxy và PostgreSQL DB.