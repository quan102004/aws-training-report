---
title : "Week 10 Worklog"
date : "2026-06-22"
weight : 10
chapter : false
pre : " <b> 1.10. </b> "
---

### Week 10 Objectives:

- Build the core backend: authentication, database, and API layer.
- Debug the first integration issues between services.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 2 | - Create a Cognito User Pool and app client<br>- Test the sign-up and sign-in flow | 22/06/2026 | 22/06/2026 | |
| 3 | - Design the DynamoDB table schema<br>- Create a Global Secondary Index for follow-up queries | 23/06/2026 | 23/06/2026 | |
| 4 | - Write four Lambda functions: list, create, update, delete applications | 24/06/2026 | 24/06/2026 | |
| 5 | - Create an HTTP API on API Gateway<br>- Attach a JWT authorizer backed by the Cognito User Pool | 25/06/2026 | 25/06/2026 | |
| 6 | - Test every route with Postman<br>- Fix the bugs found during integration | 26/06/2026 | 26/06/2026 | |

### Week 10 Achievements:

- Completed the authentication flow with Cognito and protected the API with a JWT authorizer.
- Built the DynamoDB table together with a GSI, and the four Lambda functions behind it.
- Debugged three issues worth recording:
  * **GSI partition key mismatch** — the index was created on `followUpFlag` while the item attribute was written as `followUpStatus`, so the query silently returned nothing.
  * **Missing JWT authorizer on the `cv-url` route** — every other route was protected, but this one had been left open.
  * **Postman sending the wrong token** — the `AccessToken` was being sent where the API Gateway JWT authorizer expects the `IdToken`.
- Learned that a silent empty result from DynamoDB is more often a schema mismatch than a data problem.
