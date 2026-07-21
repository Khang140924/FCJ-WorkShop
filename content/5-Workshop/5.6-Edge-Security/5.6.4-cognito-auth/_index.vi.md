---
title: "Xác thực danh tính (Cognito)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.6.4. </b> "
---

### Quản lý Định danh & Phiên đăng nhập

Để đảm bảo dữ liệu tài chính của người nào chỉ người đó được xem, FinVantage sử dụng **Amazon Cognito** để quản lý danh tính (Identity Management) một cách an toàn và chuyên nghiệp.

#### 1. Khởi tạo Cognito User Pool
*   Tạo một **User Pool** làm nơi lưu trữ thông tin tài khoản người dùng (Email, Password).
*   Thiết lập chính sách mật khẩu mạnh (chữ hoa, số, ký tự đặc biệt).
*   Kích hoạt tính năng xác thực qua Email (Gửi mã OTP khi đăng ký hoặc quên mật khẩu).

#### 2. Tích hợp JWT Token với API Gateway
Luồng hoạt động xác thực của hệ thống diễn ra như sau:
1.  Người dùng nhập Email/Mật khẩu trên giao diện web.
2.  Frontend gửi thông tin đó đến Amazon Cognito.
3.  Cognito kiểm tra hợp lệ và trả về một **JSON Web Token (JWT)**.
4.  Khi người dùng muốn xem báo cáo chi tiêu, Frontend đính kèm JWT Token này vào Header của request.
5.  **API Gateway** (nhờ cấu hình Cognito Authorizer ở Phần 5.5) sẽ kiểm tra tính hợp lệ của Token trước khi cho phép request gọi xuống hàm Lambda.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện **Amazon Cognito User Pool**, phần "App clients and analytics" hoặc màn hình hiển thị danh sách người dùng đã đăng ký thành công (User management).
> *Mã Markdown:* `![Amazon Cognito User Pool](../../../images/cognito-user-pool.png)`