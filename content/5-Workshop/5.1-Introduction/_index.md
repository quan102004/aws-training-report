---
title : "Introduction & Architecture"
date : "2026-07-06"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### The problem

Job seekers often submit dozens of applications at once and easily miss the right time to follow up with recruiters. We built a web application to manage all applications in one place, store a CV per application, and send automatic email reminders.

#### Why serverless?

- **No servers to manage**: everything runs on managed services (Lambda, DynamoDB, S3, Cognito...)
- **Scales automatically** with the number of users
- **Pay-per-use pricing** — ideal for the early stage. Actual cost during the whole development process: **$0.85** (see the Cost section)

#### Architecture diagram

![Architecture Diagram](/images/capstone/architecture-v6.png)

**The 10 main flows:**

| # | Flow | Services |
|---|------|----------|
| 1a–1b | Access the domain, check WAF rules | Route 53, CloudFront, AWS WAF |
| 2 | Load the React UI (origin fetch) | CloudFront ↔ S3 Static Website |
| 3 | Sign in / receive JWT | Amazon Cognito |
| 4a–4b | Call the API with JWT, validate token | CloudFront → API Gateway ↔ Cognito |
| 5 | Route requests to the right Lambda | API Gateway → 3 Lambdas |
| 6 | Read / write job data | Lambda ↔ DynamoDB (+GSI) |
| 7a–7b | Issue Presigned URL, upload/download CV directly | Lambda, S3 Private, KMS |
| 8a–8d | 9:00 AM cron scans due jobs, sends reminder emails | EventBridge → Lambda → SES (+SQS DLQ) |
| 9a–9d | Collect logs, alert admin when thresholds are breached | CloudWatch Alarm → SNS → Email |
| 10a–10b | Record every API call for auditing | CloudTrail → S3 |

#### Design highlights

- **No VPC**: a purely serverless architecture — every component is a managed service protected by IAM, WAF and KMS, reducing complexity and cost.
- **No DynamoDB Scan anywhere**: user queries go through the `userId` partition key; the reminder flow queries the `FollowUpIndex` GSI.
- **Strict data isolation**: `userId` comes from the JWT validated by API Gateway; users can never read or modify other users' data.
