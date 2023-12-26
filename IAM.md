# **Identity & Access Management (IAM)**

- **Global Service:** IAM entities like roles can be used globally without recreation in different regions.

- **IAM Query API:** Allows making direct calls to the IAM web service using access key ID and secret access key for authentication.

**Users & Groups**

- **Groups:** Collections of users with attached policies; they cannot be nested.

- **User Membership:** A user can belong to multiple groups or none at all.

- **Root User:** Has full access to the AWS account.

- **IAM User:** Limited permissions compared to the root user; it's recommended to log in as an IAM user with admin access for safety.

- **IAM Group Limitation:** IAM Groups are not considered identities and cannot be identified as principals in IAM policies.

- **Assumption of Roles:** Only users and services can assume a role, not groups.

- **IAM User Credentials:** A new IAM user created using AWS CLI or AWS API has no AWS credentials initially.

**Policies**

- **Types of Policies:**
  - **User-based Policies:** Define allowed API calls for a specific user.
  - **Resource-based Policies:** Control access to AWS resources.

- **Policy Structure:** JSON documents outlining permissions for users, groups, or roles.
 

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::example-bucket/*",
      "Condition": {
        "IpAddress": {"aws:SourceIp": "203.0.113.0/24"},
        "NotIpAddress": {"aws:SourceIp": "192.0.2.0/24"},
        "DateGreaterThan": {"aws:CurrentTime": "2023-01-01T00:00:00Z"}
      }
    },
    {
      "Effect": "Deny",
      "Action": "s3:*",
      "Resource": "arn:aws:s3:::example-bucket/sensitive-data/*"
    }
  ]
}
```

**Explanation:**

- **Version:** Indicates the language version of the policy. In this case, it's using version "2012-10-17," which is a common version for AWS policies.

- **Statement:** An array containing individual statements that define the permissions. In this example, there are two statements.

  - **Statement 1:**
    - **Effect:** Specifies whether the permissions are allowed or denied. In this case, it's set to "Allow."
    - **Action:** Lists the AWS actions (API calls) that are allowed. Here, the policy allows the "s3:GetObject" and "s3:PutObject" actions.
    - **Resource:** Specifies the AWS resource to which the actions apply. In this case, it's an S3 bucket named "example-bucket" and allows actions on objects within that bucket ("/*").
    - **Condition:** Defines conditions under which the permissions are granted. This statement allows access only if the request comes from the IP address range "203.0.113.0/24" but not from "192.0.2.0/24" and only if the request is made after January 1, 2023.

  - **Statement 2:**
    - **Effect:** Specifies whether the permissions are allowed or denied. In this case, it's set to "Deny."
    - **Action:** Lists the AWS actions (API calls) that are denied. This statement denies any S3 actions ("s3:*") on objects within the "sensitive-data" directory of the "example-bucket" S3 bucket.
    - **Resource:** Specifies the AWS resource to which the actions apply.

This policy, in summary, allows read and write access to objects in the "example-bucket" S3 bucket under certain conditions. However, it explicitly denies any actions on objects within the "sensitive-data" directory of the same bucket.

- **Least Privilege Principle:** Policies should follow the principle of least privilege.

- **Policy Attachment:** Policies assigned to a user are called inline policies.

**Trust Policies**

- **Role Trust Policies:** Define which principal entities (accounts, users, roles, federated users) can assume the role.

- **IAM Role:** Acts as both an identity and a resource that supports resource-based policies.

- **Role Requirements:** Both a trust policy and an identity-based policy must be attached to an IAM role.

**Roles**

- **Collection of Policies:** Roles are collections of policies for AWS services.

- **IAM Service Role:** When used with EC2, it must be stored in an instance profile.

**Protect IAM Accounts**

- **Password Policy:** Enforces standards for password rotation, reuse, and prevents brute force attacks.

- **Multi-Factor Authentication (MFA):** Recommended for both root user and IAM users.

**Reporting Tools**

- **Credentials Report:** Lists users and the status of their credentials, used for security audits.

- **Access Advisor:** Shows service permissions granted to a user and when those services were last accessed, useful for policy revision.

**Access Keys**

- **Usage:** Necessary for AWS CLI and SDK; each user generates their own access keys.

- **Security:** Access keys should not be shared, and if lost, a new access key must be generated.

- **Identification:** Access Key ID is analogous to a username, while Secret Access Key is like a password.

**Guidelines**

- **Root Account:** Use only for initial account setup.

- **IAM User Creation:** One physical user should correspond to one IAM user.

- **MFA Enforcement:** Enforce Multi-Factor Authentication for both root and IAM users.

- **Credential Security:** Never share IAM credentials and access keys.

**Policy Simulator**

- **Purpose:** An online tool to check API calls allowed for an IAM User, Group, or Role based on their permissions.

**Permission Boundaries**

- **Function:** Sets the maximum permissions an IAM entity can obtain.

- **Application:** Can be applied to users and roles (not groups) to prevent privilege escalation.

**Assume Role vs Resource-based Policy**

- **Assume Role:** When assuming an IAM role, original permissions are relinquished in favor of the role's assigned permissions.

- **Resource-based Policy:** In this case, the principal doesn't have to give up their original permissions.
