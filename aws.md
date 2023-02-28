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
