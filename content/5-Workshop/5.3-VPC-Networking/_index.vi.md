---
title: "Hạ tầng VPC & Mạng"
date: 2026-07-20
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Tổng quan Tầng Mạng (Networking Layer)

Trong kiến trúc Serverless của FinVantage, tầng mạng đóng vai trò là "bức tường thành" vật lý đầu tiên. 

Dù phần lớn logic xử lý nằm ở AWS Lambda (được AWS quản lý hạ tầng), nhưng cơ sở dữ liệu (Amazon RDS, ElastiCache) lại yêu cầu một không gian mạng cực kỳ bảo mật để tránh rò rỉ dữ liệu tài chính. Do đó, chúng ta sẽ tự tay thiết kế một **Amazon VPC (Virtual Private Cloud)** tùy chỉnh với chiến lược phân tách mạng (Network Segmentation) rõ rệt.

Trong phần này, chúng ta sẽ lần lượt thực hành:
1. Khởi tạo không gian mạng VPC và Internet Gateway.
2. Xây dựng các mạng nội bộ (Private Subnets) và cổng giao tiếp NAT Gateway.
3. Thiết lập luồng định tuyến (Route Tables) và tường lửa (Security Groups).