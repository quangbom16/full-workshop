---
title: "Các bài blogs đã dịch"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### [Blog 1 - Automating AWS Private CA audit reports and certificate expiration alerts](3.1-Blog1/)
Bài viết này hướng dẫn cách xây dựng một quy trình tự động hóa để giám sát và cảnh báo về việc hết hạn chứng chỉ số do AWS Private CA cấp. Giải pháp sử dụng kết hợp các dịch vụ **EventBridge, Lambda, S3, SNS và Security Hub** để tạo báo cáo kiểm tra (audit reports) hàng ngày. Điều này giúp quản trị viên chủ động phát hiện các chứng chỉ sắp hết hạn (kể cả những chứng chỉ tạo qua API không được ACM theo dõi tự động), đảm bảo tuân thủ bảo mật và tránh gián đoạn dịch vụ.

### [Blog 2 - Announcing second-generation AWS Outposts racks with breakthrough performance](3.2-Blog2/)
Bài viết công bố sự ra mắt của **AWS Outposts racks thế hệ thứ 2**, mang lại hiệu suất và khả năng mở rộng vượt trội cho môi trường on-premises (tại cơ sở). Điểm nổi bật bao gồm việc hỗ trợ các instance EC2 thế hệ thứ 7 (C7i, M7i, R7i) giúp tăng hiệu suất xử lý lên tới 40%, kiến trúc mạng được tái thiết kế để đơn giản hóa việc mở rộng, và sự ra đời của các instance chuyên biệt dành cho các workload yêu cầu độ trễ cực thấp và thông lượng cao (như giao dịch tài chính hay mạng 5G).

### [Blog 3 - AWS Lambda standardizes billing for INIT Phase](3.3-Blog3/)
Bài viết thông báo về thay đổi quan trọng trong chính sách giá của AWS: Từ ngày 01/08/2025, giai đoạn khởi tạo (INIT phase/cold start) sẽ được tính phí đối với tất cả các cấu hình hàm Lambda. Nội dung bài viết giải thích chi tiết về vòng đời thực thi của một hàm Lambda, hướng dẫn cách sử dụng CloudWatch để giám sát thời lượng INIT, và đề xuất các chiến lược tối ưu hóa chi phí như sử dụng **Lambda SnapStart** hoặc **Provisioned Concurrency** để giảm thiểu tác động của thay đổi này.