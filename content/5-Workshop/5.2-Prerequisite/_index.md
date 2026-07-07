---
title : "Prerequisites"
date : "2026-07-06"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Accounts and tools

- AWS account (Free Tier with $200 promotional credits), working region: **ap-southeast-1**
- A dedicated IAM user for each team member (never the root user)
- Node.js 20 LTS, Git, VS Code, Postman
- A GitHub repository with a **branch-per-module + Pull Request** workflow

#### Budget alert — the very first step

Before creating any resource, we set an **AWS Budget of $5/month** with email alerts — an insurance layer against unexpected costs.

![Budget alert](/images/capstone/budget-alert.png)

#### Naming conventions

| Resource | Name |
|---|---|
| DynamoDB table | `JobTrackerJobs` (GSI: `FollowUpIndex`) |
| Lambda | `job-tracker-crud-job`, `job-tracker-get-jobs`, `job-tracker-cv-presigned`, `lambda-followup-checker` |
| API Gateway (HTTP API) | `job-tracker-api` |
| S3 buckets | `job-tracker-cv-tqt-2026` (CV), web bucket, CloudTrail logs bucket |
| SQS | `followup-dlq` |
| SNS | `job-tracker-alerts` |
