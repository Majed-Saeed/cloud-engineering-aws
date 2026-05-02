# ☁️ AWS Global Infrastructure
### Regions · Availability Zones · Edge Locations

[![AWS](https://img.shields.io/badge/AWS-Cloud_Architecture-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)](https://aws.amazon.com)
[![SAA-C03](https://img.shields.io/badge/SAA--C03-Exam_Relevant-232F3E?style=for-the-badge&logo=amazonaws)](https://aws.amazon.com/certification/certified-solutions-architect-associate/)
[![CLF-C02](https://img.shields.io/badge/CLF--C02-Exam_Relevant-232F3E?style=for-the-badge&logo=amazonaws)](https://aws.amazon.com/certification/certified-cloud-practitioner/)
[![Study Notes](https://img.shields.io/badge/Type-Study_Notes-blue?style=for-the-badge)](.)

> A deep-dive reference on how AWS distributes infrastructure globally using **Regions**, **Availability Zones**, and **Edge Locations** — with architecture patterns, design decisions, and exam-ready takeaways.

---

## 📊 By the numbers

| Metric | Count |
|--------|-------|
| Launched Regions | 33+ |
| Availability Zones | 105+ |
| Edge / PoP locations | 600+ |
| Countries with edge presence | 90+ |

---

## 🗺️ Architecture overview

```
                        ┌────────────────────────────────────────┐
                        │   AWS Region: ap-southeast-1           │
                        │   (Singapore)                          │
                        │                                        │
                        │  ┌──────────┐ ┌──────────┐ ┌────────┐ │
                        │  │  AZ-1a   │ │  AZ-1b   │ │ AZ-1c  │ │
                        │  │ Primary  │ │ Standby  │ │Tertiary│ │
                        │  │ EC2, RDS │ │ EC2, RDS │ │EC2, $  │ │
                        │  └──────────┘ └──────────┘ └────────┘ │
                        └────────────────────────────────────────┘
                                           ▲
                                           │ origin fetch (cache miss)
                                           │
[User in KL] ──→ [Edge Location: KL PoP] ──┘
                  CloudFront · Route 53
                  Shield · WAF
```

**Request flow:** User → nearest Edge PoP → (on cache miss) → Region → target AZ

---

## 📍 Region

A **Region** is a distinct geographic area, fully isolated from all other regions. AWS never replicates your data between regions without explicit configuration.

### Key properties
- Contains **2–6 Availability Zones** per region
- Complete isolation — separate control plane, networking, and power
- Data stays inside the region unless you explicitly configure cross-region replication

### How to choose a region

| Factor | Considerations |
|--------|---------------|
| **Latency** | Deploy close to your users. Use Route 53 latency routing to measure before committing. |
| **Compliance** | GDPR → EU regions. PDPA (Malaysia), PDPB (India) may dictate choices for APAC workloads. |
| **Service availability** | Not all services launch in every region simultaneously — verify before designing. |
| **Cost** | EC2 + data transfer pricing varies up to 20–30% between regions. `us-east-1` is typically cheapest. |

> **Exam tip:** Region selection is driven by latency, compliance, service availability, and cost — not by the number of edge locations near it.

---

## 🏢 Availability Zone (AZ)

An **AZ** is one or more physical data centers inside a region with **independent power, cooling, and networking**. AZs in the same region are connected via low-latency private fibre (< 2ms).

### Key properties
- Isolated failure domain — power or networking failure in one AZ does **not** affect others
- The letter suffix (1a, 1b, 1c) is account-specific — your `us-east-1a` may be physically different to someone else's
- Foundation of the **Multi-AZ high availability** pattern

### Multi-AZ reference architecture

```
                    ┌─── Application Load Balancer ───┐
                    │                                 │
               ┌────▼────┐                     ┌─────▼───┐
               │  AZ-1a  │                     │  AZ-1b  │
               │  EC2 x2 │                     │  EC2 x2 │
               │ RDS Pri │◄──── sync repl ────►│ RDS Std │
               └─────────┘                     └─────────┘
```

> **Exam tip:** RDS Multi-AZ is for **availability**, not performance. The standby does not serve read traffic. Use read replicas for read scaling.

---

## ⚡ Edge Location

An **Edge Location** (Point of Presence) is a site that caches content and runs edge services close to users — completely separate from Regions and AZs.

### Key properties
- 600+ locations across 90+ countries — far more than Regions
- Hosts **CloudFront** CDN, **Route 53**, **AWS Shield**, **WAF**, **Lambda@Edge**, and **Global Accelerator**
- Reduces latency by serving cached responses without a round-trip to the origin region

### Services by edge component

| Service | What it does at the edge |
|---------|--------------------------|
| `CloudFront` | Caches static and dynamic content at the nearest PoP |
| `Lambda@Edge` | Runs Node.js / Python at the PoP — auth, A/B testing, header manipulation |
| `Route 53` | Responds to DNS queries from the nearest PoP globally |
| `AWS Shield` | Absorbs DDoS traffic at the edge before it reaches your origin |
| `Global Accelerator` | Routes TCP/UDP through AWS backbone from the nearest PoP |

---

## 📐 Design patterns

### Pattern 1 — Multi-AZ (high availability)

**Goal:** Survive a data center failure within a region.

```
ALB → EC2 (AZ-1a) + EC2 (AZ-1b)
          ↓
    RDS Primary (AZ-1a) ←──sync──→ RDS Standby (AZ-1b)
```

- Auto Scaling maintains capacity if one AZ goes dark
- ALB health checks stop routing to unhealthy targets automatically
- RDS failover DNS update typically completes in 60–120 seconds

### Pattern 2 — Multi-Region (disaster recovery)

**Goal:** Survive an entire region going offline.

| Strategy | RTO | RPO | Cost |
|----------|-----|-----|------|
| Backup & restore | Hours | Hours | $ |
| Pilot light | Minutes–hours | Minutes | $$ |
| Warm standby | Minutes | Seconds | $$$ |
| Active–active | Seconds | Near-zero | $$$$ |

```
Route 53 health check
        │
        ├──→ us-east-1 (primary)
        │       S3 CRR ──────────────┐
        │       DynamoDB Global ─────┤
        │                            ▼
        └──→ eu-west-1 (DR)  ←── replicated data
```

### Pattern 3 — Edge caching (performance)

**Goal:** Serve content with sub-10ms response times globally.

```
User → CloudFront PoP
            │
            ├── Cache HIT  →  instant response (no origin roundtrip)
            │
            └── Cache MISS → fetch from origin → cache → respond
                              (S3 bucket / ALB / API Gateway)
```

---

## 🧠 Key takeaways

```
Multi-AZ      → within one region  → protects against hardware / data center failure
Multi-Region  → across regions     → protects against regional outages / disaster recovery
Edge          → independent PoPs   → faster content delivery, not HA or DR
```

- **AZs are not the same as Regions** — one region has multiple AZs
- **Edge locations are not AZs** — they don't run your EC2 or RDS workloads
- **S3 is regional** — it replicates across AZs automatically but not across regions
- **IAM is global** — not bound to any region or AZ
- **RDS Multi-AZ ≠ Multi-Region** — standby is in the same region, different AZ

---

## 🔗 Related topics

`CloudFront` · `Route 53 Latency Routing` · `RDS Multi-AZ vs Read Replicas` · `EC2 Auto Scaling across AZs` · `Global Accelerator` · `AWS Local Zones` · `AWS Wavelength` · `AWS Outposts` · `S3 Cross-Region Replication` · `DynamoDB Global Tables`

---

## 📚 Resources

- [AWS Global Infrastructure map](https://aws.amazon.com/about-aws/global-infrastructure/)
- [Amazon CloudFront edge locations](https://aws.amazon.com/cloudfront/features/)
- [SAA-C03 Exam Guide](https://aws.amazon.com/certification/certified-solutions-architect-associate/)

---

*Part of my AWS Solutions Architect study notes · PRs and corrections welcome*
