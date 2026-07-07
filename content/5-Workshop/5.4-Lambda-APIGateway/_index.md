---
title : "Lambda & API Gateway"
date : "2026-07-06"
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

#### 4 Lambda functions (Node.js 20, arm64)

| Function | Responsibility |
|---|---|
| `job-tracker-crud-job` | POST/PUT/DELETE /jobs — create, update, delete jobs |
| `job-tracker-get-jobs` | GET /jobs, GET /jobs/{jobId} — list and detail |
| `job-tracker-cv-presigned` | POST /jobs/{jobId}/cv-url — issue Presigned URLs for CV upload/download |
| `lambda-followup-checker` | Scan due jobs and send reminder emails (triggered by EventBridge) |

Security principles in the code:

- `userId` always comes from `event.requestContext.authorizer.jwt.claims.sub` (the JWT already validated by API Gateway) — **never trust client-supplied data**
- PUT/DELETE use `ConditionExpression: attribute_exists(jobId)` with the `{userId, jobId}` key — nobody can modify another user's job
- Each Lambda has its own **least-privilege** IAM inline policy (e.g. the Get Lambda only has `dynamodb:Query`/`GetItem`)

#### API Gateway — HTTP API

We chose an **HTTP API** over a REST API: ~70% cheaper, one-step CORS configuration, and a native JWT authorizer for Cognito.

- 6 routes: `GET/POST /jobs`, `GET/PUT/DELETE /jobs/{jobId}`, `POST /jobs/{jobId}/cv-url`
- **JWT authorizer** `cognito-jwt`: Issuer = User Pool, Audience = Client ID, attached to **all** routes
- CORS: Allow-Origin restricted to the frontend domain

![API Gateway routes](/images/capstone/apigw-routes.png)

#### Testing with Postman

The whole API was tested with a Postman collection (JWT obtained via Cognito `InitiateAuth`, auto-saved by a post-response script):

![Postman 401 without token](/images/capstone/postman-401.png)

{{% notice tip %}}
**Lesson learned: defense in depth.** During testing, the `POST /jobs/{jobId}/cv-url` route was accidentally left without an authorizer. Because the Lambda has its own `userId` check, requests without a JWT were still rejected with 401 — a configuration gap did not leak any data. We then audited all 6 routes for the JWT Auth badge.
{{% /notice %}}
