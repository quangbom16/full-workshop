---
title: "Báo cáo Tuần 2"
date: "2025-09-15"
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
--- 


### Mục tiêu Tuần 2:

* Bảo mật tài khoản AWS Root sử dụng xác thực đa yếu tố (MFA).
* Áp dụng các phương pháp tốt nhất về Quản lý danh tính và quyền truy cập (IAM - Identity and Access Management).
* Cấu hình các cài đặt chung cho tài khoản và nắm vững quy trình hỗ trợ (Support) của AWS.

### Các công việc thực hiện trong tuần:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2 | - **Bảo mật tài khoản:** <br> - Kiểm tra lại cài đặt tài khoản AWS mới tạo <br> - Thiết lập xác thực đa yếu tố (MFA) cho tài khoản Root <br> - **Thực hành:** <br>&emsp; + Kích hoạt Virtual MFA device cho Root User | 15/09/2025 | 19/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Tìm hiểu về IAM (Quản lý danh tính và truy cập) <br> - Tạo nhóm Admin (Admin Group) và người dùng Admin (Admin User) <br> - **Thực hành:** <br>&emsp; + Tạo Group "Administrators" <br>&emsp; + Tạo IAM User và thêm vào Group | 15/09/2025 | 19/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Hỗ trợ xác thực tài khoản (Account Authentication Support): <br>&emsp; + Thiết lập chính sách mật khẩu (Password Policy) <br>&emsp; + Tạo Account Alias (URL đăng nhập tùy chỉnh) <br> - Kiểm tra đăng nhập với IAM Admin User mới | 15/09/2025 | 19/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Khám phá và cấu hình AWS Management Console: <br>&emsp; + Tùy chỉnh các widget trên Dashboard <br>&emsp; + Thiết lập Cảnh báo thanh toán (Billing Alerts/Budgets) <br>&emsp; + Tìm hiểu cài đặt về Region và Availability Zones | 15/09/2025 | 19/09/2025 | <https://cloudjourney.awsstudygroup.com/> |
| 6 | - AWS Support: <br>&emsp; + Tìm hiểu các gói Support (Basic, Developer, Business, Enterprise) <br>&emsp; + Cách tạo Support Cases và quản lý case <br> - **Thực hành:** <br>&emsp; + Mô phỏng quy trình mở một ticket hỗ trợ | 15/09/2025 | 19/09/2025 | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được Tuần 2:

* Đã bảo mật thành công tài khoản Root User bằng cách kích hoạt MFA.

* Triển khai cấu trúc IAM chuẩn:
  * Tạo nhóm Admin chuyên dụng với quyền AdministratorAccess.
  * Tạo IAM User riêng cho các tác vụ hàng ngày để tránh sử dụng tài khoản Root.
  * Cấu hình chính sách mật khẩu chặt chẽ và tạo Account Alias để dễ dàng đăng nhập.

* Đã cấu hình giao diện AWS Management Console và thiết lập Budget/Billing Alarms để giám sát chi phí.

* Nắm rõ các cấp độ hỗ trợ (Support Plans) khác nhau của AWS và quy trình mở, quản lý case hỗ trợ khi gặp sự cố kỹ thuật hoặc vấn đề thanh toán.