---
title: "Workshop"
date: "2026-07-06"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Serverless Job Application Tracker

#### Overview

Our capstone project is a **Serverless Job Application Tracker** — a system that helps users manage and follow up on their job applications, built entirely on a serverless architecture on AWS in the **ap-southeast-1 (Singapore)** region.

Main features:

- Create, track and update the status of each job application (Applied / Interview / Offer / Rejected)
- Attach a CV (PDF) to each application, uploaded/downloaded **directly to S3 via Presigned URLs**
- **Automatic email reminders** when an application is due for follow-up (daily cron at 9:00 AM)
- Operational monitoring (CloudWatch Alarm → SNS) and full API auditing (CloudTrail)

#### Architecture

![Architecture Diagram](/images/capstone/architecture-v6.png)

The system consists of 10 main flows, numbered on the diagram and described in detail in the subsections below.

#### Content

{{% children /%}}
