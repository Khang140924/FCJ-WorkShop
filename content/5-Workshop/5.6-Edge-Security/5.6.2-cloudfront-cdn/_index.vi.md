---
title: "Phân phối nội dung (CloudFront)"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.6.2. </b> "
---

### Mạng phân phối toàn cầu (CDN)

Vì Bucket S3 chứa Frontend đã bị khóa Public Access, người dùng sẽ không thể truy cập trực tiếp. Chúng ta dùng **Amazon CloudFront** đứng ra làm cầu nối phân phối nội dung.

#### 1. Khởi tạo CloudFront Distribution
CloudFront sẽ kéo (cache) giao diện web từ S3 và lưu trữ nó tại hàng trăm Edge Locations trên toàn cầu. Nhờ đó, người dùng ở Việt Nam hay Mỹ đều tải trang FinVantage với tốc độ tính bằng mili-giây.

#### 2. Bảo mật Origin với OAC (Origin Access Control)
Đây là kỹ thuật bảo mật cốt lõi để kết nối CloudFront với S3 "kín":
*   Trong cấu hình Origin của CloudFront, thiết lập **Origin Access Control (OAC)**.
*   CloudFront sẽ cung cấp một đoạn JSON Policy. Bạn copy đoạn Policy này và dán vào phần **Bucket Policy** của S3.
*   **Ý nghĩa:** S3 Bucket bây giờ sẽ chỉ mở cửa duy nhất cho luồng traffic đến từ con CloudFront phân phối này. Tất cả các request khác (kể cả copy link S3 dán ra trình duyệt) đều bị báo lỗi `403 Access Denied`.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Chụp màn hình giao diện cấu hình Origin của CloudFront, khoanh vùng phần **Origin access control settings (recommended)** đang được kích hoạt.
> *Mã Markdown:* `![Cấu hình CloudFront OAC](../../../images/cloudfront-oac.png)`