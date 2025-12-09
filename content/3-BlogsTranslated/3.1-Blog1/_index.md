---
title: "Tự động hóa báo cáo kiểm tra AWS Private CA và cảnh báo hết hạn chứng chỉ"
date: "2025-06-10"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

*Bởi Santosh Vallurupalli và Manthan Raval*

- Bài viết gốc: <a href="https://aws.amazon.com/vi/blogs/security/automating-aws-private-ca-audit-reports-and-certificate-expiration-alerts/"
   target="_blank" 
   rel="noopener noreferrer">
   Automating AWS Private CA audit reports and certificate expiration alerts – AWS Security Blog
</a>

- doc: <a href="https://docs.google.com/document/d/1sNqRGmA-5V2XF_w0HN3yr571dA4DTM-j_EWXLFpXbFo/edit?usp=sharing"
   target="_blank" 
   rel="noopener noreferrer">
   GG docs
</a>

Các tổ chức ngày nay phụ thuộc rất nhiều vào các kênh liên lạc an toàn và đáng tin cậy, và chứng chỉ kỹ thuật số đóng vai trò quan trọng trong việc bảo mật cơ sở hạ tầng nội bộ và bên ngoài bằng cách thiết lập lòng tin và cho phép giao tiếp được mã hóa. Trong khi chứng chỉ công khai thường được sử dụng để bảo mật các ứng dụng internet, nhiều tổ chức lại ưa thích chứng chỉ riêng tư cho các tài nguyên nội bộ để duy trì tính bảo mật và cho phép các cấu hình tùy chỉnh mà chứng chỉ công khai không hỗ trợ.

**AWS Private CA** cung cấp một giải pháp toàn diện để tạo và quản lý hệ thống phân cấp chứng chỉ riêng tư trong cơ sở hạ tầng khóa công khai (PKI) của một tổ chức. AWS xử lý việc quản lý CA nặng nề, cho phép các tổ chức cấp chứng chỉ cho nhiều trường hợp sử dụng khác nhau, bao gồm tạo kênh liên lạc được mã hóa, xác thực máy khách và ký mã bằng mật mã.

Tuy nhiên, khi các khối lượng công việc phát triển — bao gồm các microservices gốc đám mây, môi trường container hóa và triển khai biên lai lai — các cấu hình chứng chỉ mặc định có thể không đáp ứng mọi nhu cầu. Ví dụ:
*   Chứng chỉ TLS riêng tư được yêu cầu bằng **AWS Certificate Manager (ACM)** đi kèm với thời gian hiệu lực cố định là **13 tháng**.
*   Các doanh nghiệp hiện đại có thể cần chứng chỉ tồn tại trong thời gian ngắn cho các container tạm thời hoặc chứng chỉ kéo dài cho hệ thống tại chỗ.

Bạn có thể tạo và cập nhật chứng chỉ thông qua **AWS CLI** hoặc **AWS SDK**. Tuy nhiên, ACM **không tự theo dõi** việc hết hạn của các chứng chỉ được cấp bằng API `acm-pca:IssueCertificate` và không được yêu cầu bằng ACM. Việc thiếu giám sát này có thể dẫn đến gián đoạn hoạt động.

Trong bài đăng này, chúng tôi sẽ hướng dẫn bạn quy trình tự động hóa tùy chỉnh tận dụng các báo cáo kiểm tra của AWS Private CA để chủ động giám sát việc hết hạn chứng chỉ bằng cách sử dụng **Amazon EventBridge, AWS Lambda, Amazon S3, Amazon SNS và AWS Security Hub**.

### Thách thức: Quản lý chứng chỉ ngoài các cài đặt mặc định

Các chứng chỉ được yêu cầu bằng ACM được cấp bởi CA riêng của bạn thông qua console mặc định có thời gian hiệu lực là 13 tháng. ACM theo dõi và tự động gia hạn chúng. Tuy nhiên, môi trường IT hiện đại có các yêu cầu đa dạng:

1.  **Chứng chỉ tồn tại trong thời gian ngắn:** Các môi trường container hóa (EKS, ECS) hoặc Service Mesh (Istio, Linkerd) thường dùng chứng chỉ có hiệu lực vài giờ hoặc vài ngày để giảm bề mặt tấn công.
2.  **Chứng chỉ tồn tại lâu dài:** Các hệ thống tại chỗ (on-premise), IoT hoặc môi trường hạn chế tài nguyên mạng có thể cần chứng chỉ nhiều năm để giảm gánh nặng quản trị.

Khi sử dụng AWS CLI/SDK để cấp chứng chỉ tùy chỉnh mà không nhập vào ACM, các chứng chỉ này sẽ không được theo dõi, không kích hoạt CloudWatch Logs và không được gia hạn tự động. Nếu không có chế độ xem tập trung, bạn phải tự giám sát ngày hết hạn thủ công.

### Điều kiện tiên quyết

Để thực hiện hướng dẫn này, bạn cần có:
*   Một tài khoản AWS.
*   Một CA riêng từ AWS Private CA.
*   Một chứng chỉ được tạo bên ngoài đã được nhập vào ACM (để thử nghiệm).

### Tổng quan giải pháp

Giải pháp này sử dụng các dịch vụ AWS để giám sát trạng thái chứng chỉ, phát hiện các trường hợp hết hạn sắp tới và thông báo cho quản trị viên, đồng thời tích hợp vào Security Hub.

**Kiến trúc:**
1.  **EventBridge Rule (`PCAReportRule`):** Kích hoạt theo lịch trình (ví dụ: hàng ngày).
2.  **Lambda 1 (`PCAauditReportLambdaGenerator`):** Gọi API để tạo báo cáo kiểm tra (audit report) và lưu vào S3.
3.  **S3 Bucket:** Lưu trữ báo cáo dưới dạng CSV.
4.  **Lambda 2 (`PCAAuditReportLambdaProcessor`):** Được kích hoạt bởi sự kiện `S3:PutObject`. Hàm này tải báo cáo, phân tích và tìm các chứng chỉ sắp hết hạn (ngưỡng mặc định 30 ngày).
5.  **Amazon SNS:** Gửi thông báo email cảnh báo.
6.  **AWS Security Hub:** Tạo các phát hiện (findings) để giám sát tập trung.

![Hình 1: Kiến trúc giải pháp](/images/F1.jpeg)
*Hình 1: Kiến trúc giải pháp*

### Triển khai giải pháp

#### 1. Triển khai mẫu CloudFormation

Để bắt đầu, hãy tải xuống mẫu CloudFormation:

```bash
curl -O https://aws-security-blog-content.s3.us-east-1.amazonaws.com/public/sample/2526-monitor-private-ca-issued-certificates-aws-private-certificate-authority-eventbridge/ACM-PCA-Monitoring-cfn.yml
```

Mẫu `ACM-PCA-Monitoring-cfn.yml` bao gồm các tham số tùy chỉnh như `CertificateAuthorityArn`, `S3BucketName`, `CronJobExpression`, `SNSName`, `EmailAddress`, và `CertificateExpirationThreshold`.

Chạy lệnh sau để tạo stack (thay thế các giá trị trong ngoặc `<...>` bằng thông tin của bạn):

```bash
aws cloudformation create-stack \
--stack-name PCAMonitoringWorkflow \
--template-body file://ACM-PCA-Monitoring-cfn.yml \
--capabilities CAPABILITY_NAMED_IAM \
--parameters '[
    {"ParameterKey": "CertificateAuthorityArn", "ParameterValue": "<ARN_of_your_PrivateCA>"},
    {"ParameterKey": "S3BucketName", "ParameterValue": "<Name_of_s3_bucket>"},
    {"ParameterKey": "EventBridgeRuleName", "ParameterValue": "<Name_of_EventBridgeRule>"},
    {"ParameterKey": "CronJobExpression", "ParameterValue": "cron(0 21 * * ? *)"},
    {"ParameterKey": "SNSName", "ParameterValue": "PCASNSTopic"},
    {"ParameterKey": "SQSName", "ParameterValue": "PCASQS"},
    {"ParameterKey": "EmailAddress", "ParameterValue": "<Email_to_Receive_alerts>"},
    {"ParameterKey": "CertificateExpirationThreshold", "ParameterValue": "30"}
]'
```

Sau khi tạo stack, hãy kiểm tra email để xác nhận đăng ký SNS.

![Hình 2: Email thông báo mẫu được gửi bởi Amazon SNS](/images/F2.png)
*Hình 2: Email xác nhận đăng ký SNS*

#### 2. Kiểm tra quy trình tự động hóa

Tạo một chứng chỉ thử nghiệm có thời hạn ngắn (ví dụ: 20 ngày) để kích hoạt cảnh báo (vì ngưỡng mặc định là 30 ngày).

```bash
# Generate a Private Key
openssl genrsa -out private-key.pem 2048

# Generate a Certificate Signing Request (CSR)
openssl req -new -key private-key.pem -out csr.pem -subj "/C=US/ST=Ohio/L=Columbus/O=MyOrg/OU=IT/CN=mydomain.com"

# Issue a Certificate (valid for 20 days)
aws acm-pca issue-certificate \
--certificate-authority-arn <specify_arn_of_PrivateCA> \
--csr "$(cat csr.pem | base64 | tr -d '\n')" \
--signing-algorithm "SHA256WITHRSA" \
--validity Value=20,Type="DAYS"
```

Lưu lại `CertificateArn` từ kết quả đầu ra, sau đó lấy chứng chỉ về:

```bash
aws acm-pca get-certificate \
--certificate-authority-arn <specify_arn_of_PrivateCA> \
--certificate-arn <specify_arn_of_Certificate_generated_above> \
--output text > certificate.pem
```

#### 3. Chạy báo cáo kiểm tra theo yêu cầu

Bạn có thể đợi lịch trình Cron chạy hoặc kích hoạt thủ công để kiểm tra ngay lập tức.

**Cách 1: Chỉnh sửa EventBridge Rule**
Vào console EventBridge -> Rules -> Chọn `PCAReportRule` -> Edit -> Chuyển lịch trình sang chạy mỗi 30 phút để test -> Sau đó hoàn nguyên lại.

![Hình 3: Chỉnh sửa lịch trình của PCAReportRule](/images/F3.png)
*Hình 3: Chỉnh sửa lịch trình của PCAReportRule để kiểm tra*

**Cách 2: Kích hoạt từ Lambda Console**
Vào console Lambda -> Chọn hàm `PCAauditReportLambdaGenerator` -> Tab **Test** -> Nhấn nút **Test**.

![Hình 4: Sử dụng console để kích hoạt kiểm tra](/images/F4.jpeg)
*Hình 4: Sử dụng console để kích hoạt kiểm tra*

#### 4. Xác minh kết quả

**Kiểm tra S3 Bucket:**
Báo cáo kiểm tra sẽ được tạo trong thư mục `audit-report` của bucket bạn đã chỉ định.

![Hình 5: Báo cáo kiểm tra được lưu vào S3](/images/F5.jpeg)
*Hình 5: Báo cáo kiểm tra được lưu vào S3 bucket được chỉ định*

**Kiểm tra Security Hub:**
Vì chứng chỉ thử nghiệm hết hạn trong 20 ngày (dưới ngưỡng 30 ngày), Security Hub sẽ hiển thị Findings.

![Hình 6: Xem các phát hiện báo cáo kiểm tra trong Security Hub](/images/F6.jpeg)
*Hình 6: Xem các phát hiện báo cáo kiểm tra trong Security Hub*

**Kiểm tra Email (SNS):**
Bạn sẽ nhận được email cảnh báo chi tiết về chứng chỉ sắp hết hạn.

![Hình 7: Email thông báo mẫu](/images/F7.png)
*Hình 7: Email thông báo mẫu được gửi bởi Amazon SNS*

### Kết luận

Giải pháp này biến đổi việc quản lý chứng chỉ truyền thống từ một quy trình thủ công, dễ xảy ra lỗi thành một quy trình tự động. Bằng cách triển khai mẫu CloudFormation này, bạn có thể:

*   Tự động hóa việc tạo và xử lý các báo cáo kiểm tra AWS Private CA.
*   Nhận thông báo tức thì khi chứng chỉ sắp hết hạn.
*   Duy trì khả năng hiển thị tập trung thông qua Security Hub.
*   Giảm thiểu rủi ro gián đoạn dịch vụ do chứng chỉ hết hạn.

Hệ thống có khả năng mở rộng này giúp đơn giản hóa việc quản lý chứng chỉ và tăng cường tư thế bảo mật tổng thể của tổ chức bạn.