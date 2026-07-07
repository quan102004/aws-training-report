---
title : "Chuẩn bị"
date : "2026-07-06"
weight : 2
chapter : false
pre : " <b> 5.2 </b> "
---

#### Tài khoản và công cụ

- Tài khoản AWS (Free Tier với $200 promotional credits), region làm việc: **ap-southeast-1**
- IAM user riêng cho từng thành viên (không dùng root user)
- Node.js 20 LTS, Git, VS Code, Postman
- Repo GitHub làm việc nhóm theo quy trình **branch-per-module + Pull Request**

#### Budget alert — việc làm đầu tiên

Trước khi tạo bất kỳ tài nguyên nào, nhóm đặt **AWS Budget $5/tháng** gửi cảnh báo email — lớp bảo hiểm chống phát sinh chi phí ngoài ý muốn.

![Budget alert](/images/capstone/budget-alert.png)

#### Quy ước đặt tên

| Tài nguyên | Tên |
|---|---|
| DynamoDB table | `JobTrackerJobs` (GSI: `FollowUpIndex`) |
| Lambda | `job-tracker-crud-job`, `job-tracker-get-jobs`, `job-tracker-cv-presigned`, `lambda-followup-checker` |
| API Gateway (HTTP API) | `job-tracker-api` |
| S3 buckets | `job-tracker-cv-tqt-2026` (CV), bucket web, bucket CloudTrail logs |
| SQS | `followup-dlq` |
| SNS | `job-tracker-alerts` |
