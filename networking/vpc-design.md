# AWS Homelab: Network Design (Phase 1)

## Overview

This document outlines the initial network design and provisioning steps for a secure AWS homelab environment. It serves as a foundation for learning AWS architecture, implementing cloud security best practices, and creating a well-documented portfolio.

---

## Goals

* Simulate a realistic production-lite cloud environment
* Learn and apply AWS networking and security fundamentals
* Build a clear, extensible foundation for future services and attack simulations

---

## VPC Design

* **CIDR Block:** `10.0.0.0/16`
* **Availability Zone:** `us-east-1a`
* **Region:** `us-east-1`

This CIDR block gives 65,536 IPs and supports plenty of future subnetting and experimentation.

---

## Subnet Layout

| Subnet Name      | CIDR Block    | AZ           | Purpose                | Public? |
| ---------------- | ------------- | ------------ | ---------------------- | ------- |
| Public Subnet A  | `10.0.1.0/24` | `us-east-1a` | Jumpbox / Bastion host | ✅       |
| Private Subnet A | `10.0.2.0/24` | `us-east-1a` | App server or backend  | ❌       |

These subnets are split logically by exposure:

* Public subnet has a route to the internet via an **Internet Gateway**
* Private subnet does **not** have outbound internet access

---

## Routing Strategy

### Route Tables

* **Public Route Table**

  * Associated with: Public Subnet A
  * Routes:

    * `10.0.0.0/16` → `local`
    * `0.0.0.0/0` → Internet Gateway

* **Private Route Table**

  * Associated with: Private Subnet A
  * Routes:

    * `10.0.0.0/16` → `local`

This ensures public instances can reach the internet, while private ones remain isolated.

---

## Planned EC2 Resources

| Instance Name | Subnet           | Purpose                      |
| ------------- | ---------------- | ---------------------------- |
| Jumpbox EC2   | Public Subnet A  | Secure admin access via SSM  |
| App/DB EC2    | Private Subnet A | Internal service or database |

Jumpbox access will be via **AWS Systems Manager (SSM)**. No SSH, public IPs, or key pairs are required. Private EC2s will not be publicly accessible.

---

## IAM Considerations

| Role/User           | Purpose                       | Scope                                            |
| ------------------- | ----------------------------- | ------------------------------------------------ |
| Admin IAM User      | Full account admin (not root) | AdministratorAccess + MFA                        |
| Jumpbox IAM Role    | Attach to EC2                 | SSM access only (`AmazonSSMManagedInstanceCore`) |
| App Server IAM Role | Attach to private EC2         | Least privilege for app needs                    |

MFA will be enforced for all IAM users. Root account will be locked down and no longer used for daily access. A new IAM user (`andre-admin`) has been created for all console and CLI interactions.

---

## Security Tools To Be Added Later

* AWS CloudTrail (✅ Configured)
* AWS Config (baseline compliance)
* GuardDuty (threat detection)
* CloudWatch Alarms (visibility)
* Simulated attack exercises (e.g., compromised keys, open ports)

---

## Implementation Notes

* VPC created with CIDR `10.0.0.0/16`
* Public subnet `10.0.1.0/24` created with auto-assign public IPs enabled
* Internet Gateway (`homelab-igw`) created and attached to the VPC
* Public route table created and associated with public subnet
* Route `0.0.0.0/0 → IGW` added to public route table
* Private subnet `10.0.2.0/24` created with no public IP auto-assignment
* Private route table created and associated with private subnet
* Private route table only contains local VPC routing
* Jumpbox EC2 instance uses SSM for secure access, not SSH
* EC2 IAM Role includes `AmazonSSMManagedInstanceCore` policy
* SSM access verified through the AWS Console
* IAM user `andre-admin` created with `AdministratorAccess` and MFA enabled
* Root user access disabled for all operational tasks
* CloudTrail trail `homelab-cloudtrail` enabled, multi-region, with log file validation and default S3 encryption

---

## Next Steps

* [x] Deploy a jumpbox in the public subnet
* [x] Test connectivity and isolation between instances
* [x] Create IAM admin user and enforce MFA
* [x] Begin setting up CloudTrail logging
* [ ] Define app server IAM role
* [ ] Begin enabling GuardDuty and baseline alerting

---

## Notes

This document will evolve as the lab grows. All design choices aim for clarity, realism, and security. Portfolio-ready visuals and architecture diagrams are included in the `diagrams/` folder.
