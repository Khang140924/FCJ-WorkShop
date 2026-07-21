---
title: "NAT Gateway & Private Subnets"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### 1. Thiết lập Private Subnets (Mạng nội bộ)
Đây là khu vực "kín cổng cao tường", không cấp phát Public IP. Các dữ liệu nhạy cảm (như Database lưu thông tin thẻ/chi tiêu) sẽ được đặt tại đây.
*   **Private Subnet 1 (Database):** CIDR `10.0.10.0/24` (AZ `us-east-1a`)
*   **Private Subnet 2 (Database):** CIDR `10.0.20.0/24` (AZ `us-east-1b`)

### 2. Khởi tạo NAT Gateway
Các hàm Lambda nằm trong Private Subnet (ví dụ: `Analysis Lambda`) cần gọi ra ngoài Internet để giao tiếp với Amazon Bedrock AI. Vì không có IP Public, chúng cần đi qua một cổng trung gian là NAT Gateway.
*   **Vị trí đặt:** NAT Gateway bắt buộc phải nằm trong **Public Subnet**.
*   **Elastic IP:** Cấp phát một địa chỉ IP tĩnh (Elastic IP) cho NAT Gateway để nó đại diện cho các traffic từ Private Subnet đi ra ngoài.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình cấu hình chi tiết của NAT Gateway vừa tạo, bôi đỏ phần Subnet (nằm ở Public) và Elastic IP.
> *Mã Markdown:* `![Cấu hình NAT Gateway](../../../images/nat-gateway-config.png)`