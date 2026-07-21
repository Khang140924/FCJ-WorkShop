---
title: "Triển khai Database (Amazon RDS)"
date: 2026-07-21
weight: 2
chapter: false
pre: " <b> 5.4.2. </b> "
---

### 1. Tạo Subnet Group cho Database
Để đảm bảo Amazon RDS nằm hoàn toàn trong mạng nội bộ, chúng ta cần gộp 2 Private Subnets (đã tạo ở phần trước) thành một nhóm.
*   Truy cập RDS Console > **Subnet groups**.
*   Tạo nhóm mới, chọn VPC của dự án và add 2 Private Subnets vào.

### 2. Khởi tạo Amazon RDS (MySQL)
Tiến hành tạo một Database Instance để lưu trữ dữ liệu tài chính.
*   **Engine:** MySQL.
*   **Deployment Option:** Chọn **Multi-AZ DB Instance**. Tính năng này cho phép RDS tự động tạo một bản sao (Standby) ở Availability Zone thứ 2. Nếu máy chủ chính sập, hệ thống sẽ tự động chuyển hướng sang máy chủ dự phòng mà không mất dữ liệu.
*   **Connectivity:** 
    *   Virtual Private Cloud (VPC): Chọn VPC của dự án.
    *   Subnet group: Chọn nhóm vừa tạo ở bước 1.
    *   Public access: **No** (Cực kỳ quan trọng để bảo mật).
    *   VPC security group: Chọn `Database-SG` (Chỉ cho phép Inbound từ Lambda).

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình thông tin chi tiết của RDS (Tab **Connectivity & security**), khoanh đỏ chữ "Publicly accessible: No" và "Multi-AZ: Yes".
> *Mã Markdown:* `![Cấu hình Amazon RDS](../../../images/rds-multi-az.png)`