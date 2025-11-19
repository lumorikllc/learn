---
layout: textbook
title: "AWS Architect Accelerator: 30-Day Plan for Working Professionals - Understand IaaS, PaaS, SaaS and shared responsibility model"
date: 2025-11-19T02:20:18.810111
study_plan_url: "https://lumorikllc.github.io/learn/content/00000000-0000-0000-0000-000000000000/1eda3473-bcb3-43c1-90f1-968c9d998089/"
chapters: 8
author: "00000000-0000-0000-0000-000000000000"
description: "AI-generated textbook by Lumorik"
---

## Chapter Overview
Cloud computing transforms how organizations deploy and manage IT resources. Understanding service models and the Shared Responsibility Model is crucial for designing secure, cost-effective architectures on AWS.

Learning goals  
- Describe and differentiate IaaS, PaaS, and SaaS models  
- Explain AWS’s Shared Responsibility Model and delineate customer/provider duties  
- Classify common AWS services by service model and responsibility boundary  

## Key Concepts & Definitions
**IaaS (Infrastructure as a Service)**: On-demand computing resources (VMs, storage, networks) managed by the provider.  
**PaaS (Platform as a Service)**: Managed runtime environments where customers deploy applications without handling underlying infrastructure.  
**SaaS (Software as a Service)**: Fully managed applications delivered over the Internet, requiring no customer maintenance of platform or infrastructure.  
**Shared Responsibility Model**: Framework dividing security and compliance tasks between AWS (provider) and the customer.  
**Customer Responsibility**: Tasks such as data protection, OS patching, application security.  
**Provider Responsibility**: Tasks such as physical infrastructure, virtualization layer, and managed platform uptime.  

These concepts form a stack: as you move from IaaS → PaaS → SaaS, AWS takes on a larger share of operational duties. The Shared Responsibility Model overlays this stack, clarifying who secures which layers.

## Main Exposition

### 3.1 Service Models Explained
- **IaaS** offers raw compute, storage, and networking. You provision EC2 instances, attach EBS volumes, configure security groups, and manage the OS and applications.  
- **PaaS** abstracts infrastructure management. For example, AWS Elastic Beanstalk handles provisioning and scaling while you deploy code; Amazon RDS manages database engines, backups, and patching.  
- **SaaS** delivers end-user applications such as Salesforce or Amazon WorkDocs. You simply configure users and settings—no OS, middleware, or infrastructure to manage.

### 3.2 AWS Shared Responsibility Model
AWS categorizes responsibilities into two domains:

- **Security “of” the Cloud (AWS)**: Physical facilities, hardware, network, virtualization layer.  
- **Security “in” the Cloud (Customer)**: Guest OS, applications, data, identity management, network traffic protection.

Logical layers:
> Physical → Network → Hypervisor → OS → Middleware → Application → Data

AWS secures everything up to the hypervisor; you secure the rest.

### 3.3 Mapping AWS Services to Models & Duties
- **Amazon EC2 (IaaS)**  
  - AWS: Hypervisor, physical host, network.  
  - Customer: OS patches, firewalls (security groups), application updates.  
- **Amazon RDS (PaaS)**  
  - AWS: Underlying OS, database engine patching, backups, replication.  
  - Customer: Schema design, queries, data encryption settings.  
- **AWS Lambda (FaaS/PaaS)**  
  - AWS: Runtime, scaling, availability.  
  - Customer: Function code, event configurations, IAM permissions.  
- **Amazon S3 (Managed Storage service)**  
  - AWS: Infrastructure, durability, availability.  
  - Customer: Bucket policies, object encryption, lifecycle rules.

## Applications & Real-World Context

**Scenario 1: Startup Web App on EC2 (IaaS)**  
A fintech startup deploys its trading platform on EC2 instances. They choose IaaS to retain full control over the OS and custom libraries. AWS handles physical security, networking, and hypervisor updates. The startup’s dev-ops team manages instance patching, vulnerability scans, and scaling via Auto Scaling groups. They implement CloudWatch alarms to monitor CPU and memory, responding to alerts by deploying new instances. By using IaaS, they can install specialized financial analysis software but must ensure their AMIs remain up to date and secure.

**Scenario 2: E-Commerce Database with Amazon RDS (PaaS)**  
An online retailer uses Amazon RDS for its product catalog database. AWS automates OS patching, storage management, and Multi-AZ failover, ensuring high availability. The retailer focuses on schema optimization, indexing strategies, and SQL query performance. They enable automated backups and configure encryption at rest with AWS KMS. In case of growth, they simply scale instance class or add read replicas. This PaaS approach offloads operational burden, letting the database team concentrate on schema design and query optimization.

**Scenario 3: SaaS Adoption for Collaboration Tools**  
A global consulting firm adopts Google Workspace (a SaaS) for email, document collaboration, and video conferencing. No infrastructure provisioning is required. The firm’s IT team manages user identities and access policies via SAML SSO and MFA. Google, as the provider, ensures service uptime, security patching, and data redundancy across regions. The consulting firm configures data retention policies and audits usage logs. By using SaaS, they eliminate concerns about mail servers or file servers, gaining rapid deployment and predictable costs.

## Common Misconceptions & Pitfalls
- Belief: *“PaaS automatically secures my application.”*  
  Corrective: PaaS secures the platform but you still must secure code, credentials, and data in transit.  
- Belief: *“AWS handles everything once I’m in the cloud.”*  
  Corrective: Only “of” the cloud layers are AWS’s duty; you secure “in” the cloud layers.  
- Belief: *“Serverless = SaaS.”*  
  Corrective: AWS Lambda is PaaS/FaaS—you still manage function code, resource policies, and dependencies.

## Worked Example Problem
**Problem**  
Acme Corp migrates three workloads to AWS:  
1. A legacy application on EC2 with a custom Linux OS.  
2. A MySQL database on Amazon RDS.  
3. A customer portal built on AWS Lambda.  

For each workload, list AWS responsibilities versus Acme Corp’s responsibilities.

**Solution**  
1. EC2 Legacy App  
   - AWS: Physical hardware, hypervisor, network.  
   - Acme: Guest OS patching, security groups, application updates.  
2. RDS MySQL  
   - AWS: OS and DB engine patching, backups, replication, storage management.  
   - Acme: Schema design, data encryption, IAM policies.  
3. Lambda Portal  
   - AWS: Runtime environment, scaling, availability, underlying servers.  
   - Acme: Function code, IAM roles, event sources, environment variables.

**Commentary**  
Identifying clear boundaries avoids gaps in security and operational coverage. Each service model shifts more tasks to AWS, so you can focus on higher-level concerns.

## Practice Exercises
Q1. In your own words, differentiate IaaS and PaaS.  
Q2. Name one AWS service that exemplifies each model: IaaS, PaaS, SaaS.  
Q3. For Amazon RDS, who is responsible for patching the underlying OS?  
Q4. A team uses AWS Lambda and S3 for a photo-processing app. List customer vs. AWS duties.  
Q5. Explain how SaaS reduces operational overhead compared to IaaS.

## Summary & Further Reading
- IaaS provides raw compute, storage, and network—customers manage OS and above.  
- PaaS abstracts infrastructure; customers deploy code to a managed platform.  
- SaaS delivers fully managed applications; customers focus on configuration and users.  
- AWS’s Shared Responsibility Model splits security duties: AWS secures the cloud, you secure in the cloud.  
- Mapping service models to responsibilities prevents security gaps and simplifies operations.

Annotated Bibliography  
1. **AWS Shared Responsibility Model Whitepaper** – Official AWS documentation on security boundaries.  
2. **NIST SP 800-145** – Formal definitions of IaaS, PaaS, SaaS from the National Institute of Standards and Technology.  
3. **AWS Certified Solutions Architect Official Study Guide** – Exam-focused coverage of service models and shared responsibility.  

## Solutions
A1. IaaS provides virtualized hardware resources; customers install and maintain the OS and applications. PaaS offers a managed platform for deploying code without managing servers.  
A2. IaaS: Amazon EC2; PaaS: AWS Elastic Beanstalk or Amazon RDS; SaaS: Amazon Chime or third-party services like Salesforce.  
A3. AWS patches the underlying OS in RDS.  
A4.  
- AWS: Runtime for Lambda, scaling, S3 storage durability.  
- Customer: Function code, IAM roles, bucket policies, event triggers.  
A5. SaaS shifts infrastructure, platform, and application maintenance to the provider, leaving only configuration and user management to the customer.