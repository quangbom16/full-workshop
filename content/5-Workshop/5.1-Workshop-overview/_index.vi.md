---
title: "Tổng Quan Workshop"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Workshop: Triển Khai Hạ Tầng File Analyzer với Terraform

### Giới Thiệu

Trong workshop thực hành này, bạn sẽ triển khai một hạ tầng hoàn chỉnh cho ứng dụng phân tích file trên AWS sử dụng Terraform. Hạ tầng bao gồm auto-scaling groups, load balancers, VPC endpoints và tích hợp S3 - tất cả được cung cấp dưới dạng Infrastructure as Code.

### Tổng Quan Kiến Trúc

Hạ tầng bao gồm:
- **VPC** với public và private subnets trên 2 availability zones
- **Application Load Balancer (ALB)** để phân phối traffic
- **2 Auto Scaling Groups**:
  - Public ASG: Tầng frontend/web
  - Private ASG: Tầng backend/xử lý
- **S3 Gateway Endpoint** để truy cập S3 an toàn
- **Security Groups** để cô lập mạng
- **IAM Roles** cho quyền EC2

### Bạn Sẽ Học Được

- Khởi tạo và cấu hình Terraform cho AWS
- Triển khai hạ tầng đa tầng sử dụng Terraform modules
- Cấu hình auto-scaling groups và load balancers
- Thiết lập VPC endpoints để truy cập dịch vụ AWS an toàn
- Xác minh và kiểm tra hạ tầng đã triển khai
- Dọn dẹp tài nguyên hiệu quả

### Thời Gian Cần Thiết

**Thời lượng ước tính:** 20 phút

### Quy Trình Workshop

1. **Yêu Cầu Tiên Quyết** (2 phút) - Thiết lập công cụ và credentials
2. **Thiết Lập Hạ Tầng** (10 phút) - Cấu hình và triển khai
3. **Xác Minh** (5 phút) - Kiểm tra ứng dụng
4. **Dọn Dẹp** (3 phút) - Xóa tất cả tài nguyên
