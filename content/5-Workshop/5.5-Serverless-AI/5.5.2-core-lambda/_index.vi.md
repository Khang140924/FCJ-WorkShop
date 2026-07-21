---
title: "Thiết kế Lambda theo chức năng"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.5.2. </b> "
---

### Thiết kế Lambda theo chức năng

### Mục tiêu
Trang này sẽ hướng dẫn các bạn cách truy cập **AWS Lambda Console** để kiểm tra và xác minh cấu hình thực thi (tên hàm, Node.js 24 runtime, bộ nhớ Memory, thời gian Timeout), cấu hình mạng VPC, biến môi trường và vai trò thực thi IAM của các hàm Lambda backend trong hệ thống **FinVantage**.

### Giới thiệu ngắn
AWS Lambda là trái tim xử lý của toàn bộ backend FinVantage. Hệ thống áp dụng mô hình micro-services (dịch vụ nhỏ độc lập), chia nhỏ toàn bộ mã nguồn thành các hàm chạy độc lập để tối ưu hóa hiệu năng, co giãn tự động theo sự kiện và dễ dàng cô lập lỗi khi phát sinh sự cố.

### Vai trò của các hàm Lambda nghiệp vụ trong FinVantage

| Tên Hàm Lambda Production | Bộ Kích Hoạt (Trigger) | Chức Năng Nghiệp Vụ Cốt Lõi | Dịch Vụ Liên Quan |
| :--- | :--- | :--- | :--- |
| **`finvantage-prod-authApi`** | API Gateway | Xử lý callback đăng nhập từ Cognito, tạo phiên làm việc và ghi session vào Valkey/Redis. | Cognito, Valkey |
| **`finvantage-prod-importInvoice`** | API Gateway | Nhận metadata của hóa đơn, tạo `invoiceId`, `cacheKey`, và sinh S3 presigned URL trả về cho Frontend. | Amazon S3 |
| **`finvantage-prod-ocrInvoice`** | S3 ObjectCreated | Kích hoạt tự động khi ảnh hóa đơn được upload lên S3. Gọi Textract bóc văn bản thô và cache vào Redis. | Textract, Valkey |
| **`finvantage-prod-analyzeInvoice`** | API Gateway / Web | Lấy OCR text từ Redis, AssumeRole sang tài khoản Bedrock để phân tích và lưu PostgreSQL. | Bedrock, RDS Proxy |
| **Các hàm CRUD Invoices** | API Gateway | Quản lý vòng đời hóa đơn: `create`, `list`, `search`, `get`, `update`, `delete`. | RDS Proxy |
| **`finvantage-prod-budgetsApi`** | API Gateway | Thiết lập, cập nhật hạn mức chi tiêu hàng tháng và so sánh với tổng chi để cảnh báo. | RDS Proxy |
| **`finvantage-prod-dashboardSummary`** | API Gateway | Thống kê tổng hợp chi tiêu theo danh mục, biểu đồ chi tiêu hàng ngày của người dùng. | RDS Proxy |
| **`finvantage-prod-profileApi`** | API Gateway | Đồng bộ thông tin người dùng từ Cognito và quản lý tùy chọn ngôn ngữ/giao diện. | RDS Proxy |

---

### Các bước kiểm tra cấu hình Lambda trên AWS Console

**Bước 1:** Đăng nhập AWS Console → Tìm kiếm `Lambda` → Chọn dịch vụ **Lambda** → Click vào **Functions** ở thanh menu bên trái.

**Bước 2:** Chọn một hàm Lambda nghiệp vụ bất kỳ (ví dụ: `finvantage-prod-analyzeInvoice` để kiểm tra).

**Bước 3:** Tại tab **Code** hoặc phần **General configuration** (Cấu hình chung) dưới tab **Configuration**, xác minh:
*   **Runtime:** `Node.js 24.x` (môi trường thực thi mã nguồn Javascript mới nhất).
*   **Handler:** `src/handlers/analysisHandler.handler` (đường dẫn trỏ đúng vào file và hàm export handler trong code).
*   **Memory:** Ghi nhận dung lượng RAM cấp phát (ví dụ: 1024 MB): `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.
*   **Timeout:** Thời gian chạy tối đa trước khi bị ngắt (ví dụ: 30 giây hoặc 1 phút): `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.

---

**Bước 4:** Chuyển sang tab **Configuration** → chọn mục **VPC** ở menu bên trái:
*   Xác minh Lambda được gắn vào đúng VPC của dự án.
*   **Subnets:** Đảm bảo được gắn vào **2 Private Subnets** để giao tiếp an toàn trong mạng nội bộ.
*   **Security groups:** Được liên kết chính xác nhóm bảo mật **`Lambda-SG`** (Outbound: All Traffic, Inbound: Trống).

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → Lambda → Functions → Chọn `finvantage-prod-analyzeInvoice` → tab Configuration → mục VPC.  
> Nội dung cần thấy: Thông tin VPC liên kết, 2 Private Subnets của Singapore region, và nhóm bảo mật Lambda-SG được gán.  
> Tên ảnh đề xuất: `finvantage-lambda-vpc.png`  
> Chú thích: “Hình 5.5.2a. Cấu hình gắn kết mạng ảo VPC (2 Private Subnets và Lambda-SG) cho hàm Lambda.”

---

**Bước 5:** Vẫn ở tab **Configuration**, chọn mục **Environment variables** (Biến môi trường):
*   Xác minh các biến cấu hình cần thiết được nạp đầy đủ (như `DB_HOST`, `REDIS_URL`, `BEDROCK_ROLE_ARN`, `BEDROCK_MODEL_ID`...).
*   *Lưu ý bảo mật:* Không chụp các giá trị mật khẩu hay token nhạy cảm trong biến môi trường.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → Lambda → Functions → Chọn `finvantage-prod-analyzeInvoice` → tab Configuration → mục General configuration / Environment variables.  
> Nội dung cần thấy: Runtime Node.js 24, Timeout, Memory, và danh sách các biến môi trường cấu hình (che các secret).  
> Tên ảnh đề xuất: `finvantage-lambda-settings.png`  
> Chú thích: “Hình 5.5.2b. Cấu hình thuộc tính thực thi (Runtime, Memory, Timeout) và biến môi trường của Lambda function.”

---

**Bước 6:** Chọn mục **Permissions** (Quyền hạn) ở tab Configuration:
*   Xác minh **Execution role** (vai trò thực thi cấp quyền) được liên kết đúng. Đây là nơi chứa các quyền IAM gán cho Lambda (quyền ghi logs CloudWatch, quyền đọc ghi S3, quyền gọi Textract, và quyền AssumeRole sang Bedrock).

---

### Tìm hiểu các lỗi Bundler thường gặp khi đóng gói Lambda
Trong quá trình triển khai dự án, chúng ta thường gặp lỗi đóng gói (bundling) do esbuild khi dùng định dạng ESM (ECMAScript Modules):
*   **Lỗi: `Dynamic require of "path" is not supported` hoặc `API Gateway trả về 502 Bad Gateway`**
    *   *Nguyên nhân:* Do esbuild khi bundle code sang single file định dạng ESM đã gặp lỗi import động các thư viện CommonJS cũ không tương thích.
    *   *Cách xử lý:* Thêm thuộc tính `banner` để tiêm `createRequire` vào file cấu hình bundler của Serverless để giả lập import CommonJS tương thích ngược:
        ```javascript
        banner: "import { createRequire } from 'module'; const require = createRequire(import.meta.url);"
        ```
    *   *Lưu ý:* Sau khi sửa lỗi đóng gói code Lambda và deploy lại, **tuyệt đối không cần chạy lại database migration production** vì cấu trúc database PostgreSQL đã hoàn thành trước đó.

### Kết luận ngắn
Các hàm Lambda nghiệp vụ đã được cấu hình runtime Node.js 24, liên kết mạng VPC an toàn và sẵn sàng xử lý các yêu cầu nghiệp vụ của FinVantage.

---

### Danh sách hình ảnh cần chụp cho báo cáo
1.  `finvantage-lambda-vpc.png` - Cấu hình VPC Subnets và Security Group gán cho Lambda.
2.  `finvantage-lambda-settings.png` - Cấu hình Runtime, General Settings và các biến môi trường của Lambda.