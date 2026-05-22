# IAM Role AssumeRole Lab (AWS)

## Overview

This lab demonstrates how IAM Roles work in AWS using `AssumeRole`.

The goal was to understand:

- Difference between IAM Users and IAM Roles
- Temporary permissions using STS
- Trust relationships
- Role-based access control

---

# Architecture

```text
IAM User (junior-admin)
        │
        ▼
AssumeRole (STS)
        │
        ▼
IAM Role (PowerRole)
        │
        ▼
Temporary Administrator Permissions
```

---

# What I Created

## IAM User

User:
```text
junior-admin
```

Permissions:
```text
No administrative permissions
```

Purpose:
- Simulate a low-privileged user account

Screenshot:
```text
junior-admin-review-page.png
```

---

## IAM Role

Role:
```text
PowerRole
```

Attached Policy:
```text
AdministratorAccess
```

Purpose:
- Provide temporary elevated permissions

Screenshot:
```text
trust-policy-and-admin-policy.png
```

---

# Trust Policy

The role trust policy allows only the `junior-admin` user to assume the role.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::553490164486:user/junior-admin"
      },
      "Action": "sts:AssumeRole"
    }
  ]
}
```

---

# Testing Process

## Before AssumeRole

Logged in as:
```text
junior-admin
```

Result:
```text
AccessDenied when accessing EC2
```

Screenshot:
```text
ec2-access-denied-junior-admin.png
```

---

## Switch Role

Role used:
```text
PowerRole
```

Display name:
```text
AdminMode
```

Screenshot:
```text
switch-role-powerrole.png
```

---

## After AssumeRole

Result:
- Full EC2 access
- Temporary administrator permissions

Screenshot:
```text
adminmode-console-home.png
```

---

## After Exiting Role

Returned to:
```text
junior-admin
```

Result:
```text
AccessDenied restored
```

Screenshot:
```text
ec2-access-denied-junior-admin.png
```

---

# Key Concepts Learned

## IAM User
Permanent identity for a person or application.

---

## IAM Role
Temporary identity with specific permissions.

---

## AssumeRole
Allows a user or service to temporarily obtain permissions from a role.

---

## STS (Security Token Service)
Provides temporary credentials when assuming a role.

---

# Security Benefits

- No permanent admin access
- Temporary elevated permissions
- Better auditing and access control
- Reduced security risk

---

# Skills Practiced

- IAM Users
- IAM Roles
- Trust Policies
- AssumeRole
- AWS STS
- Permission Testing
- Access Control Validation
