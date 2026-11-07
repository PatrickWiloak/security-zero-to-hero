---
last-updated: 2026-11-07
difficulty: advanced
reading-time: 15 min
applies-to: AWS docs as read 2026-11-07
---

# 05 - Data protection

**Domain 5: Data Protection (18%)** - SCS-C03 tasks 5.1 to 5.3.

Data protection on AWS is encryption plus control of the keys, plus making data hard to destroy and easy to restore. Most exam questions are really about who can use a key and who cannot.

---

## 5.1 Data in transit

**Require encryption.** Enforce TLS at the service and with policy. Elastic Load Balancing uses **security policies** that fix the TLS versions and ciphers a listener accepts; choose a current policy and disable old protocols. For S3, deny any request that does not use TLS:

```json
{
  "Version": "2012-10-17",
  "Statement": [{
    "Sid": "DenyInsecureTransport",
    "Effect": "Deny",
    "Principal": "*",
    "Action": "s3:*",
    "Resource": ["arn:aws:s3:::example-bucket", "arn:aws:s3:::example-bucket/*"],
    "Condition": {"Bool": {"aws:SecureTransport": "false"}}
  }]
}
```

Certificates come from **AWS Certificate Manager** (public certificates, automatic renewal on integrated services) or **AWS Private CA** for internal use.

**Private access.** **AWS PrivateLink** and interface VPC endpoints let clients reach services using private IP addresses, with traffic staying on the AWS network and not traversing the public internet. Gateway endpoints serve S3 and DynamoDB. Attach endpoint policies to restrict what can be done through them (see [notes 03](./03-infrastructure-security.md)). **AWS Client VPN** gives remote users access to VPC resources, and **AWS Verified Access** provides application-level zero-trust access.

**Inter-resource encryption (new in C03).** Traffic between nodes of a distributed system needs protection too: inter-node encryption for Amazon EMR, Amazon EKS and SageMaker AI, and Nitro-based encryption in transit between supported EC2 instance types. The pattern: do not assume the private network is trusted.

## 5.2 Data at rest

**Choose the key service and the encryption location.**

- **AWS KMS** manages keys in a multi-tenant, FIPS-validated service integrated with most AWS services. **AWS CloudHSM** gives you dedicated hardware security modules under your control, for contractual or regulatory requirements to hold your own HSM or for non-AWS-integrated cryptography.
- **Server-side encryption** lets the service encrypt on write; **client-side encryption** encrypts before data leaves your application, so AWS never sees plaintext. Choose client-side when even the provider must not see the data.
- **Key types**: AWS owned keys (invisible), AWS managed keys (per service, automatic rotation, you cannot edit the policy) and **customer managed keys** (you control policy, rotation, and deletion).

**KMS key policies are the primary control.** Unlike most AWS resource policies, a KMS key policy does not automatically give permission to the account or its identities. The default key policy includes a statement that enables IAM policies, and without it IAM policies that allow access to the key are ineffective (IAM denies still work):

```json
{
  "Sid": "Enable IAM User Permissions",
  "Effect": "Allow",
  "Principal": {"AWS": "arn:aws:iam::111122223333:root"},
  "Action": "kms:*",
  "Resource": "*"
}
```

The principal here is the account, so it does not itself grant any identity access; it allows the account to delegate through IAM policies. If you write a key policy that names a single user and then delete that user, the key becomes unmanageable and you must contact AWS Support. Separate **key administrators** (manage but do not use the key) from **key users** (use it for cryptographic operations). Grants (`kms:CreateGrant`) let integrated services use a key for a resource; the condition `kms:GrantIsForAWSResource` stops users calling grant operations directly. Use `kms:ViaService` to restrict a key to specific services.

**Protect integrity and retention.** **S3 Object Lock** uses a write-once-read-many model and works only in buckets with versioning enabled. A retention period protects an object version until a retain-until date. In **compliance mode** no user, including the account root user, can overwrite or delete the version, and the retention cannot be shortened; the only way to remove it early is to delete the AWS account. In **governance mode** users with `s3:BypassGovernanceRetention` (and the bypass header) can override. A **legal hold** has no expiry and is independent of retention. Glacier Vault Lock gives similar immutability for vaults. **Versioning**, code signing and file validation protect integrity.

```bash
aws s3api create-bucket --bucket example-audit-logs --object-lock-enabled-for-bucket
aws s3api put-object-lock-configuration --bucket example-audit-logs \
  --object-lock-configuration '{"ObjectLockEnabled":"Enabled","Rule":{"DefaultRetention":{"Mode":"COMPLIANCE","Days":365}}}'
```

**Lifecycle and retention.** S3 Lifecycle policies move and expire objects; EFS lifecycle and FSx backup policies do similarly. Retention must match legal duty: keep what you must, delete what you must not keep.

**Backup and replication.** **AWS Backup** centralises policy-based backups across services, with vaults and, for ransomware resilience, logically air-gapped or locked vaults and cross-account, cross-Region copies. **Data Lifecycle Manager** automates EBS snapshots. **DataSync** moves data securely. Always test restores.

## 5.3 Confidential data, credentials, secrets and key material

**Secrets Manager** stores and rotates secrets. Rotation updates the credentials in both the secret and the database or service. Managed rotation (for managed secrets) needs no Lambda function; otherwise rotation runs a Lambda function. Applications fetch the secret at runtime by role, so no credential is in code or configuration.

```bash
aws secretsmanager rotate-secret --secret-id prod/app/db \
  --rotation-lambda-arn arn:aws:lambda:us-east-1:111122223333:function:rotate-db \
  --rotation-rules AutomaticallyAfterDays=30
```

Contrast with **SSM Parameter Store** (SecureString parameters, no built-in rotation) as a cheaper store for configuration.

**Imported key material** (new emphasis): you can create a KMS key with no key material and import your own, to meet policies that require you to generate keys. Imported material has an optional expiry, can be deleted, and AWS does not rotate it automatically, so you rotate by importing into a new key. Contrast it with AWS-generated material, which KMS can rotate automatically (and on demand). **External key stores** keep the key material outside AWS entirely, trading availability and latency for control.

**Masking sensitive data.** CloudWatch Logs data protection policies detect and mask sensitive data in log events; Amazon SNS message data protection does the same for messages. **Amazon Macie** discovers sensitive data in S3. Mask early, so downstream consumers never receive plaintext they should not.

**Keys and certificates across Regions.** A **multi-Region KMS key** has related keys in several Regions with the same key ID and material, which lets you encrypt in one Region and decrypt in another without re-encryption by a cross-Region call; each replica has its own policy. **AWS Private CA** issues and manages private certificates for internal workloads.

---

## Key terms

- **AWS KMS** - the managed service for creating and controlling cryptographic keys, integrated with most AWS services
- **AWS CloudHSM** - dedicated hardware security modules in AWS under the customer's control
- **Customer managed key** - a KMS key you create and control, including its policy, rotation and deletion
- **Key policy** - the primary resource policy for a KMS key; it does not grant account access unless it says so
- **Key administrator** - a principal allowed to manage a KMS key but not use it for cryptographic operations
- **Grant** - a delegated, limited permission to use a KMS key, often created by integrated AWS services
- **Envelope encryption** - encrypting data with a data key and protecting that data key with a KMS key
- **S3 Object Lock** - write-once-read-many protection for object versions in buckets with versioning
- **Compliance mode** - an Object Lock mode in which no user, including root, can delete or overwrite a protected version
- **Governance mode** - an Object Lock mode that users with special permission can override
- **Legal hold** - an Object Lock protection with no expiry that stays until explicitly removed
- **AWS Backup** - a service that centralises policy-based backup across AWS services
- **Imported key material** - key material you generate outside AWS and import into a KMS key
- **External key store** - a KMS feature in which key material stays in a key manager outside AWS
- **Multi-Region key** - a set of KMS keys in different Regions that share key ID and material
- **AWS Private CA** - a managed private certificate authority

---

## Related

- [Notes 04: identity and access management](./04-identity-and-access-management.md)
- [Notes 03: infrastructure security](./03-infrastructure-security.md)
- **[📖 Default key policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policy-default.html)** - the statement that enables IAM policies, administrators and users
- **[📖 Locking objects with Object Lock](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lock.html)** - retention modes and legal holds
- **[📖 Rotate AWS Secrets Manager secrets](https://docs.aws.amazon.com/secretsmanager/latest/userguide/rotating-secrets.html)** - managed rotation and Lambda rotation
- **[📖 AWS PrivateLink concepts](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints.html)** - private connectivity and endpoint policies
- **[📖 SCS-C03 exam guide, Domain 5](https://docs.aws.amazon.com/aws-certification/latest/security-specialty-03/security-specialty-03-domain5.html)** - task statements and skills
