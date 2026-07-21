---
title: "VPC & Internet Gateway"
date: 2026-07-20
weight: 1
chapter: false
pre: " <b> 5.3.1. </b> "
---

### 1. Khởi tạo Amazon VPC
Bước đầu tiên là tạo một vùng không gian mạng cô lập hoàn toàn trên AWS.
*   **Tên VPC:** `FinVantage-Production-VPC`
*   **Dải IP (IPv4 CIDR block):** `10.0.0.0/16`. Dải IP này cung cấp lên đến 65,536 địa chỉ IP, hoàn toàn dư dả để hệ thống tự động co giãn (auto-scaling) các hàm Lambda và tài nguyên sau này.

### 2. Thiết lập Internet Gateway (IGW)
Để VPC của chúng ta có thể giao tiếp với thế giới bên ngoài (Internet), cần phải gắn một Internet Gateway.
*   Khởi tạo một IGW tên là `FinVantage-IGW`.
*   Thực hiện hành động **Attach to VPC** và chọn `FinVantage-Production-VPC` vừa tạo.

### 3. Phân chia Public Subnets
Chúng ta tạo 2 Public Subnets nằm ở 2 Availability Zones (AZ) khác nhau để đảm bảo tính sẵn sàng cao (High Availability).
*   **Public Subnet 1:** CIDR `10.0.1.0/24` (Nằm tại AZ `us-east-1a`)
*   **Public Subnet 2:** CIDR `10.0.2.0/24` (Nằm tại AZ `us-east-1b`)
*   Bật tính năng *Auto-assign public IPv4 address* cho 2 subnet này.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình danh sách các Subnets vừa tạo trong giao diện VPC Console, hiển thị rõ cột IPv4 CIDR và Availability Zone.
> *Mã Markdown:* `![Danh sách Public Subnets](../../../images/public-subnets.png)`