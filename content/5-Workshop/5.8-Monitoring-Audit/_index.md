---
title : "Monitoring & Audit"
date : "2026-07-06"
weight : 8
chapter : false
pre : " <b> 5.8 </b> "
---

#### Flow 9: CloudWatch Alarm → SNS → Admin email

- All API Gateway and Lambda logs/metrics flow into **CloudWatch** (the `/aws/lambda/...` log groups were our main debugging tool throughout the project)
- Alarm **`api-5xx-alarm`**: the API's `5xx` metric, **Sum** statistic, 5-minute period, threshold **≥ 5** → when breached, it publishes to the SNS topic **`job-tracker-alerts`** → admin email (subscription confirmed)

![CloudWatch alarm](/images/capstone/cloudwatch-alarm.png)

The "5 errors / 5 minutes" threshold is sensitive enough to catch real incidents while avoiding false alarms from a single stray error.

#### Flow 10: CloudTrail → S3 audit

Trail **`job-tracker-trail`** (multi-region) records **every API call in the account** — not just API Gateway but also Lambda, DynamoDB, S3, Cognito, IAM operations — stored in a dedicated S3 bucket `aws-cloudtrail-logs-...`.

![CloudTrail logging](/images/capstone/cloudtrail-logging.png)

This was a priority for us as one team member has an information-security background: when an incident occurs, Event history lets us trace **who did what, when, and from where**.

#### The "admin" role in this system

The application **deliberately has no admin role**: application data and CVs are sensitive, and least privilege applies to operators too. System administration happens at the infrastructure layer (IAM, CloudWatch, CloudTrail). Future extension: Cognito Groups for aggregate statistics APIs.
