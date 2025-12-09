---
title: "Thiết Lập Hạ Tầng"
weight: 3
chapter: false
pre: " <b> 5.3 </b> "
---

## Thiết Lập Hạ Tầng

Trong phần này, bạn sẽ cấu hình và triển khai hạ tầng hoàn chỉnh cho ứng dụng file analyzer sử dụng Terraform. Quá trình bao gồm cấu hình variables, khởi tạo Terraform và triển khai tất cả tài nguyên AWS.

### Những Gì Sẽ Được Tạo

Cấu hình Terraform này sẽ cung cấp:

**Hạ Tầng Mạng:**
- VPC với CIDR block tùy chỉnh
- 2 Public subnets trên các availability zones
- 2 Private subnets trên các availability zones
- Internet Gateway và NAT Gateway
- Route tables và associations
- Cấu hình DNS

**Tài Nguyên Compute:**
- Application Load Balancer (ALB) với target groups
- Public Auto Scaling Group (min: 1, max: 3)
- Private Auto Scaling Group (min: 1, max: 3)
- Launch templates với user data scripts
- Health checks và scaling policies

**Dịch Vụ Hỗ Trợ:**
- Bảng DynamoDB cho application state
- Security groups cho ALB, public ASG và private ASG
- IAM roles và instance profiles cho EC2
- SSH key pair để truy cập instances

**CI/CD Pipeline (Image Builder):**
- EC2 Image Builder pipeline
- Tạo custom AMI với các dependencies của ứng dụng
- Quy trình refresh image tự động

### Cấu Trúc Terraform Module

Hạ tầng được tổ chức thành các thành phần modular:
- `networking.tf` - VPC, subnets, gateways, routes
- `security_groups.tf` - Quy tắc firewall cho từng tầng
- `services_load_balancer.tf` - Cấu hình ALB
- `services_groups.tf` - Auto Scaling Groups
- `launch_template.tf` - Cấu hình launch EC2
- `dynamodb.tf` - Thiết lập bảng DynamoDB
- `image_builder.tf` - Cấu hình pipeline AMI
- `dns.tf` - Cấu hình DNS và routing

### Thời Gian Ước Tính
⏱️ **10 phút**

### Tổng Quan Các Bước

1. **Cấu Hình Variables** - Đặt AWS region, instance types và capacity
2. **Khởi Tạo Terraform** - Tải AWS provider và validate cấu hình
3. **Triển Khai Hạ Tầng** - Tạo tất cả tài nguyên bằng một lệnh

{{% notice info %}}
💡 Tất cả tài nguyên sẽ được gắn tag `Environment: dev` và `ManagedBy: terraform` để dễ dàng xác định và theo dõi chi phí.
{{% /notice %}}

{{% notice warning %}}
⚠️ **Lưu ý:** Image Builder pipeline có thể mất thêm thời gian để tạo custom AMIs. Triển khai ban đầu sẽ sử dụng base AMI được chỉ định trong variables.
{{% /notice %}}

Hãy tiến hành cấu hình!
