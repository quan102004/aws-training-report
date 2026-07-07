---
title : "Cognito & DynamoDB"
date : "2026-07-06"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Amazon Cognito — user authentication

We created a **User Pool** with email sign-in and an SPA app client (no client secret). Users self-register, receive a 6-digit confirmation code by email and activate their account.

![Cognito User Pool](/images/capstone/cognito-pool.png)

For Postman testing we also enabled the `ALLOW_USER_PASSWORD_AUTH` flow on the app client.

{{% notice tip %}}
**Lesson learned: IdToken vs AccessToken.** The API Gateway JWT authorizer is configured with Audience = Client ID, and only the **IdToken** contains the `aud` claim. Using the AccessToken returns 401 even though the token itself is perfectly valid — it took us a whole debugging session to figure this out.
{{% /notice %}}

#### DynamoDB — job data storage

Table `JobTrackerJobs`, **On-demand** capacity mode, encrypted at rest with the AWS managed KMS key:

- **Partition key**: `userId` (String) — taken from the `sub` claim in the JWT
- **Sort key**: `jobId` (String) — a UUID generated at creation time

![DynamoDB table](/images/capstone/dynamodb-table.png)

**GSI `FollowUpIndex`** powers the reminder flow:

- Partition key: `followUpStatus` (PENDING / NOTIFIED / NONE)
- Sort key: `followUpDate` (YYYY-MM-DD)

Thanks to this GSI, the reminder Lambda **queries exactly the due PENDING jobs** instead of scanning the whole table.

{{% notice warning %}}
**Lesson learned: GSI keys cannot be modified.** We initially created the partition key as `followUpFlag` by mistake; the Lambda failed with `ValidationException: Query condition missed key schema element`. We had to delete and recreate the index with the correct `followUpStatus` key — deleting an index does not affect the data in the table.
{{% /notice %}}
