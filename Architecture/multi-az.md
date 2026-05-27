# AWS Multi-AZ Architecture

Basic AWS Multi-AZ architecture concept for improving availability and reducing single points of failure.

---

## Services

- Amazon VPC
- EC2
- Application Load Balancer (ALB)
- Security Groups
- Route Tables
- Internet Gateway
- Amazon RDS (Concept)

---

## Architecture

```text
Internet
    ↓
Application Load Balancer
    ↓
EC2 Instances (Multiple AZs)
    ↓
Database Layer