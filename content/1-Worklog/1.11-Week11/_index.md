---
title : "Week 11 Worklog"
date : "2026-06-29"
weight : 11
chapter : false
pre : " <b> 1.11. </b> "
---

### Week 11 Objectives:

- Complete CV storage, the reminder pipeline, and the monitoring layer.
- Build the React frontend and finalise the architecture diagram.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Create the CV bucket with KMS encryption at rest<br>- Add a Lambda function that issues presigned URLs for upload and download | 29/06/2026 | 29/06/2026 | |
| 3 | - Configure EventBridge Scheduler to trigger daily follow-up checks<br>- Verify a sender identity in SES and send reminder emails | 30/06/2026 | 30/06/2026 | |
| 4 | - Attach an SQS dead-letter queue to the reminder Lambda<br>- Create CloudWatch alarms and route notifications through SNS<br>- Enable CloudTrail for audit logging | 01/07/2026 | 01/07/2026 | |
| 5 | - Build the React frontend: application list, status filter, add/edit/delete, CV upload | 02/07/2026 | 02/07/2026 | |
| 6 | - Finalise the architecture diagram after several rounds of review<br>- Apply feedback on numbered flows, edge routing, and WAF placement | 03/07/2026 | 03/07/2026 | |

### Week 11 Achievements:

- Completed CV storage: files are encrypted with KMS and uploaded straight from the browser through presigned URLs.
- Completed the reminder pipeline: EventBridge Scheduler to Lambda to SES, with an SQS dead-letter queue capturing failed invocations.
- Added the observability layer: CloudWatch alarms, SNS notifications, and CloudTrail audit logs.
- Delivered a working React frontend covering the full application lifecycle.
- Iterated the architecture diagram through several versions, learning that a diagram is a communication artefact — numbering the flows and routing the edges cleanly matters as much as the components themselves.
