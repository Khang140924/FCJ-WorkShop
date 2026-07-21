---
title: "Public và private subnet"
date: 2026-07-20
weight: 2
chapter: false
pre: " <b> 5.3.2. </b> "
---

### Public và private subnet

### Mục tiêu
Trang này sẽ hướng dẫn các bạn cách truy cập giao diện quản lý **Subnets** và **NAT Gateways** trên AWS Console để kiểm tra việc phân chia vùng mạng công khai/riêng tư, cấu hình đa vùng khả dụng Availability Zone (AZ) của hệ thống **FinVantage**.

### Giới thiệu ngắn
Để đạt tính bảo mật tối đa, một hệ thống mạng AWS luôn được chia thành hai vùng riêng biệt: public subnet (phân đoạn mạng công khai) tiếp xúc với Internet và private subnet (phân đoạn mạng riêng tư) bị cô lập hoàn toàn. Việc định cấu hình đúng đắn các Subnets này giúp đảm bảo dữ liệu quan trọng không thể bị truy cập trái phép.

### Vai trò của các phân đoạn mạng trong FinVantage
*   **Private Subnets:** Đây là nơi đặt cơ sở dữ liệu quan hệ Amazon RDS PostgreSQL và cụm bộ nhớ đệm Amazon ElastiCache Valkey/Redis. Để đảm bảo high availability (tính sẵn sàng cao), RDS và Valkey được cấu hình chạy Multi-AZ trên ít nhất hai Private Subnets nằm ở hai Availability Zone khác nhau (ví dụ: `ap-southeast-1a` và `ap-southeast-1b`). Nếu một AZ gặp sự cố, hệ thống sẽ tự động switch-over (chuyển đổi dự phòng) sang AZ còn lại mà không mất mát dữ liệu.
*   **Public Subnets:** Nơi đặt các cổng giao tiếp biên và đặc biệt là **NAT Gateway** (hoặc VPC Endpoint). Vì các hàm Lambda chạy backend nằm trong Private Subnet không có IP công cộng, chúng bắt buộc phải gửi lưu lượng mạng đi qua NAT Gateway đặt ở Public Subnet để có thể kết nối ra ngoài Internet và gọi API của Cognito, STS hay Bedrock.

---

### Các bước kiểm tra cấu hình trên AWS Console

#### 1. Kiểm tra danh sách Subnets

**Bước 1:** Tại thanh menu bên trái của giao diện **VPC Console**, click chọn **Subnets**.

**Bước 2:** Nhập tên dự án FinVantage vào ô lọc để hiển thị toàn bộ các subnets liên quan. 

**Bước 3:** Kiểm tra và xác minh cột **Availability Zone**:
*   Đảm bảo hệ thống có ít nhất 2 Public Subnets và 2 Private Subnets.
*   Kiểm tra cột **Availability Zone** hiển thị các AZs khác nhau (ví dụ: `ap-southeast-1a` và `ap-southeast-1b`) để xác nhận tính sẵn sàng cao.
*   Ghi nhận dải địa chỉ **IPv4 CIDR** của từng subnet: `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → VPC → Subnets.  
> Nội dung cần thấy: Danh sách các Subnets của dự án FinVantage, hiển thị rõ cột Name, IPv4 CIDR, và Availability Zone (ít nhất 2 AZs khác nhau như ap-southeast-1a và ap-southeast-1b).  
> Tên ảnh đề xuất: `finvantage-subnets.png`  
> Chú thích: “Hình 5.3.2a. Danh sách các Public và Private Subnets phân chia theo vùng khả dụng (Availability Zones) của dự án FinVantage.”

---

#### 2. Kiểm tra NAT Gateway

**Bước 1:** Tại thanh menu bên trái, click chọn **NAT Gateways**. (Trường hợp dự án của bạn sử dụng VPC Endpoint cho các dịch vụ cụ thể, bạn có thể click chọn menu **Endpoints**).

**Bước 2:** Chọn NAT Gateway của dự án (thường có tag Name là `FinVantage-NAT` hoặc `finvantage-prod-nat`).

**Bước 3:** Nhìn xuống bảng thông tin chi tiết:
*   Xác minh cột **State** hiển thị trạng thái `Available`.
*   Kiểm tra trường **Subnet**: Đảm bảo NAT Gateway được đặt chính xác tại một **Public Subnet** (nếu đặt nhầm ở Private Subnet, NAT Gateway sẽ không thể kết nối ra Internet).
*   Ghi nhận địa chỉ **Elastic IP** (địa chỉ IP tĩnh công cộng) được cấp phát cho NAT Gateway: `<LẤY GIÁ TRỊ THỰC TẾ TỪ AWS CONSOLE>`.

---

> 📸 HÌNH CẦN THÊM  
> Chụp màn hình: AWS Console → VPC → NAT Gateways.  
> Nội dung cần thấy: Chi tiết cấu hình của NAT Gateway, hiển thị rõ trạng thái Available, địa chỉ Elastic IP và thông tin Subnet thuộc Public Subnet.  
> Tên ảnh đề xuất: `finvantage-nat-gateway.png`  
> Chú thích: “Hình 5.3.2b. Cấu hình chi tiết NAT Gateway cấp phát IP tĩnh kết nối cho Private Subnets.”

---

### Các lỗi thường gặp và cách xử lý
*   **Lỗi: `Lambda timeout when calling Bedrock API`**
    *   *Nguyên nhân:* Hàm Lambda nằm ở Private Subnet không thể kết nối ra Internet do NAT Gateway bị cấu hình sai Subnet (đặt trong Private Subnet) hoặc chưa được cấp Elastic IP.
    *   *Cách xử lý:* Kiểm tra lại NAT Gateway trên Console, đảm bảo trường Subnet trỏ đúng về Public Subnet có gắn Route Table đi qua Internet Gateway.

### Kết luận ngắn
Hạ tầng chia subnet và cổng NAT Gateway đã sẵn sàng, tạo đường truyền kết nối an toàn cho các ứng dụng chạy ngầm của FinVantage.

---

### Danh sách hình ảnh cần chụp cho báo cáo
1.  `finvantage-subnets.png` - Danh sách Public và Private Subnets.
2.  `finvantage-nat-gateway.png` - Chi tiết NAT Gateway.