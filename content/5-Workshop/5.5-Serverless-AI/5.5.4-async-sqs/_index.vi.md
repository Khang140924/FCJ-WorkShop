---
title: "Xử lý Bất đồng bộ (Amazon SQS)"
date: 2026-07-20
weight: 4
chapter: false
pre: " <b> 5.5.4. </b> "
---

### Tối ưu hóa kiến trúc với Hàng đợi (Queue)

Quá trình Textract phân tích ảnh và Bedrock suy luận logic có thể mất từ 3 đến 10 giây. Nếu bắt người dùng (Frontend) đứng chờ quá trình này hoàn tất, ứng dụng sẽ bị đánh giá là chậm chạp (timeout). Do đó, hệ thống được thiết kế theo luồng **Bất đồng bộ (Async Processing)**.

#### 1. Sử dụng Amazon SQS (Simple Queue Service)
*   Thay vì gọi trực tiếp AI, `Import Lambda` chỉ cần đẩy một "Task" (chứa đường dẫn file S3) vào hàng đợi **Amazon SQS**, sau đó lập tức trả về phản hồi cho Frontend: *"Hóa đơn đang được xử lý!"*.
*   Hàng đợi SQS sẽ giữ các task này một cách an toàn, tránh tình trạng mất dữ liệu (data loss) khi có hàng ngàn người dùng upload cùng lúc.

#### 2. Worker Lambda & Dead Letter Queue (DLQ)
*   Chúng ta cấu hình một **Worker Lambda** có nhiệm vụ liên tục "lắng nghe" (poll) SQS. Cứ có task mới, nó sẽ lấy ra và gọi chuỗi logic Textract + Bedrock.
*   **Dead Letter Queue (DLQ):** Nếu một hóa đơn bị mờ, AI không đọc được, Worker Lambda báo lỗi 3 lần liên tiếp, task đó sẽ bị đẩy sang DLQ. Quản trị viên (Dev/Admin) có thể vào DLQ để xem lại các hóa đơn lỗi này mà không làm tắc nghẽn luồng xử lý chính.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện cấu hình của Amazon SQS, hiển thị Hàng đợi chính đang được liên kết với một Dead-letter queue (DLQ) và Lambda trigger.
> *Mã Markdown:* `![Cấu hình Hàng đợi Amazon SQS](../../../images/sqs-dlq-config.png)`