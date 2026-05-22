<div align="center">

# ☁️ Cloud Engineering AWS

Production-style AWS cloud engineering labs focused on security, infrastructure, IAM, networking, monitoring, and real-world cloud operations.

<img src="https://skillicons.dev/icons?i=aws,bash,linux,github" />

</div>

---

# Overview

This repository contains hands-on AWS implementations and cloud engineering practice projects built using AWS native services and security-focused architecture patterns.

The goal of this repository is to document practical cloud engineering workflows, infrastructure management, IAM design, and operational best practices in a structured and scalable format.

---

# Repository Architecture

```text
cloud-engineering-aws/
│
├── Architecture/
├── CloudWatch/
├── Cost-Management/
├── EC2/
├── IAM/
├── Route53/
├── S3/
├── VPC/
├── aws organizations/
└── policies/
```

---

# Core Focus Areas

<table>
<tr>
<td width="50%">

### Identity & Security
- IAM Users
- IAM Roles
- AssumeRole
- STS
- RBAC
- Least Privilege
- Trust Policies
- Explicit Deny

</td>
<td width="50%">

### Infrastructure & Networking
- EC2
- VPC
- Multi-AZ Architecture
- Route53
- DNS Routing
- Security Groups
- Cloud Architecture

</td>
</tr>

<tr>
<td width="50%">

### Storage & Access Control
- S3 Policies
- Bucket Permissions
- Inline Policies
- Resource Authorization

</td>
<td width="50%">

### Monitoring & Operations
- CloudWatch
- AWS Organizations
- Cost Management
- Infrastructure Validation

</td>
</tr>
</table>

---

# AWS Services Used

| Service | Purpose |
|---|---|
| IAM | Identity and access management |
| STS | Temporary credentials |
| EC2 | Compute infrastructure |
| S3 | Object storage |
| Route53 | DNS management |
| VPC | Networking |
| CloudWatch | Monitoring |
| AWS Organizations | Multi-account management |
| CloudFormation | Infrastructure provisioning |

---

# Featured Labs

## IAM Role AssumeRole Lab
Implemented secure temporary privilege escalation using IAM Roles and AWS STS.

### Skills Practiced
- AssumeRole
- Trust Relationships
- Temporary Credentials
- RBAC
- Least Privilege

---

## EC2 + IAM Role Integration
Integrated EC2 instances with IAM roles for secure service authorization without hardcoded credentials.

---

## Explicit Deny Policy Testing
Tested IAM policy evaluation logic using explicit deny scenarios with S3 access controls.

---

# Engineering Approach

This repository follows a structured lab organization model:

```text
service/
 ├── README.md
 ├── screenshots/
 ├── templates/
 └── policies/
```

Each lab includes:
- Documentation
- Architecture/workflow explanation
- Screenshots
- Policies/templates when applicable

---

# Objectives

- Build production-style AWS engineering skills
- Practice secure cloud design
- Develop real-world IAM workflows
- Improve infrastructure organization
- Document practical cloud implementations

---

# Current Areas of Practice

- AWS IAM Security
- Infrastructure Architecture
- Cloud Networking
- Access Control Design
- Resource Authorization
- DNS Management
- Monitoring & Logging
- Multi-Service Integration

---

<div align="center">

### AWS Cloud Engineering Portfolio Repository

Security • Infrastructure • IAM • Networking • Operations

</div>
