---
title: "Cổng giao tiếp API Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.5.1. </b> "
---

### Khởi tạo Amazon API Gateway

**Amazon API Gateway** đóng vai trò là "lễ tân" duy nhất của toàn bộ hệ thống backend. Mọi request từ Frontend (người dùng) bắt buộc phải đi qua cổng này trước khi được định tuyến (route) tới các hàm Lambda tương ứng.

#### 1. Xây dựng REST API
Chúng ta khởi tạo một REST API với cấu trúc các Endpoint rõ ràng:
*   `POST /invoice/import`: Nhận file hóa đơn. Trỏ tới `Import Lambda`.
*   `POST /payment/create`: Tạo giao dịch thủ công. Trỏ tới `Payment Lambda`.
*   `GET /analytics/summary`: Lấy thống kê chi tiêu. Trỏ tới `Analysis Lambda`.

#### 2. Tích hợp xác thực (Cognito Authorizer)
Để đảm bảo chỉ người dùng đã đăng nhập mới gọi được API, chúng ta gắn thêm **Cognito Authorizer** vào API Gateway.
*   Khi có request đến, API Gateway sẽ kiểm tra mã `JWT Token` trên Header. 
*   Nếu token hợp lệ, nó mới cho phép request đi tiếp vào Lambda. Nếu không, trả về lỗi `401 Unauthorized` ngay lập tức, giúp bảo vệ Lambda khỏi các cuộc gọi rác (tiết kiệm chi phí thực thi).

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện **Resources** của API Gateway, cho thấy cây thư mục các API endpoints (ví dụ `/invoice`, `/payment`) và luồng tích hợp (Integration Request) đang trỏ về các hàm Lambda.
> *Mã Markdown:* `![Cấu hình Amazon API Gateway](../../../images/api-gateway-routes.png)`