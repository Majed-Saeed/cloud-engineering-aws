# ☁️ AWS Global Infrastructure — Regions, AZs & Edge Locations

![AWS](https://img.shields.io/badge/AWS-Cloud_Architecture-FF9900?style=flat&logo=amazonaws&logoColor=white)
![Level](https://img.shields.io/badge/Level-Foundations-blue)
![Focus](https://img.shields.io/badge/Focus-Architecture-green)

> Understanding how AWS is structured globally is essential for designing highly available, fault-tolerant, and scalable systems.

---

## 🗺️ Overview

AWS infrastructure is built in layers to deliver reliability and performance worldwide.

```
User → Edge Location (Cache)
              ↓
        AWS Region (e.g. ap-southeast-1)
            ├── AZ-1a
            ├── AZ-1b
            └── AZ-1c
```

---

## 📍 Region

A **Region** is a geographic location where AWS clusters multiple data centers.

- Fully isolated from other regions
- Contains multiple Availability Zones
- Services are deployed at the region level

### Used for:
- Data residency & compliance  
- Disaster recovery (Multi-Region)  
- Latency optimization  

---

## 🏢 Availability Zone (AZ)

An **Availability Zone** is one or more data centers inside a Region.

- Independent power, cooling, networking
- Connected via low-latency links
- Designed for fault isolation

### Used for:
- High availability (Multi-AZ)
- Redundancy within a region

---

## ⚡ Edge Location

An **Edge Location** is a global point of presence used for caching content closer to users.

- Used by CloudFront (CDN)
- Reduces latency significantly
- Not part of VPC or AZ structure

### Used for:
- Content delivery
- DNS (Route 53)
- DDoS protection (AWS Shield)

---

## 📊 Comparison

| Component | Scope | Purpose | Example Services |
|----------|------|--------|------------------|
| Region | Global area | Isolation & compliance | EC2, RDS, S3 |
| AZ | Inside Region | High availability | EC2, RDS Multi-AZ |
| Edge | Global edge | Performance | CloudFront, Route 53 |

---

## 🧠 Key Takeaways

- Multi-AZ → protects against **data center failure**
- Multi-Region → protects against **regional outages**
- Edge Locations → improve **user experience & latency**

---

## 🛠️ Real Scenario

Production web application:

- Deployed across 2 AZs  
- Uses Application Load Balancer  
- Auto Scaling enabled  
- Database in RDS Multi-AZ  

➡️ If one AZ fails → application remains available

---

## 🔗 Related

`Multi-AZ Architecture` · `Auto Scaling` · `Load Balancing` · `CloudFront` · `Route 53`

---

## 🚀 Summary

AWS global infrastructure is designed to:
- Isolate failures
- Scale globally
- Deliver low-latency experiences

Understanding this is the foundation of every real AWS architecture.
