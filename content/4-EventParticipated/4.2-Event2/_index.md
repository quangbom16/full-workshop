---
title: "Event 2: DevOps on AWS Workshop"
date: "2025-11-17"
weight: 2
chapter: false
pre: " <b> 4.2. </b> "
---

## Summary Report: "DevOps on AWS Workshop"

### Event Objectives

- Instill the DevOps culture and mindset, focusing on key performance metrics (DORA).
- Master the AWS Developer Tools suite to build fully automated CI/CD pipelines.
- Understand Infrastructure as Code (IaC) using CloudFormation and AWS CDK.
- Explore containerization strategies on AWS (ECS, EKS, App Runner).
- Implement comprehensive monitoring and observability using CloudWatch and X-Ray.

### Speakers

- **AWS DevOps Specialists & Community Leaders**

### Key Highlights

#### DevOps Mindset & Culture

- **Cultural Shift**: Moving from siloed development and operations to a unified culture.
- **Metrics that Matter**: Deep dive into DORA metrics (Deployment Frequency, Lead Time for Changes, Time to Restore Service, Change Failure Rate) to measure success.

#### AWS DevOps Services – CI/CD Pipeline

**Source & Build**
- **AWS CodeCommit**: Managing secure Git repositories and comparing GitFlow vs. Trunk-based development strategies.
- **AWS CodeBuild**: configuring build environments and integrating automated testing.

**Deployment & Orchestration**
- **Deployment Strategies**: Detailed breakdown of **Blue/Green** (zero downtime), **Canary** (risk mitigation), and **Rolling** updates using AWS CodeDeploy.
- **AWS CodePipeline**: Orchestrating the entire release process from commit to production.

#### Infrastructure as Code (IaC)

- **CloudFormation**: Defining infrastructure using JSON/YAML templates and managing drift detection.
- **AWS CDK**: The power of defining infrastructure using familiar programming languages (TypeScript, Python) and using constructs for reusable patterns.
- **Comparison**: Discussion on when to use declarative templates (CFN) versus imperative code (CDK).

#### Container Services on AWS

- **Registry**: Securing images with Amazon ECR and lifecycle policies.
- **Orchestration Choices**:
    - **Amazon ECS**: For deep AWS integration and simplicity.
    - **Amazon EKS**: For Kubernetes-native workloads and portability.
    - **AWS App Runner**: For rapid deployment of containerized web apps without managing infrastructure.

#### Monitoring & Observability

- **Full-Stack Visibility**: Moving beyond simple metrics to distributed tracing with **AWS X-Ray**.
- **CloudWatch**: Setting up composite alarms and dashboards to proactively manage system health.

### Key Takeaways

#### Automation is Everything

- **Pipeline First**: Every project should start with a pipeline. Manual deployments are a risk.
- **Immutable Infrastructure**: Servers should not be patched in place; they should be replaced via automated deployments.

#### The Power of IaC

- **Version Control Infrastructure**: Treating infrastructure definitions exactly like application code allows for rollbacks, reviews, and consistency across environments.
- **CDK Efficiency**: Using AWS CDK significantly speeds up development by reducing boilerplate code compared to raw CloudFormation.

#### Operational Excellence

- **Observability**: It’s not just about knowing *if* the system is down, but *why*. Distributed tracing is essential for microservices.
- **Deployment Safety**: Always use deployment strategies like Canary or Blue/Green to minimize blast radius during updates.

### Applying to Work

- **Audit Current Pipelines**: Review existing CI/CD processes and implement DORA metrics tracking.
- **Adopt IaC**: Begin migrating manually created resources to AWS CDK or CloudFormation stacks.
- **Containerize Legacy Apps**: Evaluate monolithic applications for migration to Amazon ECS or App Runner.
- **Enhance Monitoring**: Implement AWS X-Ray for critical microservices to identify performance bottlenecks.

### Event Experience

The **"DevOps on AWS Workshop"** was an intensive, full-day deep dive that connected the dots between theoretical DevOps principles and practical AWS implementation.

- The **morning session** on CI/CD cleared up the specific use cases for each AWS Code* service. The demo of a full pipeline showed how seamless the integration is.
- The **IaC discussion** was a highlight. Seeing the code reduction when switching from CloudFormation templates to **AWS CDK** constructs was convincing evidence to adopt CDK for future projects.
- The **afternoon session** on containers provided a clear decision matrix for choosing between **ECS, EKS, and App Runner**, which is often a confusing topic.
- The **Observability** segment emphasized that monitoring is a proactive engineering discipline, not just a reactive support task.

Overall, this workshop provided the technical toolkit necessary to accelerate software delivery while maintaining stability and security on the AWS cloud.