---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 8 Objectives:

* Design, deploy, and finalize the Capstone Project: **Serverless Job Application Tracker**.
* Successfully integrate Serverless services: API Gateway, Cognito, DynamoDB, Lambda, S3, Amplify, WAF, Route 53, SES, and CloudWatch/CloudTrail.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Gather requirements and design the overall system architecture <br> - Set up Amazon DynamoDB database and configure Amazon Cognito for user management | 06/08/2026 | 06/08/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - Develop AWS Lambda functions to handle job application CRUD operations <br> - Integrate and configure Amazon API Gateway | 06/09/2026 | 06/09/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Create S3 bucket for CV storage <br> - Write logic to generate Presigned URLs to upload/download CVs securely from the browser | 06/10/2026 | 06/10/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Configure Amazon SES for email delivery <br> - Set up Amazon EventBridge Scheduler to trigger daily reminder Lambda functions | 06/11/2026 | 06/11/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Deploy the Frontend application to AWS Amplify <br> - Configure operational monitoring with CloudWatch Alarms, SNS, and audit logging with CloudTrail | 06/12/2026 | 06/12/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Week 8 Achievements:

* Completed the design and implementation of the stable **Serverless Job Application Tracker** on AWS, meeting all business requirements.
* Secured the system by configuring detailed IAM permissions, user authentication with Cognito, and integrating WAF to prevent abuse.
* Successfully implemented secure upload/download flows for CV files using S3 Presigned URLs, reducing server bandwidth and improving performance.
* Created an automated email notification mechanism, ensuring users receive timely follow-up reminders.
* Configured automated monitoring and auditing systems to detect errors and log system actions.

