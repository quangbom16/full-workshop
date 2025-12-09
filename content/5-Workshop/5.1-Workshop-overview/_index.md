---
title: "Workshop Overview"
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Workshop: Deploy File Analyzer Infrastructure with Terraform

### Introduction

In this hands-on workshop, you will deploy a complete file analyzer application infrastructure on AWS using Terraform. The infrastructure includes auto-scaling groups, load balancers, VPC endpoints, and S3 integration - all provisioned as Infrastructure as Code.

### Architecture Overview

The infrastructure consists of:
- **VPC** with public and private subnets across 2 availability zones
- **Application Load Balancer (ALB)** for traffic distribution
- **2 Auto Scaling Groups**:
  - Public ASG: Frontend/web tier
  - Private ASG: Backend/processing tier
- **S3 Gateway Endpoint** for secure S3 access
- **Security Groups** for network isolation
- **IAM Roles** for EC2 permissions

### What You'll Learn

- Initialize and configure Terraform for AWS
- Deploy multi-tier infrastructure using Terraform modules
- Configure auto-scaling groups and load balancers
- Set up VPC endpoints for secure AWS service access
- Verify and test deployed infrastructure
- Clean up resources efficiently

### Time Required

**Estimated Duration:** 20 minutes

### Workshop Flow

1. **Prerequisites** (2 minutes) - Setup tools and credentials
2. **Infrastructure Setup** (10 minutes) - Configure and deploy
3. **Verification** (5 minutes) - Test the application
4. **Cleanup** (3 minutes) - Remove all resources
