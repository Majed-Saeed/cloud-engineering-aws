# IAM Explicit Deny Policy Lab

## Overview
This lab demonstrates how AWS IAM policies work when both Allow and Deny permissions exist.

## Objectives
- Create IAM user
- Assign AmazonS3FullAccess policy
- Create custom deny policy
- Prevent bucket deletion using explicit deny
- Test IAM permission evaluation

## Services Used
- IAM
- Amazon S3

## Steps Performed

### 1. Created IAM User
Created IAM user named:
- Leo

Enabled:
- AWS Management Console access

---

### 2. Attached Managed Policy
Attached AWS managed policy:
- AmazonS3FullAccess

This allowed full access to Amazon S3 resources.

---

### 3. Created S3 Bucket
Created S3 bucket:
- myfirstbucketleoaws

---

### 4. Created Custom IAM Policy
Created custom policy:
- DenyDeleteBucket

Policy used:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "DenyDeleteBucket",
      "Effect": "Deny",
      "Action": "s3:DeleteBucket",
      "Resource": "*"
    }
  ]
}
```

---

### 5. Attached Policy to User
Attached custom deny policy to IAM user:
- Leo

---

### 6. Tested Permissions
Attempted to delete the S3 bucket.

Result:
- Access denied

This demonstrates that:
- Explicit Deny overrides Allow in AWS IAM policy evaluation.
