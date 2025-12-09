---
title: "Translated Blogs"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

### [Blog 1 - Automating AWS Private CA audit reports and certificate expiration alerts](3.1-Blog1/)
This blog guides you through building an automated workflow to monitor and alert on the expiration of digital certificates issued by AWS Private CA. The solution leverages a combination of **EventBridge, Lambda, S3, SNS, and Security Hub** to generate daily audit reports. This allows administrators to proactively identify expiring certificates (including those created via API that are not automatically tracked by ACM), ensuring security compliance and preventing service disruptions.

### [Blog 2 - Announcing second-generation AWS Outposts racks with breakthrough performance](3.2-Blog2/)
This article announces the launch of the **second-generation AWS Outposts racks**, delivering breakthrough performance and scalability for on-premises environments. Key highlights include support for 7th generation EC2 instances (C7i, M7i, R7i) offering up to 40% better performance, a redesigned network architecture for simplified scaling, and the introduction of specialized instances designed for ultra-low latency and high throughput workloads (such as financial trading or 5G core networks).

### [Blog 3 - AWS Lambda standardizes billing for INIT Phase](3.3-Blog3/)
This blog announces a significant change in AWS pricing: Effective August 1, 2025, the initialization phase (INIT phase/cold start) will be billed for all Lambda function configurations. The content explains the Lambda execution lifecycle in detail, guides how to use CloudWatch to monitor INIT duration, and suggests cost optimization strategies such as using **Lambda SnapStart** or **Provisioned Concurrency** to minimize the impact of this change.