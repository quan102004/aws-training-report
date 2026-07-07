---
title : "Kết luận & Hướng phát triển"
date : "2026-07-06"
weight : 12
chapter : false
pre : " <b> 5.12 </b> "
---

#### Kết quả đạt được

- Hệ thống **serverless hoàn chỉnh 10 luồng** trên AWS: xác thực (Cognito + JWT authorizer), CRUD (Lambda + DynamoDB), lưu trữ CV bảo mật (S3 + KMS + Presigned URL), **nhắc nhở tự động chạy thật hằng ngày** (EventBridge + SES + DLQ), giám sát (CloudWatch Alarm → SNS) và audit (CloudTrail → S3)
- Frontend React + TypeScript + Tailwind hoàn chỉnh, tự refresh token, cách ly dữ liệu theo người dùng
- Chi phí phát triển thực tế **$0.85**, quy trình làm việc nhóm chuẩn Git branch + PR
- Các nguyên tắc bảo mật xuyên suốt: least privilege IAM, không Scan, không tin dữ liệu client, bucket private tuyệt đối, mã hoá at-rest

#### Bài học kinh nghiệm

- Phân biệt IdToken/AccessToken với JWT authorizer; key GSI không sửa được — thiết kế kỹ trước khi tạo
- Defense in depth cứu nhóm khi sót authorizer trên một route
- Account AWS mới có các giới hạn chống lạm dụng (CloudFront, SES sandbox) — cần tính vào kế hoạch dự án thực tế

#### Hướng phát triển

- **Infrastructure as Code** (Terraform) để tái tạo hạ tầng tự động
- Hoàn tất CloudFront + WAF + Route 53 khi account được verify; xin SES production access
- Xoá CV trên S3 khi xoá job (DeleteObject hoặc S3 Lifecycle rule)
- Cognito Groups cho API thống kê tổng hợp; CI/CD với GitHub Actions
