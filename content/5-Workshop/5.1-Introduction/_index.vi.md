---
title : "Giới thiệu & Kiến trúc"
date : "2026-07-06"
weight : 1
chapter : false
pre : " <b> 5.1 </b> "
---

#### Bài toán

Người tìm việc thường nộp hàng chục đơn ứng tuyển cùng lúc và dễ bỏ lỡ thời điểm follow-up với nhà tuyển dụng. Nhóm xây dựng một ứng dụng web cho phép quản lý tập trung các đơn ứng tuyển, lưu CV theo từng đơn, và tự động nhắc nhở qua email.

#### Vì sao chọn serverless?

- **Không quản lý server**: toàn bộ dùng managed service (Lambda, DynamoDB, S3, Cognito...)
- **Tự động scale** theo lượng người dùng
- **Chi phí theo mức sử dụng** — phù hợp giai đoạn đầu khi người dùng chưa nhiều. Chi phí thực tế của nhóm trong suốt quá trình phát triển: **$0.85** (xem mục Chi phí)

#### Sơ đồ kiến trúc

![Architecture Diagram](/images/capstone/architecture-v6.png)

**10 luồng hoạt động chính:**

| # | Luồng | Dịch vụ |
|---|-------|---------|
| 1a–1b | Truy cập domain, kiểm tra WAF rules | Route 53, CloudFront, AWS WAF |
| 2 | Tải giao diện React (origin) | CloudFront ↔ S3 Static Website |
| 3 | Đăng nhập / nhận JWT | Amazon Cognito |
| 4a–4b | Gọi API kèm JWT, xác thực token | CloudFront → API Gateway ↔ Cognito |
| 5 | Route request đến Lambda theo chức năng | API Gateway → 3 Lambda |
| 6 | Đọc / ghi dữ liệu job | Lambda ↔ DynamoDB (+GSI) |
| 7a–7b | Cấp Presigned URL, upload/download CV trực tiếp | Lambda, S3 Private, KMS |
| 8a–8d | Cron 9:00 quét job đến hạn, gửi email nhắc | EventBridge → Lambda → SES (+SQS DLQ) |
| 9a–9d | Thu log, vượt ngưỡng thì cảnh báo admin | CloudWatch Alarm → SNS → Email |
| 10a–10b | Ghi log mọi API call phục vụ audit | CloudTrail → S3 |

#### Điểm nhấn thiết kế

- **Không có VPC**: kiến trúc thuần serverless, mọi dịch vụ là managed service được bảo vệ bằng IAM, WAF và KMS — giảm độ phức tạp và chi phí.
- **Không có Scan trên DynamoDB**: truy vấn người dùng đi theo partition key `userId`; luồng nhắc nhở query GSI `FollowUpIndex`.
- **Cách ly dữ liệu tuyệt đối**: `userId` lấy từ JWT đã được API Gateway xác thực, người dùng không thể đọc/sửa dữ liệu của người khác.
