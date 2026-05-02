# ☁️ AWS Global Infrastructure
### Regions · Availability Zones · Edge Locations

[![AWS](https://img.shields.io/badge/AWS-Cloud_Architecture-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![SAA-C03](https://img.shields.io/badge/SAA--C03-Exam_Relevant-232F3E?style=for-the-badge&logo=amazonaws)](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
[![Focus](https://img.shields.io/badge/Focus-Architecture-blue?style=for-the-badge)](.)

> Understanding how AWS is structured globally is essential for designing highly available and fault-tolerant systems.

---

## 🗺️ Architecture Overview

```
User → Edge Location (Cache)
              ↓
        AWS Region
        ├── AZ-1a
        ├── AZ-1b
        └── AZ-1c
```

---

## 📍 Region

A **Region** is a geographic location where AWS runs multiple data centers.

- Fully isolated from other regions  
- Contains multiple Availability Zones  
- No cross-region data replication unless configured  

### Used for:
- Compliance & data residency  
- Disaster recovery (Multi-Region)  
- Latency optimization  

---

## 🏢 Availability Zone (AZ)

An **AZ** is one or more data centers inside a Region.

- Independent power, networking, cooling  
- Connected with low latency  
- Failure in one AZ does not affect others  

### Used for:
- High availability (Multi-AZ)  
- Fault isolation  

---

## ⚡ Edge Location

An **Edge Location** is used to cache content closer to users.

- Used by CloudFront  
- Improves latency  
- Not part of VPC / AZ  

---

## 📊 Comparison

| Component | Scope | Purpose |
|----------|------|--------|
| Region | Global area | Isolation & compliance |
| AZ | Inside region | High availability |
| Edge | Global edge | Performance |

---

## 🧠 Key Takeaways

- Multi-AZ → protects against **data center failure**
- Multi-Region → protects against **regional failure**
- Edge → improves **latency only**

---

## 🛠️ Real Scenario

Production web app:

- Runs in 2 AZs  
- Uses Load Balancer  
- Auto Scaling enabled  
- Database in RDS Multi-AZ  

➡️ If one AZ fails → application remains available  

---

## 🔗 Related

`Multi-AZ` · `Auto Scaling` · `Load Balancing` · `CloudFront` · `Route 53`

---

## 🚀 Summary

AWS infrastructure is designed to:
- Isolate failures  
- Scale globally  
- Deliver low-latency systems  
