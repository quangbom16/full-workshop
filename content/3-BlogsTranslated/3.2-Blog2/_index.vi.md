---
title: "Thông báo thế hệ thứ hai của AWS Outposts racks với hiệu suất và khả năng mở rộng đột phá tại cơ sở"
date: "2025-11-10"
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

*Bởi Micah Walter*

- Bài viết gốc: <a href="https://aws.amazon.com/vi/blogs/aws/announcing-second-generation-aws-outposts-racks-with-breakthrough-performance-and-scalability-on-premises/"
   target="_blank" 
   rel="noopener noreferrer">
   Announcing second-generation AWS Outposts racks with breakthrough performance and scalability on-premises - AWS News Blog
</a>

- doc: <a href="https://docs.google.com/document/d/1mB6ErhrYN0f5nNnMISk67VDqtof5zET2NPsDZiXnRyM/edit?usp=sharing"
   target="_blank" 
   rel="noopener noreferrer">
   GG docs
</a>

Hôm nay, chúng tôi công bố sự ra mắt rộng rãi của thế hệ thứ hai AWS Outposts racks, đánh dấu sự đổi mới mới nhất từ AWS cho edge computing. Thế hệ mới này bao gồm hỗ trợ cho các instance Amazon Elastic Compute Cloud (Amazon EC2) chạy x86 mới nhất, khả năng mở rộng và cấu hình mạng đơn giản hóa mới, cùng với các instance networking được tăng tốc được thiết kế đặc biệt cho các workload có độ trễ cực thấp và thông lượng cao. Những cải tiến này mang lại hiệu suất cao hơn cho nhiều loại workload tại chỗ, chẳng hạn như các hệ thống giao dịch cốt lõi của dịch vụ tài chính và các workload 5G Core của viễn thông.

Các khách hàng như athenahealth, FanDuel, First Abu Dhabi Bank, Mercado Libre, Liberty Latin America, Riot Games, Vector Limited và Wiwynn đã và đang sử dụng Outposts racks cho các workload cần duy trì tại chỗ. Outposts rack thế hệ thứ hai có thể cung cấp độ trễ thấp, xử lý dữ liệu cục bộ hoặc đáp ứng nhu cầu về data residency, chẳng hạn như game servers cho các trò chơi trực tuyến nhiều người chơi, dữ liệu giao dịch của khách hàng, hồ sơ y tế, hệ thống điều khiển công nghiệp và sản xuất, Business Support Systems (BSS) của viễn thông và edge inference của nhiều mô hình machine learning (ML). Giờ đây, khách hàng có thể tận dụng thế hệ bộ xử lý mới nhất và các cấu hình Outposts racks tiên tiến hơn để hỗ trợ xử lý nhanh hơn, dung lượng bộ nhớ cao hơn và băng thông mạng tăng lên.

### Các instance EC2 thế hệ mới nhất

Chúng tôi rất vui mừng thông báo hỗ trợ cục bộ cho thế hệ mới nhất (thế hệ thứ 7) của các instance Amazon EC2 chạy x86 trên AWS Outposts racks, bắt đầu với các instance C7i compute-optimized, các instance M7i general-purpose và các instance R7i memory-optimized. Các instance mới này cung cấp gấp đôi vCPU, memory và network bandwidth trong khi mang lại hiệu suất tốt hơn tới 40% so với các instance C5, M5 và R5 trên Outposts racks thế hệ trước.

Chúng được cung cấp sức mạnh bởi bộ xử lý Intel Xeon Scalable thế hệ thứ 4 và lý tưởng cho nhiều loại workload tại chỗ yêu cầu hiệu suất nâng cao như các database lớn hơn, các ứng dụng tiêu tốn nhiều memory hơn, phân tích big data thời gian thực nâng cao, mã hóa và streaming video hiệu suất cao, và edge inference dựa trên CPU với các mô hình ML phức tạp hơn. Hỗ trợ cho nhiều instance EC2 thế hệ mới nhất, bao gồm các instance hỗ trợ GPU, sẽ sớm ra mắt.

Video này sẽ giải thích những tiến bộ lớn trong AWS Outposts racks mới.

- Video này sẽ giải thích những tiến bộ lớn trong AWS Outposts racks mới: <a href="https://www.youtube.com/watch?v=Mu231AhT1AE"
   target="_blank" 
   rel="noopener noreferrer">
   Next-gen AWS Outposts racks: Built for tomorrow’s on-premises demands | Amazon Web Services
</a>

### Đơn giản hoá khả năng mở rộng và cấu hình mạng

Chúng tôi đã hoàn toàn tái thiết kế networking trong thế hệ Outposts mới nhất của mình, làm cho nó đơn giản và có khả năng mở rộng hơn bao giờ hết. Trọng tâm của bản nâng cấp này là Outposts network rack mới của chúng tôi, hoạt động như một trung tâm cho tất cả lưu lượng compute và storage của bạn.

Thiết kế mới này mang lại ba lợi ích chính:
1.  Giờ đây bạn có thể mở rộng tài nguyên compute của mình độc lập với cơ sở hạ tầng networking, mang lại cho bạn sự linh hoạt và hiệu quả chi phí hơn khi các workload của bạn phát triển.
2.  Chúng tôi đã tích hợp khả năng phục hồi mạng ngay từ đầu, với network rack tự động xử lý các lỗi thiết bị để giữ cho hệ thống của bạn hoạt động trơn tru.
3.  Việc kết nối với môi trường tại chỗ và AWS Regions giờ đây trở nên dễ dàng – bạn có thể cấu hình mọi thứ từ địa chỉ IP đến cài đặt VLAN và BGP thông qua các API đơn giản hoặc giao diện console được cập nhật của chúng tôi.

### Các instance Amazon EC2 chuyên biệt với accelerated networking

Chúng tôi đang giới thiệu một danh mục mới các instance Amazon EC2 chuyên biệt trên Outposts racks với accelerated networking. Các instance này được xây dựng có mục đích cho các workload mission-critical nhạy cảm nhất về độ trễ, chuyên sâu về compute và thông lượng cao nhất tại chỗ. Để mang lại hiệu suất tốt nhất có thể, ngoài Outpost logical network, các instance này còn có một secondary physical network với network accelerator cards được kết nối với top-of-rack (TOR) switches.

Đầu tiên trong danh mục này là các instance **bmn-sf2e**, được thiết kế cho độ trễ cực thấp với hiệu suất deterministic. Các instance mới chạy trên bộ xử lý Sapphire Rapids mới nhất của Intel (Xeon Scalable thế hệ thứ 4), mang lại hiệu suất duy trì 3.9 GHz trên tất cả các core với phân bổ memory hào phóng – 8GB RAM cho mỗi CPU core. Chúng tôi đã trang bị các instance bmn-sf2e với card mạng AMD Solarflare X2522 kết nối trực tiếp với top-of-rack switches.

Đối với khách hàng dịch vụ tài chính, đặc biệt là các công ty thị trường vốn, các instance này cung cấp networking deterministic thông qua Layer 2 (L2) multicast gốc, precision time protocol (PTP) và độ dài cáp bằng nhau. Điều này cho phép khách hàng đáp ứng các yêu cầu quy định về giao dịch công bằng và tiếp cận bình đẳng trong khi dễ dàng kết nối với cơ sở hạ tầng giao dịch hiện có của họ.

| Instance Name | vCPUs | Memory (DDR5) | Network Bandwidth | NVMe SSD Storage | Accelerated Network Cards | Accelerated Bandwidth (Gbps) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bmn-sf2e.metal-16xl | 64 | 512 GiB | 25 Gbps | 2 x 8 TB (16 TB) | 2 | 100 |
| bmn-sf2e.metal-32xl | 128 | 1024 GiB | 50 Gbps | 4 x 8 TB (32 TB) | 4 | 200 |

Loại instance thứ hai, **bmn-cx2**, được tối ưu hóa cho thông lượng cao và độ trễ thấp. Instance này có NVIDIA ConnectX-7 400G NIC được kết nối vật lý với top-of-rack switches tốc độ cao, mang lại băng thông mạng bare metal lên tới 800 Gbps hoạt động ở gần line rate. Với Layer 2 (L2) multicast gốc và hỗ trợ PTP phần cứng, instance này lý tưởng cho các workload thông lượng cao như phân phối dữ liệu thị trường thời gian thực, phân tích rủi ro và các ứng dụng mạng 5G core của viễn thông.

| Instance Name | vCPUs | Memory (DDR5) | Network Bandwidth | NVMe SSD Storage | Accelerated Network Cards | Accelerated Bandwidth (Gbps) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bmn-cx2.metal-48xl | 192 | 1024 GiB | 50 Gbps | 4 x 4 TB (16 TB) | 2 | 800 |

![Hình 2: Các instance chuyên biệt](/images/S2.jpg)
*Hình 2: Các instance chuyên biệt*

Tóm lại, thế hệ Outposts racks mới mang lại hiệu suất, khả năng mở rộng và khả năng phục hồi nâng cao cho nhiều loại workload tại chỗ, ngay cả đối với các workload mission-critical với các yêu cầu nghiêm ngặt nhất về độ trễ và thông lượng. Bạn có thể lựa chọn và bắt đầu đặt hàng từ AWS Management Console. Các instance mới duy trì tính nhất quán với các triển khai khu vực bằng cách hỗ trợ cùng các API, AWS Management Console, automation, governance policies và security controls trên cloud và tại chỗ, cải thiện năng suất của nhà phát triển và hiệu quả CNTT.

### Những điều cần biết

Khi ra mắt, Outposts racks thế hệ thứ hai có thể được vận chuyển đến Mỹ và Canada và được kết nối trở lại 6 AWS Regions bao gồm US East (N. Virginia và Ohio), US West (Oregon), EU West (London và France) và Asia Pacific (Singapore). Hỗ trợ cho nhiều quốc gia và vùng lãnh thổ cũng như AWS Regions sẽ sớm ra mắt. Khi ra mắt, Outposts racks thế hệ thứ hai hỗ trợ cục bộ một tập hợp con các dịch vụ AWS có trong Outposts racks thế hệ trước. Hỗ trợ cho nhiều loại instance EC2 và nhiều dịch vụ AWS sẽ sớm ra mắt.

Để tìm hiểu thêm, hãy truy cập trang sản phẩm AWS Outposts racks và hướng dẫn sử dụng. Bạn cũng có thể nói chuyện với chuyên gia Outposts nếu bạn sẵn sàng thảo luận về nhu cầu tại cơ sở của mình.

*1/5/2025: Dung lượng Memory (DDR5) được cập nhật trong bảng cho instance 48xl.*