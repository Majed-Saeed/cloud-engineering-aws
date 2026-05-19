# IAM Roles

## What is IAM Role
IAM Role provides temporary permissions to AWS services or users.

## Common Use Cases
- Lambda Execution Role
- Cross Account Access
- Identity Federation
- Emergency Access

## IAM User vs IAM Role

### IAM User
- Permanent identity
- Long-term credentials

### IAM Role
- Temporary credentials
- Assumed when needed

## Lambda Execution Role
AWS Lambda can assume a role to access services like:
- S3
- CloudWatch

## Identity Federation
Users can sign in using:
- Google
- Facebook
- Active Directory

without creating IAM users.
