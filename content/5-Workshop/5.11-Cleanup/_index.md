---
title : "Clean Up Resources"
date : "2026-07-06"
weight : 11
chapter : false
pre : " <b> 5.11 </b> "
---

After the defense, clean up resources in this order to avoid charges (especially after credits expire):

1. **EventBridge Scheduler**: delete the `daily-followup-check` schedule (stop the cron first)
2. **CloudFront**: Disable → wait for Deployed → Delete distribution (if created)
3. **API Gateway**: delete `job-tracker-api`
4. **Lambda**: delete all 4 functions (delete their IAM roles in the IAM console)
5. **DynamoDB**: delete the `JobTrackerJobs` table (turn off Deletion protection first)
6. **S3**: Empty then Delete each bucket (CV, web, CloudTrail logs) — buckets must be empty before deletion
7. **CloudTrail**: delete the `job-tracker-trail` trail
8. **CloudWatch**: delete the `api-5xx-alarm` alarm and the `/aws/lambda/...` log groups
9. **SNS / SQS**: delete the `job-tracker-alerts` topic and the `followup-dlq` queue
10. **Cognito**: delete the User Pool
11. **SES**: delete verified identities
12. Keep: the **Budget alert** (free, worth keeping) and the GitHub repositories

{{% notice tip %}}
Final check via Billing → Bills after 1–2 days: every cost line at zero means the cleanup is complete.
{{% /notice %}}
