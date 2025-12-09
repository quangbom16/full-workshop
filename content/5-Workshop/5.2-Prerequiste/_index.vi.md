---
title: "Yêu Cầu Tiên Quyết"
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Yêu Cầu Tiên Quyết

Trước khi bắt đầu workshop này, hãy đảm bảo bạn đã chuẩn bị:

### 1. AWS Account
- Tài khoản AWS đang hoạt động với quyền administrator
- Khuyến nghị: Sử dụng tài khoản sandbox/development
- Đảm bảo bạn đang ở region **Asia Pacific (Singapore) ap-southeast-1**

### 2. Công Cụ Cần Thiết

**Terraform** (phiên bản >= 1.0)
```bash
# Kiểm tra cài đặt
terraform version

# Tải về từ: https://www.terraform.io/downloads
```

**AWS CLI** (phiên bản >= 2.0)
```bash
# Kiểm tra cài đặt
aws --version

# Cấu hình credentials
aws configure
```

**Git**
```bash
# Clone dự án
git clone https://github.com/Aohk22/fcj-1-file-analyzer.git
cd fcj-1-file-analyzer/terraform/envs/dev
```

### 3. AWS Credentials

Cấu hình AWS credentials của bạn:
```bash
aws configure
# AWS Access Key ID: [Access Key của bạn]
# AWS Secret Access Key: [Secret Key của bạn]
# Default region: ap-southeast-1
# Default output format: json
```

Hoặc thiết lập biến môi trường:
```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="ap-southeast-1"
```

### 4. Quyền IAM Cần Thiết

AWS user/role của bạn cần quyền cho:
- EC2 (tạo instances, security groups, launch templates)
- Auto Scaling (tạo ASGs, launch configurations)
- ELB (tạo ALB, target groups, listeners)
- VPC (tạo subnets, route tables, endpoints)
- IAM (tạo roles, policies)

### 5. Chi Phí Ước Tính

**Chi phí ước tính:** ~$5-10 cho 20 phút
- EC2 instances: t3.micro (miễn phí nếu đủ điều kiện free tier)
- ALB: ~$0.025/giờ
- Data transfer: tối thiểu

**Mẹo:** Đảm bảo bạn hoàn thành phần cleanup để tránh phí phát sinh ngoài ý muốn!

### 6. Xác Minh Thiết Lập

Chạy các lệnh sau để xác minh thiết lập của bạn:
```bash
# Kiểm tra Terraform
terraform version

# Kiểm tra AWS credentials
aws sts get-caller-identity

# Kiểm tra region
aws configure get region
```
