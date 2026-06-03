## AWS CloudTrail

### Overview
AWS CloudTrail is a logging and auditing service that records API activity and account actions across AWS. It helps track changes, monitor user activity, and maintain an audit trail for security and compliance purposes.

### Features
- Records AWS API calls and account activity.
- 90-day Event History available by default.
- Supports Management Events, Data Events, and Insights Events.
- Stores logs in Amazon S3 for long-term retention.
- Integrates with CloudWatch Logs for monitoring and alerting.
- Supports organization-wide logging through AWS Organizations.
- Multi-region trail support.

### Event Types
- **Management Events** – Administrative actions on AWS resources.
- **Data Events** – Operations performed within resources (e.g., S3 object access, Lambda invocations).
- **Insights Events** – Detect unusual API activity patterns.

### Trail Types
- **Single-Region Trail** – Captures events from one region.
- **Multi-Region Trail** – Captures events from all AWS regions.

### Log Destinations
- Amazon S3
- CloudWatch Logs

### Notes
- CloudTrail is enabled by default with 90 days of event history.
- Data Events must be explicitly enabled.
- Global services such as IAM, STS, and CloudFront generate global service events.
- Log delivery is not real-time and may take several minutes.

### Use Cases
- Security auditing
- Compliance monitoring
- Change tracking
- Troubleshooting and investigation
- Activity monitoring across AWS accounts
