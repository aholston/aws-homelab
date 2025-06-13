# AWS Homelab: CloudTrail Setup

## Overview

This document outlines how CloudTrail was configured for the AWS Homelab to ensure account activity is logged, monitored, and auditable. CloudTrail provides the foundation for detecting misconfigurations, investigating suspicious behavior, and simulating real-world incident response.

---

## Goals

* Enable full visibility into AWS account activity
* Log all management events across all regions
* Store logs in a dedicated S3 bucket
* Use log file validation for tamper detection

---

## Configuration Details

| Setting               | Value                                |
| --------------------- | ------------------------------------ |
| Trail Name            | `homelab-cloudtrail`                 |
| Trail Type            | Multi-region (global)                |
| Apply to Organization | ❌ No (single-account homelab)        |
| Log Destination       | S3 bucket: `homelab-cloudtrail-logs` |
| Encryption            | SSE-S3 (default)                     |
| Log File Validation   | ✅ Enabled                            |
| SNS Notification      | ❌ Disabled                           |
| Data Events           | ❌ Not enabled (for now)              |

---

## Log Storage

* Logs are delivered to the following path:
  `s3://homelab-cloudtrail-logs/AWSLogs/<account-id>/`

* Default permissions applied to bucket allow CloudTrail to write logs.

* No lifecycle policies or object locks are currently configured (future improvement).

---

## Verification Steps

* Confirmed trail status: **Logging**
* Trail is collecting management events from all supported services
* Log files will be visible after initial actions are taken in the account

---

## Future Improvements

* Enable CloudWatch integration for real-time alerting
* Add S3 and Lambda data event logging for more granular visibility
* Enable log retention policies and integrity alerting
* Enable CloudTrail Insights for anomaly detection (optional)

---

## Notes

This trail forms the foundation for future security simulations and compliance tracking. As additional services are added to the lab, CloudTrail coverage may be expanded to include data events and custom logging filters.
