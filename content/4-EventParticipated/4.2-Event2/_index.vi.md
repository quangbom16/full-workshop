---
title: "Sự kiện: Workshop DevOps trên AWS"
date: "2025-11-17"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

## Báo cáo tổng kết: "Workshop DevOps trên AWS"

### Mục tiêu sự kiện

- Thấm nhuần văn hóa và tư duy DevOps, tập trung vào các chỉ số hiệu suất chính (DORA).
- Làm chủ bộ công cụ AWS Developer Tools để xây dựng các pipeline CI/CD tự động hoàn toàn.
- Hiểu về Cơ sở hạ tầng dưới dạng mã (IaC) sử dụng CloudFormation và AWS CDK.
- Khám phá các chiến lược container hóa trên AWS (ECS, EKS, App Runner).
- Triển khai giám sát và khả năng quan sát (observability) toàn diện bằng CloudWatch và X-Ray.

### Diễn giả

- **Các chuyên gia DevOps của AWS & Lãnh đạo cộng đồng**

### Điểm nổi bật chính

#### Tư duy & Văn hóa DevOps

- **Chuyển đổi văn hóa**: Chuyển từ phát triển và vận hành tách biệt sang một văn hóa thống nhất.
- **Các chỉ số quan trọng**: Đi sâu vào các chỉ số DORA (Tần suất triển khai, Thời gian thay đổi, Thời gian khôi phục dịch vụ, Tỷ lệ lỗi khi thay đổi) để đo lường thành công.

#### Dịch vụ AWS DevOps – Quy trình CI/CD

**Source & Build**
- **AWS CodeCommit**: Quản lý kho lưu trữ Git an toàn và so sánh chiến lược GitFlow vs. Trunk-based.
- **AWS CodeBuild**: Cấu hình môi trường build và tích hợp kiểm thử tự động.

**Triển khai & Điều phối**
- **Chiến lược triển khai**: Phân tích chi tiết các cập nhật **Blue/Green** (không downtime), **Canary** (giảm thiểu rủi ro), và **Rolling** sử dụng AWS CodeDeploy.
- **AWS CodePipeline**: Điều phối toàn bộ quy trình phát hành từ khi commit code đến môi trường production.

#### Cơ sở hạ tầng dưới dạng mã (IaC)

- **CloudFormation**: Định nghĩa cơ sở hạ tầng bằng các mẫu JSON/YAML và quản lý phát hiện sai lệch (drift detection).
- **AWS CDK**: Sức mạnh của việc định nghĩa hạ tầng bằng ngôn ngữ lập trình quen thuộc (TypeScript, Python) và sử dụng các construct để tái sử dụng.
- **So sánh**: Thảo luận khi nào nên dùng mẫu khai báo (CFN) so với mã mệnh lệnh (CDK).

#### Dịch vụ Container trên AWS

- **Registry**: Bảo mật image với Amazon ECR và các chính sách vòng đời (lifecycle policies).
- **Lựa chọn điều phối**:
    - **Amazon ECS**: Tích hợp sâu với AWS và đơn giản.
    - **Amazon EKS**: Dành cho các workload Kubernetes thuần túy và tính di động cao.
    - **AWS App Runner**: Triển khai nhanh ứng dụng web container mà không cần quản lý hạ tầng.

#### Giám sát & Khả năng quan sát (Observability)

- **Tầm nhìn toàn diện**: Vượt ra ngoài các chỉ số đơn giản để tiến tới truy vết phân tán (distributed tracing) với **AWS X-Ray**.
- **CloudWatch**: Thiết lập các cảnh báo tổng hợp và dashboard để chủ động quản lý sức khỏe hệ thống.

### Bài học chính (Key Takeaways)

#### Tự động hóa là tất cả

- **Pipeline First**: Mọi dự án nên bắt đầu bằng một pipeline. Triển khai thủ công là một rủi ro lớn.
- **Hạ tầng bất biến (Immutable Infrastructure)**: Server không nên được vá lỗi trực tiếp; chúng nên được thay thế thông qua quy trình triển khai tự động.

#### Sức mạnh của IaC

- **Quản lý phiên bản hạ tầng**: Coi định nghĩa hạ tầng giống hệt như mã ứng dụng cho phép rollback, review code và đảm bảo tính nhất quán giữa các môi trường.
- **Hiệu quả của CDK**: Sử dụng AWS CDK giúp tăng tốc độ phát triển đáng kể bằng cách giảm bớt lượng code lặp lại so với CloudFormation thuần túy.

#### Sự xuất sắc trong vận hành

- **Observability**: Không chỉ là biết hệ thống *có* chết hay không, mà là *tại sao*. Truy vết phân tán là thiết yếu cho microservices.
- **An toàn khi triển khai**: Luôn sử dụng các chiến lược như Canary hoặc Blue/Green để giảm thiểu phạm vi ảnh hưởng khi cập nhật.

### Ứng dụng vào công việc

- **Rà soát Pipeline hiện tại**: Đánh giá quy trình CI/CD hiện có và bắt đầu theo dõi các chỉ số DORA.
- **Áp dụng IaC**: Bắt đầu di chuyển các tài nguyên được tạo thủ công sang AWS CDK hoặc CloudFormation stacks.
- **Container hóa ứng dụng cũ**: Đánh giá các ứng dụng nguyên khối (monolithic) để di chuyển sang Amazon ECS hoặc App Runner.
- **Nâng cao giám sát**: Triển khai AWS X-Ray cho các microservices quan trọng để xác định điểm nghẽn hiệu năng.

### Trải nghiệm sự kiện

Buổi **"Workshop DevOps trên AWS"** là một ngày học tập chuyên sâu, kết nối các nguyên lý DevOps lý thuyết với việc triển khai thực tế trên AWS.

- **Phiên buổi sáng** về CI/CD đã làm rõ các trường hợp sử dụng cụ thể cho từng dịch vụ AWS Code*. Bản demo pipeline đầy đủ cho thấy sự tích hợp liền mạch giữa các công cụ.
- **Thảo luận về IaC** là điểm nhấn. Việc nhìn thấy lượng code giảm đi khi chuyển từ CloudFormation sang **AWS CDK** là bằng chứng thuyết phục để áp dụng CDK cho các dự án tương lai.
- **Phiên buổi chiều** về container cung cấp một ma trận quyết định rõ ràng để lựa chọn giữa **ECS, EKS và App Runner**, vốn là một chủ đề thường gây bối rối.
- Phần **Observability** nhấn mạnh rằng giám sát là một kỷ luật kỹ thuật chủ động, không chỉ là công việc hỗ trợ phản ứng khi có sự cố.

Nhìn chung, workshop này đã cung cấp bộ công cụ kỹ thuật cần thiết để tăng tốc độ phân phối phần mềm trong khi vẫn duy trì sự ổn định và bảo mật trên đám mây AWS.