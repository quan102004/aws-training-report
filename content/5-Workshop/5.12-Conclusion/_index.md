---
title : "Conclusion & Future Work"
date : "2026-07-06"
weight : 12
chapter : false
pre : " <b> 5.12 </b> "
---

#### Achievements

- A **complete 10-flow serverless system** on AWS: authentication (Cognito + JWT authorizer), CRUD (Lambda + DynamoDB), secure CV storage (S3 + KMS + Presigned URLs), **daily automatic reminders running in production** (EventBridge + SES + DLQ), monitoring (CloudWatch Alarm → SNS) and auditing (CloudTrail → S3)
- A complete React + TypeScript + Tailwind frontend with auto token refresh and per-user data isolation
- Actual development cost of **$0.85**, with a standard Git branch + PR team workflow
- Security principles applied throughout: least-privilege IAM, no Scans, never trusting client data, fully private buckets, encryption at rest

#### Lessons learned

- IdToken vs AccessToken with JWT authorizers; GSI keys are immutable — design carefully before creating
- Defense in depth saved us when one route was missing its authorizer
- New AWS accounts have abuse-prevention limits (CloudFront, SES sandbox) — factor them into real project plans

#### Future work

- **Infrastructure as Code** (Terraform) to recreate the infrastructure automatically
- Complete CloudFront + WAF + Route 53 once the account is verified; request SES production access
- Delete CVs from S3 when a job is deleted (DeleteObject or an S3 Lifecycle rule)
- Cognito Groups for aggregate statistics APIs; CI/CD with GitHub Actions
