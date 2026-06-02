# AWS Service Control Policies (SCPs)

## Definition
A Service Control Policy (SCP) is a policy document used within AWS Organizations to define a permission boundary for AWS accounts. SCPs restrict the maximum available permissions for an account.

## Key Characteristics
- SCPs do not grant permissions. They only define the maximum permissions an account can have.
- SCPs apply to the entire account, including the account root user.
- The account root user cannot be directly restricted, but restricting the account via an SCP indirectly limits the root user.
- Permissions must still be granted separately through IAM identity policies.

## Attachment and Inheritance
SCPs can be attached at three levels:
- Organization root container — affects all accounts in the organization.
- Organizational Unit (OU) — affects all accounts in that OU and any nested OUs.
- Individual account — affects only that account.

SCPs inherit downward through the organization tree.

## Management Account
The management account is not affected by any SCP, whether attached directly or inherited. Running workloads in the management account is not recommended, as it cannot be restricted by SCPs.

## Allow List vs Deny List

### Deny List (default)
- When SCPs are enabled, AWS attaches a default policy named `FullAWSAccess` to the organization and all OUs.
- `FullAWSAccess` allows all actions on all resources, so no restrictions exist by default.
- Restrictions are applied by adding explicit Deny statements.
- Lower administrative overhead. New AWS services are allowed automatically.

### Allow List
- Requires removing the `FullAWSAccess` policy, leaving an implicit deny on all actions.
- Required services must be explicitly allowed in a new policy.
- Higher administrative overhead. Each service must be added manually.

## Policy Examples

FullAWSAccess (default):
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "*",
      "Resource": "*"
    }
  ]
}
```

Deny S3:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:*",
      "Resource": "*"
    }
  ]
}
```

Allow S3 and EC2 only:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:*",
        "ec2:*"
      ],
      "Resource": "*"
    }
  ]
}
```

## Permission Evaluation
- Effective permissions are the intersection of IAM identity policies and applicable SCPs.
- An action must be allowed by both the IAM identity policy and the SCP to be permitted.
- An explicit Deny in any policy overrides any Allow.
- In the absence of an explicit Allow, an implicit Deny applies.

## Evaluation Reference

| Allowed by IAM | Allowed by SCP | Result |
|----------------|----------------|--------|
| Yes            | Yes            | Allowed |
| Yes            | No             | Denied |
| No             | Yes            | Denied |
| No             | No             | Denied |
