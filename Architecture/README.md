# Architecture

This section covers how AWS services are designed together to build reliable and scalable systems.

## Topics
- Multi-AZ
- Regions & Availability Zones

---

## What is Architecture?

Architecture is how different AWS services are connected and structured to build a system.

It is not a single service, but a design approach.

---

## Why it matters

- High availability (system stays up)
- Fault tolerance (handles failures)
- Scalability (handles traffic)
- Performance (faster for users)

---

## Example

User → Load Balancer → EC2 (Multiple AZs) → Database

---

## Key Idea

Architecture = how services work together, not just what services you use.
