---
title: "Tầng Serverless & Trí tuệ nhân tạo"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

### Trái tim của FinVantage: Serverless & AI

Ở các phần trước, chúng ta đã xây dựng xong "nhà kho" (Database) và "bức tường thành" (VPC/Security Groups). Bây giờ là lúc xây dựng các "công nhân" (Compute) để xử lý logic kinh doanh.

Điểm đặc biệt của FinVantage là ứng dụng hoàn toàn kiến trúc **Serverless (Phi máy chủ)**. Thay vì thuê một máy chủ EC2 chạy 24/7 gây lãng phí, chúng ta sử dụng AWS Lambda để hệ thống chỉ chạy (và tính tiền) khi có request thực tế. 

Đồng thời, tầng này cũng là nơi tích hợp các dịch vụ Trí tuệ nhân tạo (AI) để hiện thực hóa tính năng bóc tách và phân loại hóa đơn tự động.

Trong phần này, chúng ta sẽ thực hành:
1. Thiết lập cổng giao tiếp Amazon API Gateway.
2. Triển khai các hàm AWS Lambda xử lý logic cốt lõi.
3. Tích hợp AI (Amazon Textract và Amazon Bedrock).
4. Tối ưu hệ thống bằng kiến trúc xử lý bất đồng bộ (Amazon SQS).