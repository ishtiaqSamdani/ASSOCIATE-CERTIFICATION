# **Identity & Access Management (IAM)**

- **Global Service:** IAM entities like roles can be used globally without recreation in different regions.

- **IAM Query API:** Allows making direct calls to the IAM web service using access key ID and secret access key for authentication.

**Users & Groups**

- **Groups:** Collections of users with attached policies; they cannot be nested.

- **User Membership:** A user can belong to multiple groups or none at all.

- **Root User:** Has full access to the AWS account.

- **IAM User:** Limited permissions compared to the root user; it's recommended to log in as an IAM user with admin access for safety.

- **IAM Group Limitation:** IAM Groups are not considered identities and cannot be identified as principals in IAM policies.

- **IAM User Credentials:** A new IAM user created using AWS CLI or AWS API has no AWS credentials initially.

**Policies**

- **Types of Policies:**
  - **User-based Policies:** Define allowed API calls for a specific user.
  - **Resource-based Policies:** Control access to AWS resources.

- **Policy Structure:** JSON documents outlining permissions for users, groups, or roles.


```json
{
  "Version": "2012-10-17",
  "Id": "MyExamplePolicy",
  "Statement": [
    {
      "Sid": "AllowS3Read",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/*",
      "Condition": {
        //conditions
      },
      "Principal": {"AWS": "arn:aws:iam::123456789012:user/ishtiaq"},
      "NotPrincipal": {"AWS": "arn:aws:iam::987654321098:role/RestrictedRole"},
      "Description": "Allow ishtiaq to read objects from 'my-bucket'."
    }
  ],
  "Description": "This is a simple example IAM policy."
}
```

**Explanation:**

- **`Sid`:** Statement ID for uniqueness and manageability.

- **`Effect`:** Specifies whether the permissions are allowed or denied. Here, it's set to "Allow."

- **`Action`:** Lists the AWS actions (API calls) that are allowed. In this case, it allows the "s3:GetObject" action.

- **`Resource`:** Specifies the AWS resource to which the actions apply. Here, it allows actions on objects within the "my-bucket" S3 bucket ("/*").

- **`Condition`:** Defines conditions under which the permissions are granted. In this example, it allows access only if the request comes from the IP address range "192.168.1.0/24" and if the request is made after January 1, 2023.

- **`Principal`:** Specifies the AWS entity (user, role, or service) that the statement is about. In this case, it allows access for the IAM user "ishtiaq."

- **`NotPrincipal`:** Specifies the AWS entity that the statement is not about. Here, it denies access if the action is performed by the role "RestrictedRole."

- **`Description`:** A brief description of the statement's purpose for documentation purposes.

**Roles**

- **Collection of Policies:** Roles are collections of policies for AWS services.

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
