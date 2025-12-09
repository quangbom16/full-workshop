---
title: "Prerequisites"
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Prerequisites

Before starting this workshop, ensure you have the following ready:

### 1. AWS Account
- Active AWS account with administrator access
- Recommended: Use a sandbox/development account
- Ensure you're in the **Asia Pacific (Singapore) ap-southeast-1** region

### 2. Required Tools

**Terraform** (version >= 1.0)
```bash
# Check installation
terraform version

# Download from: https://www.terraform.io/downloads
```

**AWS CLI** (version >= 2.0)
```bash
# Check installation
aws --version

# Configure credentials
aws configure
```

**Git**
```bash
# Clone the project
git clone https://github.com/Aohk22/fcj-1-file-analyzer.git
cd fcj-1-file-analyzer/terraform/envs/dev
```

### 3. AWS Credentials

Configure your AWS credentials:
```bash
aws configure
# AWS Access Key ID: [Your Access Key]
# AWS Secret Access Key: [Your Secret Key]
# Default region: ap-southeast-1
# Default output format: json
```

Or set environment variables:
```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_DEFAULT_REGION="ap-southeast-1"
```

### 4. Required IAM Permissions

Your AWS user/role needs permissions for:
- EC2 (create instances, security groups, launch templates)
- Auto Scaling (create ASGs, launch configurations)
- ELB (create ALB, target groups, listeners)
- VPC (create subnets, route tables, endpoints)
- IAM (create roles, policies)

### 5. Cost Considerations

**Estimated cost:** ~$5-10 for 20 minutes
- EC2 instances: t3.micro (included in free tier if eligible)
- ALB: ~$0.025/hour
- Data transfer: minimal

**Tip:** Ensure you complete the cleanup section to avoid unexpected charges!

### 6. Verify Setup

Run these commands to verify your setup:
```bash
# Check Terraform
terraform version

# Check AWS credentials
aws sts get-caller-identity

# Check region
aws configure get region
```
