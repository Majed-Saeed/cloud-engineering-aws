## AWS CloudTrail Audit Logging

Implemented an enhanced CloudTrail deployment focused on auditability, log protection, and operational visibility.

### Configuration

- Multi-Region CloudTrail Trail
- Amazon S3 Log Storage
- AWS KMS Encryption
- Log File Integrity Validation
- CloudWatch Logs Integration
- Dedicated IAM Role for Log Delivery

### Architecture

```text
        AWS API Activity
                │
                ▼
          AWS CloudTrail
                │
      ┌─────────┴─────────┐
      ▼                   ▼
 Amazon S3         CloudWatch Logs
 Audit Storage      Log Monitoring
      │
      ▼
 AWS KMS Encryption
```

### Highlights

- Centralized audit logging across AWS regions.
- Encrypted CloudTrail log storage using AWS KMS.
- Enabled log file validation to support integrity verification.
- Integrated CloudTrail with CloudWatch Logs for operational monitoring.
- Configured IAM permissions required for secure log delivery.

### Services

AWS CloudTrail • AWS KMS • Amazon S3 • Amazon CloudWatch Logs • AWS IAM
