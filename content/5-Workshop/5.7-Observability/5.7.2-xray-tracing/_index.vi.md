---
title: "Truy vết hệ thống (AWS X-Ray)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.7.2. </b> "
---

### Phân tích độ trễ với AWS X-Ray

Khi một người dùng upload hóa đơn, request sẽ đi qua rất nhiều trạm. Nếu API trả về chậm (ví dụ mất tới 5 giây), chúng ta cần biết chính xác khoảng thời gian đó bị kẹt ở đâu.

**AWS X-Ray** là công cụ hoàn hảo cho kiến trúc Serverless.
*   **Kích hoạt:** Bật tính năng *Active tracing* trong cấu hình của Amazon API Gateway và các hàm AWS Lambda.
*   **Service Map (Bản đồ dịch vụ):** X-Ray sẽ tự động vẽ ra một bản đồ kết nối trực quan mạng lưới FinVantage. Bạn sẽ nhìn thấy request đi từ Client -> API Gateway -> Lambda -> Textract -> Bedrock -> RDS.
*   **Traces:** Cung cấp biểu đồ Gantt phân tích thời gian từng chặng. Giúp chúng ta nhận ra ngay nếu mô hình Bedrock AI phản hồi chậm hay do câu query MySQL chưa được tối ưu.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình **Service Map** của AWS X-Ray (những vòng tròn kết nối với nhau) hoặc biểu đồ Traces hiển thị thanh thời gian của một request.
> *Mã Markdown:* `![Bản đồ truy vết AWS X-Ray](../../../images/xray-service-map.png)`