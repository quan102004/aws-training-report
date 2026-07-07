---
title : "CloudFront, WAF & Route 53"
date : "2026-07-06"
weight : 9
chapter : false
pre : " <b> 5.9 </b> "
---

#### Edge layer design (flows 1–2)

In the full architecture, the static React build is stored in a **private S3 bucket** (Block all public access) and served through **Amazon CloudFront**:

- **Origin Access Control (OAC)**: only CloudFront can read the bucket via its bucket policy — the bucket is never public in any form
- **AWS WAF** attached to CloudFront as a rule set: requests are checked against managed rules (SQLi, XSS, bots...) right at the edge — protecting both static content and the API
- **Default root object** `index.html` + custom error responses 403/404 → `/index.html` (code 200) for SPA routing
- **Route 53** handles DNS for a custom domain with an alias record pointing to CloudFront

![CloudFront configuration](/images/capstone/cloudfront-config.png)

#### Actual deployment status

{{% notice warning %}}
Our AWS account (newly created in 2026) is currently restricted from creating CloudFront distributions by AWS's **new-account abuse-prevention mechanism**: *"Your account must be verified before you can add new CloudFront resources"*. We opened a support case which was **escalated to the specialized program support team** (confirmed in writing by AWS Support). This is not a configuration or billing issue — the account's billing is valid and every other service works normally.
{{% /notice %}}

![Support case escalation](/images/capstone/support-case.png)

The full CloudFront configuration (Free plan, OAC, WAF, error pages) has been prepared and executed up to the final wizard step. Once the account is verified, completion takes ~15 minutes and **changes nothing else** in the system.

For the demo, the application runs in the dev environment (local frontend connected to the real AWS backend) — flows 3→10 are fully operational.

#### The Route 53 decision

We researched and confirmed that **domain registration fees are not covered by promotional credits** (a pass-through charge paid to the registry). For the demo scope we decided to use CloudFront's default domain — zero cost, identical architecture. This follows the **Cost Optimization** pillar of the Well-Architected Framework: only pay for what creates value at the current stage.
