# AWS CloudWatch Monitoring

## Overview
This lab demonstrates AWS CloudWatch monitoring and alerting using EC2.

## What I Did
- Created an EC2 instance
- Configured CloudWatch alarm for CPUUtilization
- Set threshold to 15%
- Created SNS topic for email notifications
- Connected SNS with CloudWatch alarm
- Used stress command to increase CPU usage
- Triggered CloudWatch alarm successfully
- Received email notification from SNS

## Services Used
- Amazon EC2
- Amazon CloudWatch
- Amazon SNS

## Testing Command
```bash
stress --cpu 1 --timeout 300s
