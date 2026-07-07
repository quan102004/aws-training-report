---
title : "Chi phí"
date : "2026-07-06"
weight : 10
chapter : false
pre : " <b> 5.10 </b> "
---

#### Chi phí thực tế trong quá trình phát triển

Sau toàn bộ quá trình xây dựng và kiểm thử (hàng nghìn request API, hàng chục lần deploy Lambda, upload CV, email nhắc nhở):

| Hạng mục | Số tiền |
|---|---|
| Tổng chi phí phát sinh | **$0.85** |
| Được cover bởi Free Tier credits | $0.85 |
| **Thực trả** | **$0.00** |

![Billing thực tế](/images/capstone/billing.png)

![Credits còn lại](/images/capstone/credits.png)

#### Vì sao rẻ đến vậy?

- **DynamoDB On-demand, Lambda, API Gateway HTTP API**: tính tiền theo request — lượng request của giai đoạn phát triển nằm gọn trong free tier
- **HTTP API rẻ hơn REST API ~70%**; Lambda arm64 rẻ hơn x86 ~20%
- **S3 Bucket Key** giảm ~90% số lần gọi KMS
- Không có tài nguyên chạy 24/7 (không EC2, không NAT Gateway, không VPC)

#### Ước tính khi vận hành thật (1.000 người dùng hoạt động/tháng)

| Dịch vụ | Ước tính/tháng |
|---|---|
| Lambda + API Gateway | ~$1–3 |
| DynamoDB On-demand | ~$2–5 |
| S3 (CV) + CloudFront | ~$1–3 |
| Cognito | $0 (dưới 10.000 MAU) |
| SES + SNS + CloudWatch | ~$1 |
| **Tổng** | **~$5–12/tháng** |

Kiến trúc serverless cho phép chi phí **tăng tuyến tính theo người dùng thật** thay vì trả cố định cho server nhàn rỗi.
