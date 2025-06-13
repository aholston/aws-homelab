# AWS Homelab: IAM Roles & Permissions

## Overview

This document defines and tracks IAM users, roles, and permissions used in the AWS Homelab. It enforces least privilege, documents access boundaries, and supports secure experimentation within a realistic cloud environment.

---

## Goals

* Avoid using the root account for any operational access
* Use IAM users and roles with scoped permissions
* Enable centralized auditing and secure access via SSM

---

## IAM Users

| User Name     | Purpose               | Permissions           | MFA Enabled | Notes                          |
| ------------- | --------------------- | --------------------- | ----------- | ------------------------------ |
| `andre-admin` | Primary admin account | `AdministratorAccess` | ✅           | Used for all console + CLI use |

Root account access is disabled for all operations and retained for emergency use only.

---

## IAM Roles

| Role Name          | Attached To         | Purpose                                   | Policies                          |
| ------------------ | ------------------- | ----------------------------------------- | --------------------------------- |
| `jumpbox-ssm-role` | Jumpbox EC2         | Enable secure access via SSM              | `AmazonSSMManagedInstanceCore`    |
| `app-server-role`  | App/DB EC2 (future) | Scoped role for internal backend services | (To be defined — least privilege) |

---

## Best Practices Followed

* IAM roles are used for EC2 access instead of access keys
* No key pairs or SSH are used — all admin access is via SSM + IAM
* MFA is enabled for all IAM users
* Roles are documented by purpose and permissions for portfolio clarity

---

## To Do

* [ ] Define policies for `app-server-role`
* [ ] Create additional roles for logging, audit, or simulated attack cases
* [ ] Set up group-based IAM access if multiple identities are used

---

## Notes

This document will evolve with the homelab. Each new service added (e.g., Lambda, S3, GuardDuty) will have its own scoped roles and be documented here.
