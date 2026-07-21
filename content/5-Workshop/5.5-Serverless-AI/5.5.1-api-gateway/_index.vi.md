---
title: "Amazon API Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### Amazon API Gateway

### Mục tiêu
Trang này sẽ hướng dẫn các bạn cách truy cập **Amazon API Gateway Console** trên AWS để kiểm tra và xác minh cấu hình định tuyến REST API (giao diện lập trình ứng dụng truyền tải trạng thái đại diện), liên kết Lambda Integration, CORS configuration (cấu hình chia sẻ tài nguyên nguồn gốc chéo) và deployment stage `prod` của hệ thống **FinVantage**.

### Giới thiệu ngắn
Amazon API Gateway đóng vai trò là "lễ tân biên" duy nhất tiếp nhận mọi yêu cầu HTTP từ Frontend gửi lên, sau đó kiểm tra bảo mật và định tuyến xuống các hàm Lambda xử lý tương ứng ở phía sau.

### Vai trò của API Gateway trong dự án FinVantage
*   **Định tuyến API (API Routing):** Ánh xạ chính xác các phương thức HTTP (GET, POST, PUT, DELETE) vào các hàm Lambda backend tương ứng.
*   **CORS (Cross-Origin Resource Sharing):** Cấu hình cho phép tên miền Frontend Amplify (`https://main.dp5hgt6k889yu.amplifyapp.com`) gửi request (yêu cầu) an toàn về API endpoint mà không bị trình duyệt chặn lại.
*   **Cognito Authorizer (bộ lọc chứng thực):** Bảo vệ các API nhạy cảm bằng cách kiểm tra tính hợp lệ của mã JWT token gửi kèm trên Header của request. Nếu token không hợp lệ hoặc hết hạn, API Gateway sẽ từ chối ngay lập tức, giúp tiết kiệm chi phí thực thi Lambda.

---

### Các bước kiểm tra cấu hình trên AWS Console

**Bước 1:** Đăng nhập AWS Console → Tìm kiếm `API Gateway` → Chọn dịch vụ **API Gateway**.

**Bước 2:** Tìm và click chọn tên API thực tế của dự án: **`stcs2116b8`** (thường có tag Name là `finvantage-prod` hoặc tương đương).

**Bước 3:** Tại thanh menu bên trái, click chọn **Resources** (hoặc **Routes**):
*   Xác minh danh sách các endpoints (các điểm cuối kết nối API) cốt lõi của hệ thống có hiển thị đầy đủ hay không:
    *   `GET /auth/health` - Kiểm tra sức khỏe dịch vụ auth.
    *   `GET /auth/config` - Lấy cấu hình xác thực Cognito.
    *   `GET /auth/me` - Kiểm tra thông tin phiên đăng nhập.
    *   `POST /invoices/import` - Nhận metadata và tạo presigned URL để upload hóa đơn.
    *   `POST /invoices/{id}/analyze` - Kích hoạt phân tích AI của hóa đơn.
    *   `GET /invoices` & `POST /invoices` - Lấy danh sách giao dịch hoặc tạo thủ công.
    *   `GET /invoices/{id}`, `PUT /invoices/{id}`, `DELETE /invoices/{id}` - Quản lý chi tiết hóa đơn.
    *   `GET /dashboard-summary` - Lấy dữ liệu báo cáo chi tiêu trực quan.
    *   `/budgets` & `/spending-plan` - Thiết lập hạn mức ngân sách và kế hoạch chi tiêu.
*   Click chọn một phương thức bất kỳ (ví dụ: `POST` của `/invoices/import`), kiểm tra mục **Integration type** hiển thị là `Lambda Function` và trỏ đúng về hàm Lambda tương ứng: `finvantage-prod-importInvoice`.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → API Gateway → APIs → click chọn `stcs2116b8` → tab Resources/Routes.  
> Nội dung cần thấy: Danh sách cây thư mục các API endpoints thực tế (như `/invoices`, `/dashboard-summary`, `/auth`), phương thức HTTP, và liên kết Lambda Integration tương ứng.  
> Tên ảnh đề xuất: `finvantage-api-gateway-routes.png`  
> Chú thích: “Hình 5.5.1. Cấu hình chi tiết các API Routes và liên kết Lambda Integration của dự án FinVantage.”

---

**Bước 4:** Click chọn mục **Stages** ở thanh menu bên trái:
*   Click chọn stage **`prod`**.
*   Ghi nhận địa chỉ **Invoke URL** (đường dẫn gọi API trực tuyến) được cấp phát: `https://stcs2116b8.execute-api.ap-southeast-1.amazonaws.com/prod`.

---

### Tìm hiểu các mã trạng thái HTTP (HTTP Status Codes) phổ biến
Khi thực hiện gọi API từ Frontend, API Gateway và Lambda sẽ trả về các mã trạng thái tiêu chuẩn sau:
*   **`200 OK` (hoặc `201 Created`):** Gọi API thành công, dữ liệu được xử lý và trả về chính xác.
*   **`401 Unauthorized`:** Chưa đăng nhập hoặc JWT token gửi lên không hợp lệ/hết hạn.
*   **`403 Forbidden`:** Request bị chặn do lỗi phân quyền hoặc lỗi cấu hình CORS (Domain Frontend chưa được cho phép).
*   **`404 Not Found`:** Đường dẫn API route không tồn tại hoặc tài nguyên (hóa đơn) yêu cầu không có trong DB.
*   **`500 Internal Server Error`:** Hàm Lambda backend gặp lỗi crash code (lỗi logic lập trình).
*   **`502 Bad Gateway`:** Lambda trả về kết quả không đúng định dạng JSON chuẩn của API Gateway hoặc Lambda bị quá thời gian chạy (Timeout).

### Kết luận ngắn
Amazon API Gateway đã được cấu hình định tuyến và phân stage `prod` chính xác, đóng vai trò cửa ngõ định tuyến an toàn cho ứng dụng FinVantage.

---

### Danh sách hình ảnh cần chụp cho báo cáo
1.  `finvantage-api-gateway-routes.png` - Danh sách API Routes và cấu hình Lambda Integration.