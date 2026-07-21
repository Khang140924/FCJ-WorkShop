---
title: "Live Demo & Đúc kết"
date: 2026-07-20
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

### Trải nghiệm Hệ thống & Đánh giá Kiến trúc

#### 1. Kịch bản Live Demo
Hệ thống FinVantage đã sẵn sàng hoạt động thực tế. Kịch bản kiểm thử (Test Case) bao gồm:
1. Truy cập giao diện ứng dụng qua domain CloudFront, đăng nhập thông qua Amazon Cognito.
2. Upload một bức ảnh hóa đơn thực tế (ví dụ: hóa đơn đi siêu thị hoặc ăn uống).
3. Hệ thống hiển thị trạng thái "Đang xử lý". Ở hậu trường, file vào S3, đánh thức Textract quét chữ, Bedrock phân tích và SQS quản lý hàng đợi.
4. Refresh trang và chiêm ngưỡng hóa đơn đã được AI bóc tách thông minh, tự động gán nhãn "Ăn uống" và lưu gọn gàng vào CSDL MySQL.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện ứng dụng FinVantage của bạn (trên trình duyệt) hiển thị kết quả một hóa đơn vừa được AI nhận diện và phân loại thành công.
> *Mã Markdown:* `![Giao diện kết quả Live Demo](../../images/live-demo-result.png)`

#### 2. Bài học kinh nghiệm (Reflection)
Quá trình triển khai kiến trúc Serverless + AI mang lại những bài học kỹ thuật quý giá:
*   **Nỗi đau "Cold Start" (Khởi động lạnh):** Các hàm Lambda nằm trong Private VPC ban đầu sẽ mất thêm vài giây để khởi tạo kết nối mạng (ENI). Việc kết hợp Amazon ElastiCache (để lưu cache) và thiết kế xử lý luồng bất đồng bộ bằng SQS đã giúp che giấu độ trễ này khỏi trải nghiệm của người dùng.
*   **Quyền lực của RDS Proxy:** Kết nối trực tiếp Lambda vào RDS truyền thống là "tự sát" nếu có bùng nổ traffic. Sự hiện diện của RDS Proxy đóng vai trò như một bộ phuộc nhún hoàn hảo, gánh vác việc chia sẻ Connection Pool một cách trơn tru.
*   **Vận hành Trí tuệ Nhân tạo:** Việc dùng Textract (OCR) kết hợp với Bedrock (LLM) hiệu quả hơn rất nhiều so với tự train mô hình từ đầu, tối ưu hóa thời gian đưa sản phẩm ra thị trường (Time-to-Market).