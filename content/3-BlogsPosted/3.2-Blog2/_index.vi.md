---
title: "Blog 2"
date: 2026-07-06
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# TỐI ƯU HÓA MÔI TRƯỜNG KIỂM THỬ VỚI AMAZON EKS VÀ VCLUSTER

Vấn đề muôn thuở khi vận hành các dự án sử dụng Kubernetes là việc cấp phát môi trường kiểm thử (QA/Testing) thường quá chậm chạp và tốn kém. Trước đây, mỗi khi cần một môi trường độc lập để test ứng dụng, các team phải chờ đợi đội ngũ nền tảng (Platform team) dựng hẳn một cụm Amazon EKS riêng biệt. Quá trình này ngốn đến 30-45 phút, kéo theo sự lãng phí khủng khiếp về tài nguyên (mỗi cụm lại "cõng" thêm Load Balancer, DNS, monitoring riêng) và khiến chi phí hạ tầng AWS tăng vọt.
Giải pháp triệt để cho vấn đề này đã được Deloitte áp dụng thành công: Kết hợp Amazon EKS (làm máy chủ nền tảng) và vCluster để tạo ra các cụm Kubernetes ảo (virtual clusters) siêu nhẹ, chạy chung trên một hạ tầng vật lý duy nhất.

Các điểm chính cần nắm:

* Tốc độ triển khai "siêu tốc": Thời gian tạo mới một môi trường kiểm thử giảm từ 45 phút xuống dưới 5 phút (nhanh hơn 89%). Lập trình viên và QA có ngay không gian độc lập để làm việc mà không cần pha cà phê chờ đợi.
* Vận hành tập trung, giảm thiểu rườm rà: Thay vì phải bảo trì hàng tá các công cụ (như Ingress controller, giám sát...) rải rác ở hàng chục cụm khác nhau, giờ đây tất cả dùng chung một bộ chia sẻ (shared stack) trên host cluster.
* Cắt giảm chi phí hạ tầng cực lớn: Việc dùng chung tài nguyên gốc giúp tiết kiệm hàng chục vCPU và hàng trăm GB RAM. Thậm chí có thể tiết kiệm đến 70% chi phí khi kết hợp linh hoạt tính năng EKS Auto Mode và chạy trên các EC2 Spot Instances.
* Trao quyền tự phục vụ (Self-service): Đội phát triển không còn bị phụ thuộc. Họ có thể tự "bấm nút" tạo môi trường Kubernetes ảo cho riêng mình trong vài phút, giúp giải phóng hoàn toàn sức lao động cho đội ngũ vận hành nền tảng.



![Bài Blog 2](images/blog2.png)

[Đường Link dẫn đến bài Blog 2](https://www.facebook.com/groups/awsstudygroupfcj/permalink/2205004010264559/)
