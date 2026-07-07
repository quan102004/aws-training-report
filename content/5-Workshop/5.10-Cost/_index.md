---
title : "Cost"
date : "2026-07-06"
weight : 10
chapter : false
pre : " <b> 5.10 </b> "
---

#### Actual development cost

After the entire build and testing process (thousands of API requests, dozens of Lambda deployments, CV uploads, reminder emails):

| Item | Amount |
|---|---|
| Total incurred cost | **$0.85** |
| Covered by Free Tier credits | $0.85 |
| **Actually paid** | **$0.00** |

![Actual billing](/images/capstone/billing.png)

![Remaining credits](/images/capstone/credits.png)

#### Why so cheap?

- **DynamoDB On-demand, Lambda, API Gateway HTTP API**: pay-per-request — development traffic fits comfortably in the free tier
- **HTTP API is ~70% cheaper than REST API**; arm64 Lambda is ~20% cheaper than x86
- **S3 Bucket Key** cuts KMS call costs by ~90%
- Nothing runs 24/7 (no EC2, no NAT Gateway, no VPC)

#### Estimate at real scale (1,000 monthly active users)

| Service | Monthly estimate |
|---|---|
| Lambda + API Gateway | ~$1–3 |
| DynamoDB On-demand | ~$2–5 |
| S3 (CV) + CloudFront | ~$1–3 |
| Cognito | $0 (under 10,000 MAU) |
| SES + SNS + CloudWatch | ~$1 |
| **Total** | **~$5–12/month** |

The serverless architecture lets cost **grow linearly with real users** instead of paying a fixed price for idle servers.
