<div align="center">

# Cloud Engineering AWS

**Production-style AWS labs covering security, infrastructure, IAM, networking, monitoring, and real-world cloud operations.**

[![AWS](https://img.shields.io/badge/AWS-Cloud%20Engineering-FF9900?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/)
[![CloudFormation](https://img.shields.io/badge/CloudFormation-IaC-FF4F00?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/cloudformation/)
[![IAM](https://img.shields.io/badge/IAM-Security%20First-DD344C?style=for-the-badge&logo=amazon-aws&logoColor=white)](https://aws.amazon.com/iam/)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)]()

<img src="https://skillicons.dev/icons?i=aws,bash,linux,github,vscode" />

</div>

---

## Table of Contents

- [Overview](#overview)
- [Repository Structure](#repository-structure)
- [AWS Services Covered](#aws-services-covered)
  - [IAM — Identity & Access Management](#-iam--identity--access-management)
  - [EC2 — Elastic Compute Cloud](#-ec2--elastic-compute-cloud)
  - [S3 — Simple Storage Service](#-s3--simple-storage-service)
  - [VPC — Virtual Private Cloud](#-vpc--virtual-private-cloud)
  - [CloudWatch — Monitoring & Alerting](#-cloudwatch--monitoring--alerting)
  - [CloudTrail — Audit Logging](#-cloudtrail--audit-logging)
  - [Route 53 — DNS Management](#-route-53--dns-management)
  - [Cost Management — Billing & Budgets](#-cost-management--billing--budgets)
  - [AWS Organizations — Multi-Account Governance](#-aws-organizations--multi-account-governance)
- [Technologies Used](#technologies-used)
- [Skills Demonstrated](#skills-demonstrated)
- [Lab Structure](#lab-structure)

---

## Overview

This repository is a structured collection of hands-on AWS cloud engineering labs built around real-world scenarios and production-grade practices. Each section targets a core AWS service domain — from identity and access management to networking, monitoring, audit logging, and cost governance.

The work here reflects a security-first engineering mindset, with an emphasis on:

- **Least privilege** IAM design and role-based access control
- **Infrastructure as Code** using AWS CloudFormation
- **Operational visibility** through CloudWatch and CloudTrail
- **Secure networking** with VPC isolation models
- **DNS and compute integration** using Route 53 and EC2
- **Cost awareness** with AWS Budgets and billing alerts

---

## Repository Structure

```text
cloud-engineering-aws/
│
├── IAM/                          # Identity & Access Management labs
│   ├── IAM Users/                #   User creation, MFA, account setup
│   ├── iam-groups/               #   Group-based permission management
│   ├── iam-roles/                #   Role architectures & trust policies
│   │   ├── assume-role/          #     STS AssumeRole lab
│   │   └── ec2-s3-role-integration/  # EC2 instance profile with S3 access
│   └── explicit-deny-s3-policy/  #   Policy evaluation & explicit deny testing
│
├── EC2/                          # Compute infrastructure labs
│   └── templates/                #   CloudFormation templates (SSM-connected)
│
├── S3/                           # Object storage & bucket policy labs
│
├── VPC/                          # Networking & service exposure models
│
├── CloudWatch/                   # Monitoring, alarms & SNS alerting
│
├── CloudTrail/                   # Audit logging, KMS encryption, integrity
│
├── Route53/                      # DNS hosted zones & domain routing
│
├── Cost-Management/              # AWS Budgets & billing alerts
│
├── aws organizations/            # Multi-account governance & SCPs
│   └── service-control-policies/ #   SCP configuration examples
│
├── Architecture/                 # Multi-AZ, HA & cloud design concepts
│
├── policies/                     # Reusable IAM policy documents
│
└── screenshots/                  # Visual evidence across labs
```

---

## AWS Services Covered

### Identity & Access Management

#### IAM — Identity & Access Management

> `IAM/`

The IAM section is the most comprehensive in this repository, covering the full spectrum of AWS identity patterns:

| Lab | Description |
|-----|-------------|
| IAM User Setup | Created an admin IAM user, enabled MFA for both root and IAM accounts, configured account alias, and established the practice of never using the root account for daily operations |
| IAM Groups | Configured group-based permission management to apply policies at scale |
| AssumeRole with STS | Implemented temporary privilege escalation using IAM Roles and AWS STS — a core real-world pattern for cross-account and service-to-service authorization |
| EC2 + IAM Role Integration | Attached an IAM instance profile to an EC2 instance for secure S3 access without hardcoded credentials |
| Explicit Deny Testing | Tested IAM policy evaluation logic by verifying that explicit deny overrides allow, using S3 bucket access scenarios |

**Key Concepts:** RBAC, Trust Policies, Temporary Credentials, Least Privilege, Permission Delegation, Policy Evaluation Order

---

### Compute

#### EC2 — Elastic Compute Cloud

> `EC2/`

Progressed from manual EC2 provisioning to fully automated, secure deployments using Infrastructure as Code:

| Approach | Details |
|----------|---------|
| Manual Launch | Amazon Linux instance, SSH connectivity, foundational compute setup |
| CloudFormation Deployment | EC2 provisioned via CloudFormation template with an IAM Role for SSM — eliminating the need for SSH keys or open inbound ports |
| Session Manager Access | Connected to instances securely via AWS Systems Manager Session Manager instead of SSH |

**Key Concepts:** CloudFormation IaC, IAM Instance Profiles, SSM Session Manager, Keyless Access

---

### Storage

#### S3 — Simple Storage Service

> `S3/`

Covered S3 fundamentals and access control patterns:

- Created and configured S3 buckets with correct region placement
- Applied bucket policies and resource-based authorization
- Tested inline policies and explicit deny scenarios (in conjunction with the IAM lab)
- Explored bucket permission models: public, private, and policy-controlled access

**Key Concepts:** Bucket Policies, Resource Authorization, Object Storage, Namespace Uniqueness

---

### Networking

#### VPC — Virtual Private Cloud

> `VPC/`

Analyzed AWS service exposure models and the role of VPC as a network isolation boundary:

- Distinguished between **internet-facing (public)** and **VPC-isolated (private)** service architectures
- Explored how routing, NAT, Security Groups, and VPC Endpoints control access
- Established the foundational mental model for designing secure, multi-tier architectures

**Key Concepts:** Public vs. Private Subnets, Security Groups, Service Exposure, Network Boundaries

---

### Monitoring & Audit

#### CloudWatch — Monitoring & Alerting

> `CloudWatch/`

Built a full CPU monitoring and alerting pipeline on EC2:

```text
EC2 Instance
     │
     ▼
CloudWatch (CPUUtilization metric)
     │
     ▼ threshold exceeded (>15% for 5 min)
CloudWatch Alarm → ALARM state
     │
     ▼
Amazon SNS → Email Notification
```

| Configuration | Value |
|---------------|-------|
| Metric | CPUUtilization |
| Threshold | 15% |
| Evaluation Period | 5 minutes |
| Alarm Transition | OK → ALARM → OK |
| Notification | Email via Amazon SNS |

Simulated high CPU load using the `stress` tool to validate the full alarm lifecycle end-to-end.

**Key Concepts:** Metrics, Alarms, SNS, Threshold-Based Alerting, Alarm State Machine

---

#### CloudTrail — Audit Logging

> `CloudTrail/`

Deployed a production-grade CloudTrail configuration for full API activity visibility:

```text
     AWS API Activity
           │
           ▼
     AWS CloudTrail
           │
   ┌───────┴───────┐
   ▼               ▼
Amazon S3    CloudWatch Logs
(Audit Store) (Live Monitoring)
   │
   ▼
AWS KMS Encryption
```

| Feature | Configuration |
|---------|--------------|
| Trail Scope | Multi-Region |
| Log Storage | Amazon S3 |
| Encryption | AWS KMS |
| Integrity Validation | Enabled |
| Log Monitoring | CloudWatch Logs integration |
| IAM Role | Dedicated role for secure log delivery |

**Key Concepts:** API Audit Logging, KMS Encryption, Log Integrity, Multi-Region Coverage, CloudWatch Integration

---

### DNS & Routing

#### Route 53 — DNS Management

> `Route53/`

Connected a real custom domain to a live EC2 instance using Route 53:

1. **Created a public hosted zone** for `majed-devops.site` in Route 53 — AWS auto-generated NS and SOA records
2. **Updated nameservers** on Namecheap to delegate DNS management to Route 53
3. **Configured an A record** pointing the domain to the EC2 public IPv4 address
4. **Verified end-to-end** — domain resolved correctly in the browser to the running EC2 instance

**Key Concepts:** Hosted Zones, NS Delegation, A Records, DNS Propagation, Domain-to-EC2 Mapping

---

### Cost & Governance

#### Cost Management — Billing & Budgets

> `Cost-Management/`

Implemented proactive cost governance using AWS Budgets:

| Budget Setting | Value |
|----------------|-------|
| Budget Type | Monthly Cost Budget |
| Limit | $5 USD |
| Alert — Actual 85% | Email notification |
| Alert — Actual 100% | Email notification |
| Alert — Forecasted Overrun | Email notification |

**Key Concepts:** AWS Budgets, Billing Alerts, Cost Governance, FinOps Foundations

---

#### AWS Organizations — Multi-Account Governance

> `aws organizations/`

Explored AWS Organizations as a foundation for enterprise-scale AWS management:

- Centralized account management with Organizational Units (OUs)
- Service Control Policies (SCPs) for guardrail-based permission boundaries
- Centralized billing across all member accounts
- Security and governance at scale

**Key Concepts:** OUs, SCPs, Centralized Billing, Permission Guardrails, Multi-Account Strategy

---

## Technologies Used

| Category | Technologies |
|----------|-------------|
| Cloud Platform | AWS (Amazon Web Services) |
| Infrastructure as Code | AWS CloudFormation |
| Identity & Security | AWS IAM, AWS STS, AWS KMS |
| Compute | Amazon EC2, AWS Systems Manager |
| Storage | Amazon S3 |
| Networking | Amazon VPC, Security Groups |
| Monitoring | Amazon CloudWatch, Amazon SNS |
| Audit & Compliance | AWS CloudTrail |
| DNS | Amazon Route 53 |
| Cost Management | AWS Budgets, AWS Billing |
| Governance | AWS Organizations, SCPs |
| CLI & Scripting | AWS CLI, Bash, Linux |
| Version Control | Git, GitHub |

---

## Skills Demonstrated

```text
Security & IAM                    Infrastructure & IaC
─────────────────                 ────────────────────
✔ RBAC Design                     ✔ CloudFormation Templates
✔ Least Privilege                 ✔ EC2 Provisioning
✔ Trust Policies                  ✔ SSM Session Manager
✔ STS / AssumeRole                ✔ Instance Profiles
✔ Explicit Deny Logic             ✔ Multi-AZ Awareness
✔ MFA Enforcement

Monitoring & Compliance           Networking & DNS
───────────────────────           ────────────────
✔ CloudWatch Alarms               ✔ VPC Isolation Models
✔ SNS Alerting                    ✔ Subnet Architecture
✔ CloudTrail Audit Logging        ✔ Route 53 Hosted Zones
✔ KMS Log Encryption              ✔ DNS Record Management
✔ Log Integrity Validation        ✔ Domain-to-EC2 Routing

Cost & Governance
─────────────────
✔ AWS Budgets
✔ Billing Alerts
✔ AWS Organizations
✔ Service Control Policies
```

---

## Lab Structure

Each lab in this repository follows a consistent format:

```text
service/
├── README.md          ← Objectives, configuration, results
├── screenshots/       ← Visual proof of implementation
├── templates/         ← CloudFormation or config files (where applicable)
└── policies/          ← IAM policy documents (where applicable)
```

---

<div align="center">

**AWS Cloud Engineering Portfolio**

Security • Infrastructure • IAM • Networking • Monitoring • Governance

[![GitHub](https://img.shields.io/badge/GitHub-Majed--Saeed-181717?style=flat-square&logo=github)](https://github.com/Majed-Saeed)

</div>
