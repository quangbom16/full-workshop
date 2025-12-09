---
title: "Infrastructure Setup"
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Infrastructure Setup

In this section, you will configure and deploy the complete file analyzer infrastructure using Terraform. The process involves configuring variables, initializing Terraform, and deploying all AWS resources.

### What Will Be Created

This Terraform configuration will provision:

**Network Infrastructure:**
- VPC with custom CIDR block
- 2 Public subnets across availability zones
- 2 Private subnets across availability zones
- Internet Gateway and NAT Gateway
- Route tables and associations
- DNS configuration

**Compute Resources:**
- Application Load Balancer (ALB) with target groups
- Public Auto Scaling Group (min: 1, max: 3)
- Private Auto Scaling Group (min: 1, max: 3)
- Launch templates with user data scripts
- Health checks and scaling policies

**Supporting Services:**
- DynamoDB table for application state
- Security groups for ALB, public ASG, and private ASG
- IAM roles and instance profiles for EC2
- SSH key pair for instance access

**CI/CD Pipeline (Image Builder):**
- EC2 Image Builder pipeline
- Custom AMI creation with application dependencies
- Automated image refresh workflow

### Terraform Module Structure

The infrastructure is organized into modular components:
- `networking.tf` - VPC, subnets, gateways, routes
- `security_groups.tf` - Firewall rules for each tier
- `services_load_balancer.tf` - ALB configuration
- `services_groups.tf` - Auto Scaling Groups
- `launch_template.tf` - EC2 launch configurations
- `dynamodb.tf` - DynamoDB table setup
- `image_builder.tf` - AMI pipeline configuration
- `dns.tf` - DNS and routing configuration

### Estimated Time
⏱️ **10 minutes**

### Steps Overview

1. **Configure Variables** - Set AWS region, instance types, and capacity
2. **Initialize Terraform** - Download AWS provider and validate configuration
3. **Deploy Infrastructure** - Create all resources with single command

{{% notice info %}}
💡 All resources will be tagged with `Environment: dev` and `ManagedBy: terraform` for easy identification and cost tracking.
{{% /notice %}}

{{% notice warning %}}
⚠️ **Note:** The Image Builder pipeline may take additional time to create custom AMIs. The initial deployment will use the base AMI specified in variables.
{{% /notice %}}

Let's proceed with the configuration!
