---
title: "Tích hợp AI (Textract & Bedrock)"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.5.3. </b> "
---

### Tự động hóa với Trí tuệ Nhân tạo

Đây là tính năng "ăn tiền" nhất của FinVantage. Chúng ta sử dụng hàm `Parse & Categorize Lambda` kết hợp cùng lúc 2 dịch vụ AI của AWS.

#### 1. Trích xuất văn bản với Amazon Textract (OCR)
Khi file hóa đơn (ảnh/PDF) vừa đáp xuống S3, nó sẽ đánh thức `Parse & Categorize Lambda`. 
*   Lambda sẽ gọi API của **Amazon Textract** (`AnalyzeDocument`).
*   Textract sử dụng học máy (Machine Learning) để nhận diện chữ viết, bảng biểu và bóc tách ra các trường thông tin thô (Ví dụ: "Trà sữa", "50,000đ", "12/07/2026").

#### 2. Phân loại thông minh với Amazon Bedrock (LLM)
Dữ liệu thô từ Textract chưa có ý nghĩa thống kê. `Parse & Categorize Lambda` tiếp tục gom đoạn text đó và gửi một Prompt đến **Amazon Bedrock** (sử dụng mô hình như Claude 3).
*   **Prompt ví dụ:** *"Dựa vào nội dung hóa đơn này: [Dữ liệu Textract], hãy phân loại chi tiêu vào một trong các danh mục (Ăn uống, Mua sắm, Đi lại) và xuất ra định dạng JSON".*
*   Bedrock trả về kết quả JSON chuẩn xác. Sau đó Lambda mới lưu kết quả cuối cùng này vào Amazon RDS (thông qua RDS Proxy).

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Bạn có thể chụp màn hình đoạn code Python/Node.js gọi `boto3.client('bedrock-runtime')` trong AWS Lambda, HOẶC chụp một log kết quả trả về (JSON) từ Bedrock trên CloudWatch.
> *Mã Markdown:* `![Code tích hợp Amazon Bedrock](../../../images/bedrock-integration.png)`