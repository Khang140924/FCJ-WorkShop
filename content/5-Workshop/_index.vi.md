---
title: "Workshop"
date: 2026-07-20
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# THỰC HÀNH TRIỂN KHAI HẠ TẦNG ĐÁM MÂY FINVANTAGE

### Tổng quan (Overview)

Trong lĩnh vực công nghệ tài chính (FinTech) hiện đại, việc duy trì một hệ thống ổn định, tự động hóa cao và bảo mật nghiêm ngặt dữ liệu người dùng là yếu tố sống còn. 

Trong bài Lab này, bạn sẽ tự tay thực hành thiết kế, cấu hình và triển khai toàn bộ hạ tầng đám mây AWS cho nền tảng **FinVantage** (Hệ thống Quản lý Chi tiêu & Cảnh báo Tài chính Cá nhân). Hệ thống được xây dựng theo kiến trúc **Serverless** (Phi máy chủ) kết hợp AI, phân tách rõ ràng các tầng dịch vụ. 

Đặc biệt, bài thực hành nhấn mạnh vào tư duy thiết kế hệ thống và bảo mật cốt lõi thông qua việc ẩn giấu hoàn toàn cơ sở dữ liệu vào mạng nội bộ (Private Subnets), xử lý bất đồng bộ (Async) và tự động hóa trích xuất dữ liệu.

### Các Dịch vụ Trọng tâm (Core Services Utilized)

*   **Entry & Security:** AWS WAF, Amazon CloudFront, Amazon S3, Amazon Cognito.
*   **Compute & APIs:** Amazon API Gateway, AWS Lambda.
*   **AI & OCR:** Amazon Textract, Amazon Bedrock.
*   **Database & Cache:** Amazon RDS (MySQL), Amazon RDS Proxy, Amazon ElastiCache.
*   **Async Processing:** Amazon SQS, Amazon SNS.
*   **Observability:** Amazon CloudWatch, AWS X-Ray, AWS CloudTrail.

### Lộ trình Thực hành (Workshop Content)

1. [Tổng quan Workshop](5.1-workshop-overview/): Tìm hiểu bài toán thực tế và phân tích Sơ đồ kiến trúc giải pháp.
2. [Điều kiện tiên quyết](5.2-prerequisite/): Chuẩn bị môi trường AWS, IAM Role và quyền truy cập mô hình AI.
3. [Hạ tầng VPC & Mạng](5.3-vpc-networking/): Xây dựng khung mạng nội bộ, định tuyến Public/Private và tối ưu bảo mật.
4. [Tầng Dữ liệu & Bộ đệm](5.4-data-cache-layer/): Triển khai Amazon RDS, ElastiCache và cấu hình RDS Proxy.
5. [Tầng Serverless & AI](5.5-serverless-ai/): Cấu hình API Gateway, viết logic AWS Lambda và tích hợp Textract, Bedrock.
6. [Tầng Biên & Bảo mật](5.6-edge-security/): Phân phối tĩnh qua S3/CloudFront, thiết lập AWS WAF và xác thực Cognito.
7. [Giám sát & Cảnh báo](5.7-observability/): Theo dõi CloudWatch, truy vết X-Ray và thiết lập cảnh báo SNS.
8. [Live Demo & Đúc kết kinh nghiệm](5.8-live-demo/): Trải nghiệm thực tế hệ thống và rút ra các bài học tối ưu.
9. [Dọn dẹp tài nguyên](5.9-cleanup/): Phá hủy hạ tầng an toàn để triệt tiêu chi phí phát sinh.

> 📸 **[NHẮC NHỞ CHÈN ẢNH]:** Ở trang tổng này, bạn **không bắt buộc** phải chèn ảnh. Tuy nhiên, nếu muốn trang bìa đẹp hơn, bạn có thể chèn một logo AWS hoặc một ảnh minh họa dự án FinVantage thật ngầu vào ngay dưới tiêu đề chính.