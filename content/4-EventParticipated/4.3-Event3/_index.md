---
title: "Event 3: AWS Well-Architected Security Pillar Workshop"
date: "2025-11-29"
weight: 3
chapter: false
pre: " <b> 4.3. </b> "
---

## Summary Report: "AWS Well-Architected Security Pillar"

### Event Objectives

- Deep dive into the Security Pillar of the AWS Well-Architected Framework.
- Understand the core security principles: Least Privilege, Zero Trust, and Defense in Depth.
- Analyze the top cloud security threats specifically within the Vietnamese market.
- Master the 5 key security domains: IAM, Detection, Infrastructure Protection, Data Protection, and Incident Response.
- Learn practical automation for security using Lambda and Step Functions.

### Speakers

- **AWS Security Solutions Architects**

### Key Highlights

#### Opening & Security Foundation

- **Core Principles**: Re-emphasizing **Least Privilege**, **Zero Trust**, and **Defense in Depth** as the non-negotiable foundations of any cloud architecture.
- **Shared Responsibility Model**: Clarifying the boundary between AWS's security of the cloud and the customer's security in the cloud.
- **Local Context**: Discussion on the top cybersecurity threats facing Vietnamese enterprises today.

#### Pillar 1: Identity & Access Management (IAM)

- **Modern Architecture**: Moving away from long-term IAM User credentials towards temporary credentials and **IAM Identity Center** (SSO).
- **Control Mechanisms**: Using **Service Control Policies (SCPs)** for multi-account governance and setting permission boundaries.
- **Mini Demo**: Validating IAM Policies and simulating access to ensure least privilege is actually enforced.

#### Pillar 2: Detection

- **Continuous Monitoring**: Enabling **CloudTrail** at the organization level and centralizing findings with **AWS Security Hub** and **Amazon GuardDuty**.
- **Logging Strategy**: Importance of capturing logs at every layer (VPC Flow Logs, ALB, S3).
- **Detection-as-Code**: Automating alerting using Amazon EventBridge to react to security events in real-time.

#### Pillar 3: Infrastructure Protection

- **Network Security**: Implementing strict VPC segmentation and understanding the correct placement of public vs. private resources.
- **Defense Layers**: The correct model for applying Security Groups (stateful) vs. NACLs (stateless), and layering **AWS WAF** and **Shield** for edge protection.

#### Pillar 4: Data Protection

- **Encryption Strategy**: Comprehensive use of **AWS KMS** for key management, rotation, and enforcing encryption at-rest (EBS, S3, RDS) and in-transit.
- **Secrets Management**: Patterns for rotating database credentials using **AWS Secrets Manager** to eliminate hardcoded secrets in code.

#### Pillar 5: Incident Response (IR)

- **IR Lifecycle**: Preparation, Detection, Containment, Eradication, Recovery, and Post-Incident Activity.
- **Playbooks**: Walkthrough of specific scenarios:
    - Handling a compromised IAM Access Key.
    - Reacting to accidental S3 public exposure.
    - Isolating EC2 instances infected with malware.
- **Automation**: Using Lambda and Step Functions to auto-remediate simple threats.

### Key Takeaways

#### Zero Trust is a Journey

- **Identity is the new perimeter**: In the cloud, network perimeters are porous; identity controls (IAM) are the primary defense.
- **Eliminate long-term keys**: Static access keys are the #1 vector for account compromise.

#### Defense in Depth

- **Layered Security**: Never rely on a single control. Use WAF at the edge, Security Groups at the instance, and Encryption at the data layer.
- **Encryption is standard**: Encryption should be the default state for all data, not an optional feature.

#### Automate Response

- **Speed matters**: In a security incident, manual response is too slow. Automated playbooks (e.g., auto-revoking a compromised key) save the day.
- **Practice IR**: You cannot figure out your Incident Response plan during an actual attack. Game days are essential.

### Applying to Work

- **Audit IAM**: Immediately review and remove unused IAM users/keys and enable MFA for everyone.
- **Enable GuardDuty**: Turn on GuardDuty in all regions to detect anomalous behavior.
- **Review Secrets**: Migrate hardcoded API keys/passwords from code to AWS Secrets Manager.
- **Define Playbooks**: Write down the exact steps the team must take if an S3 bucket is found public or a server is compromised.

### Event Experience

The **"AWS Well-Architected Security Pillar"** workshop was a dense, high-impact session that highlighted the critical importance of security in every stage of the cloud journey.

- The **"Vietnam Threat Landscape"** segment was particularly eye-opening, showing that local businesses are often targeted due to misconfigured S3 buckets and exposed IAM keys.
- The **IAM Mini Demo** provided a practical way to verify permissions, which I can immediately apply to my current project to tighten security.
- The **Incident Response** section was the most valuable, as it moved beyond theory into actionable playbooks. Learning how to automate the isolation of a compromised EC2 instance using Lambda was a highlight.

Overall, the session reinforced that security is not just the job of the security team, but a fundamental responsibility of every cloud builder.