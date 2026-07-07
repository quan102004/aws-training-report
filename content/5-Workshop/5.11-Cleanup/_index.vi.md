---
title : "Dọn dẹp tài nguyên"
date : "2026-07-06"
weight : 11
chapter : false
pre : " <b> 5.11 </b> "
---

Sau khi bảo vệ xong, để tránh phát sinh chi phí (đặc biệt khi credits hết hạn), dọn tài nguyên theo thứ tự:

1. **EventBridge Scheduler**: xoá schedule `daily-followup-check` (dừng cron trước tiên)
2. **CloudFront**: Disable → chờ Deployed → Delete distribution (nếu đã tạo)
3. **API Gateway**: xoá `job-tracker-api`
4. **Lambda**: xoá 4 functions (role IAM đi kèm xoá trong IAM console)
5. **DynamoDB**: xoá bảng `JobTrackerJobs` (tắt Deletion protection trước)
6. **S3**: Empty rồi Delete từng bucket (CV, web, CloudTrail logs) — bucket phải rỗng mới xoá được
7. **CloudTrail**: xoá trail `job-tracker-trail`
8. **CloudWatch**: xoá alarm `api-5xx-alarm` và các log groups `/aws/lambda/...`
9. **SNS / SQS**: xoá topic `job-tracker-alerts` và queue `followup-dlq`
10. **Cognito**: xoá User Pool
11. **SES**: xoá các identity đã verify
12. Giữ lại: **Budget alert** (miễn phí, nên giữ) và repo GitHub

{{% notice tip %}}
Kiểm tra lần cuối bằng Billing → Bills sau 1–2 ngày: mọi dòng chi phí về 0 là dọn sạch.
{{% /notice %}}
