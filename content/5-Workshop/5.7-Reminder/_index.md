---
title : "Automatic Reminders (EventBridge + SES)"
date : "2026-07-06"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

#### Flow 8: fully automated

**EventBridge Scheduler** (`daily-followup-check`, cron `0 9 * * ? *`, timezone Asia/Saigon) → invokes the **Follow-up Checker Lambda** → queries the `FollowUpIndex` GSI with `followUpStatus = PENDING AND followUpDate <= today` → sends reminder emails via **Amazon SES** → marks jobs as `NOTIFIED`.

![EventBridge schedule](/images/capstone/eventbridge-schedule.png)

#### Duplicate prevention

The cron runs daily but users are **never spammed**: once reminded, a job switches to `NOTIFIED` and drops out of the query; when the user changes the follow-up date, the CRUD Lambda resets it to `PENDING` so it will be reminded again for the new date.

#### Failure handling — SQS Dead Letter Queue

The Lambda is configured for asynchronous invocation: on failure it retries twice, and if it still fails the message lands in the **`followup-dlq`** queue — no data is lost and it can be reprocessed later.

#### Results

Manual test returned `{"checked": 2, "sent": 2}`; the second run returned `{"checked": 0, "sent": 0}` (duplicate prevention works). The next morning, at exactly 9:00 AM, the system **sent the email entirely on its own**:

![Automatic reminder email](/images/capstone/reminder-email.png)

{{% notice note %}}
SES is in **sandbox mode** — it can only send to verified addresses, which fits the demo scope (team members' emails verified). Production access will be requested for a real launch.
{{% /notice %}}
