---
title: "Week 3 Worklog"
date: "2025-09-22"
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
--- 


### Week 3 Objectives:

* Master the core components of Amazon VPC (Virtual Private Cloud).
* Implement network security using Security Groups and Network ACLs.
* Deploy EC2 instances within a custom network architecture.
* Understand Hybrid Connectivity via Site-to-Site VPN.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - **Introduction to VPC Networking:** <br> - Understand CIDR blocks <br> - **1.1 Subnets:** Public vs. Private <br> - **1.2 Route Tables:** Associations and Route propagation <br> - **1.3 Internet Gateway (IGW):** Enabling internet access | 09/22/2025 | 09/26/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 3   | - **Advanced Networking & Firewall:** <br> - **1.4 NAT Gateway:** Outbound internet for private subnets <br> - **2. Firewall in VPC:** <br>&emsp; + Security Groups (Stateful) <br>&emsp; + Network ACLs (Stateless) | 09/22/2025 | 09/26/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - **3. Preparation Steps:** Planning VPC design (IP addressing) <br> - **4. Deploying Amazon EC2 Instances:** <br>&emsp; + Create a custom VPC <br>&emsp; + Launch EC2 in Public Subnet <br>&emsp; + Launch EC2 in Private Subnet | 09/22/2025 | 09/26/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - **5. Setting Up Site-to-Site VPN Connection:** <br> - Understand Virtual Private Gateway (VGW) & Customer Gateway (CGW) <br> - Learn VPN configuration steps <br> - **Practice:** Configure the AWS side of a VPN connection | 09/22/2025 | 09/26/2025      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - **Review & Troubleshooting:** <br> - Test connectivity between instances (Ping, SSH) <br> - Verify Security Group rules <br> - Troubleshoot common VPC connection issues                               | 09/22/2025 | 09/26/2025      | <https://cloudjourney.awsstudygroup.com/> |


### Week 3 Achievements:

* Designed and created a custom Virtual Private Cloud (VPC) with proper CIDR block planning.

* Successfully configured network components:
  * Public and Private Subnets.
  * Route Tables for traffic direction.
  * Internet Gateway for public access and NAT Gateway for private subnet updates.

* Secured the network layers by implementing Security Groups (Instance level) and Network ACLs (Subnet level).

* Deployed EC2 instances into the custom network and verified internal/external connectivity.

* Gained theoretical and practical knowledge on establishing a Site-to-Site VPN connection between AWS and on-premises environments.