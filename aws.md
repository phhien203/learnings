# AWS Certified Cloud Practitioner

## Security and Compliance

### AWS Shared Responsibility Model

- Customer Responsibility

Responsible for security IN the Cloud

    - Customer Data
    - Platform, Application, IAM
    - OS, Network, Firewall Config
    - Client-side data encryption & data integrity authentication
    - Server-side encryption (file system and/or data)
    - Network traffic protection (encryption/integrity/identity)

- AWS Responsibility

Responsible for security OFF the Cloud

    - Compute
    - Storage
    - Database
    - Networking
    - Regions
    - Availability Zones
    - Edge Locations

### IAM

Service used to securely control access to your AWS resources.

Controls authentication (who) and authorization (what they can do).

### Dashboard

1. Users
2. User Groups
3. Roles
4. Policies

### Root User vs. IAM User

#### Root User

- One per account
- Unrestricted access
- Difficult to restrict and revoke access

Can perform

- Close an AWS account
- Change an AWS support plan
- Change AWS account settings

#### IAM User

- Multiple per account
- Users can be deleted or disabled
- Easy to restrict access

#### Best Practices

- Always work in IAM account, not root account
- Setup IAM users with least number of permissions needed

### Roles

- Similar to a user (an identity with permissions)
- Does not have credentials (passwords or keys)
- Assumable, temporarily, by anyone who needs it
- Users, User Groups, Roles -> Identities (the "who")

Real-life analogy

A role is like a hat. When you wear a hat, you have that role assigned. You can wear a hat of Parent, Software Engineer, Soccer Coach, Home Chief, Therapist.

### Policy

Who can do what to which resources and when.

E.g. Allow IAM users to rotate their own credentials programmatically and in the console.

```JSON
{
  "Statement": [
    {
      "Effect": "allow/deny",
      "Action": "s3:DeleteBucket",
      "Resource": "arn:aws:ec2:*:*:instance/instance-id",
      "Condition": {
        "condition": {
          "key": "value"
        }
      }
    }
  ]
}
```

### 2FA Authentication

Two or more factors to authenticate (figure out who you are)
- Something you know (password)
- Something you have (phone or hard token)
- Something you are (fingerprint)

### IAM Best Practices

- Use IAM user for day-to-day work, NOT the root account
- Use Roles to give permissions to AWS Services
- Don't share credentials (user name, password, access keys)
- Assign permissions to groups (made up of users) rather than to individual users
- When assigning permissions (policies), give the least amount possible
- Enforce MFA and strong password policies

### Security and Compliance Services

Infrastructure Protection:
- AWS Shield
- AWS Web Application Firewall

Data Protection:
- AWS Key Management System (KMS) and CloudHSM
- AWS Certificate Manager (ACM)
- AWS Secrets Manager
- Amazon Macie

Detection:
- Amazon Inspector
- Amazon GuardDuty
- AWS Config
- AWS Security Hub

Incident Response:
- Amazon Detective

Compliance:
- Amazon Artifact

### Distributed Denial of Services (DDoS)

AWS Shield - protects against DDoS on AWS

Standard
- Free
- Automatically protects all AWS customers
- Protects from the most common types of DDoS attacks

Advanced
- Paid services that protects against more sophisticated attacks
- Integrates with other services like CloudFront, Route 53, and Elastic Load Balancing

### AWS Web Application Firewall

Configure rules
- Allow, block, monitor/count
- IP addresses, country of origin, present of a script, URL strings, etc.
- Example:
    - Block IP addresses and values that are used by known attackers
    - A specific IP address can only send 100 requests to your application in 5 minutes

### Two types of encryptions

At rest: data that stored and archived on a device

E.g: S3 bucket, hard disk, database

In transit: data being transferred from one location to another

E.g: moving data from EC instance to an S3 bucket, moving data from an on-premises data center to AWS

### AWS Key Management System (KMS)

- Primary service for encryption in AWS
- AWS manages the encryption hardware, software, and keys for you
- Integrated with many other AWS services, including EBS, S3, Redshift, and Cloudtrail
- FIPS 140-2 Compliance: Level 2 overall


### AWS CloudHSM (Hardware Security Module)

- AWS provisions the hardware and you do everything else
- AWS cannot access your keys
- AWS cannot recover your keys
- Integrated with limited number of other AWS services
- FIPS 140-2 Compliance: Level 3 (considered more secure)

### Types of keys

- AWS Managed: AWS creates and manages. Used by AWS services: aws/lambda, aws/cloud9, aws/s3
- Customer managed: customer create and manage, can create policies to rotate keys, specify who can use and manage the keys, support bring your own keys
- Custom key stores: created with CloudHSM. You own and manage

### AWS Certificate Manager (ACM)

Provision, manage, and deploy public and private SSL/TLS certificates

- Public - for resources on the public internet (these certificates are free)
- Private - for resources on private networks

Loads certificates on
- API Gateway
- Elastic load balancers
