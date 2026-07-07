---
title : "Giám sát & Audit"
date : "2026-07-06"
weight : 8
chapter : false
pre : " <b> 5.8 </b> "
---

#### Luồng 9: CloudWatch Alarm → SNS → Email admin

- Mọi log/metric của API Gateway và Lambda tự đổ về **CloudWatch** (log groups `/aws/lambda/...` là công cụ debug chính của nhóm suốt dự án)
- Alarm **`api-5xx-alarm`**: metric `5xx` của API, thống kê **Sum**, chu kỳ 5 phút, ngưỡng **≥ 5** → khi vượt, đẩy thông báo vào SNS topic **`job-tracker-alerts`** → email admin (subscription đã confirm)

![CloudWatch alarm](/images/capstone/cloudwatch-alarm.png)

Ngưỡng "5 lỗi 5xx / 5 phút" đủ nhạy để phát hiện sự cố thật, đủ trễ để không cảnh báo oan vì một lỗi lẻ.

#### Luồng 10: CloudTrail → S3 audit

Trail **`job-tracker-trail`** (multi-region) ghi **toàn bộ API call trong account** — không chỉ API Gateway mà cả thao tác với Lambda, DynamoDB, S3, Cognito, IAM... — lưu vào bucket S3 riêng `aws-cloudtrail-logs-...`.

![CloudTrail logging](/images/capstone/cloudtrail-logging.png)

Đây là điểm nhóm chú trọng vì có thành viên background bảo mật: khi có sự cố, Event history cho phép truy vết **ai, làm gì, lúc nào, từ đâu**.

#### Vai trò "admin" trong hệ thống

Ứng dụng **chủ đích không có role admin**: dữ liệu ứng tuyển và CV là thông tin nhạy cảm, nguyên tắc least privilege áp dụng cho cả người vận hành. Quản trị hệ thống thực hiện ở tầng hạ tầng (IAM, CloudWatch, CloudTrail). Hướng mở rộng: dùng Cognito Groups nếu cần API thống kê tổng hợp.
