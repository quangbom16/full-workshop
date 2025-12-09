---
title: "Báo cáo Tuần 3"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
--- 


### Mục tiêu Tuần 3:

* Nắm vững các thành phần cốt lõi của Amazon VPC (Virtual Private Cloud).
* Triển khai bảo mật mạng sử dụng Security Groups và Network ACLs.
* Triển khai máy ảo EC2 bên trong kiến trúc mạng tùy chỉnh.
* Hiểu về kết nối lai (Hybrid Connectivity) thông qua Site-to-Site VPN.

### Các công việc thực hiện trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2 | - **Giới thiệu về mạng VPC:** <br> - Tìm hiểu về CIDR blocks <br> - **1.1 Subnets:** Phân biệt Public và Private <br> - **1.2 Route Tables:** Liên kết (Associate) và quảng bá đường đi <br> - **1.3 Internet Gateway (IGW):** Cấp quyền truy cập Internet | 22/09/2025 | 26/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - **Mạng nâng cao & Tường lửa:** <br> - **1.4 NAT Gateway:** Cấp mạng Internet chiều đi cho Private Subnet <br> - **2. Firewall in VPC:** <br>&emsp; + Security Groups (Stateful) <br>&emsp; + Network ACLs (Stateless) | 22/09/2025 | 26/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - **3. Các bước chuẩn bị:** Lên quy hoạch địa chỉ IP cho VPC <br> - **4. Deploying Amazon EC2 Instances:** <br>&emsp; + Tạo một VPC tùy chỉnh (Custom VPC) <br>&emsp; + Khởi tạo EC2 trong Public Subnet <br>&emsp; + Khởi tạo EC2 trong Private Subnet | 22/09/2025 | 26/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - **5. Thiết lập kết nối Site-to-Site VPN:** <br> - Tìm hiểu Virtual Private Gateway (VGW) & Customer Gateway (CGW) <br> - Quy trình cấu hình VPN <br> - **Thực hành:** Cấu hình phía AWS cho kết nối VPN | 22/09/2025 | 26/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - **Rà soát & Xử lý sự cố:** <br> - Kiểm tra kết nối giữa các instance (Ping, SSH) <br> - Xác minh lại các quy tắc Security Group <br> - Xử lý các lỗi kết nối VPC thường gặp | 22/09/2025 | 26/09/2025 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được Tuần 3:

* Đã thiết kế và khởi tạo thành công một Virtual Private Cloud (VPC) với quy hoạch CIDR hợp lý.

* Cấu hình hoàn chỉnh các thành phần mạng:
  * Subnets (Public và Private).
  * Route Tables để điều hướng lưu lượng.
  * Internet Gateway cho truy cập công khai và NAT Gateway cho cập nhật từ mạng nội bộ.

* Bảo mật các lớp mạng bằng cách triển khai Security Groups (mức Instance) và Network ACLs (mức Subnet).

* Triển khai thành công các máy chủ EC2 vào trong hệ thống mạng tùy chỉnh và kiểm tra thông mạng.

* Nắm được kiến thức lý thuyết và quy trình thiết lập kết nối VPN Site-to-Site giữa AWS và môi trường on-premise.