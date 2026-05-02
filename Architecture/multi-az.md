# Multi-AZ Architecture

## Overview
Multi-AZ is an architectural pattern where an application is deployed across multiple Availability Zones within the same region to eliminate single points of failure.

---

## Objectives
- High availability
- Fault isolation
- Production-grade resilience

---

## Architecture

- VPC spanning multiple AZs
- Public Subnets → Application Load Balancer (ALB)
- Private Subnets → EC2 instances
- Database → RDS (Multi-AZ)

Flow:
Client → ALB → Target Group → EC2 (AZ-A / AZ-B) → Database

---

## Implementation

1. Create VPC across multiple AZs
2. Create public and private subnets in each AZ
3. Deploy ALB in public subnets
4. Launch EC2 instances in private subnets
5. Register instances in a Target Group
6. Enable Auto Scaling across AZs
7. Configure a highly available database (e.g., RDS Multi-AZ)

---

## Failure Handling

- If an instance fails → traffic goes to healthy instances
- If an AZ fails → traffic shifts to another AZ automatically

---

## Best Practices

- Distribute resources across AZs
- Use health checks with ALB
- Keep databases private
- Avoid single points of failure

---

## Key Takeaway

Multi-AZ is a design pattern, not a single AWS service.
