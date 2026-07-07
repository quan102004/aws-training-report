---
title : "Lambda & API Gateway"
date : "2026-07-06"
weight : 4
chapter : false
pre : " <b> 5.4 </b> "
---

#### 4 Lambda function (Node.js 20, arm64)

| Function | Nhiệm vụ |
|---|---|
| `job-tracker-crud-job` | POST/PUT/DELETE /jobs — tạo, sửa, xoá job |
| `job-tracker-get-jobs` | GET /jobs, GET /jobs/{jobId} — danh sách và chi tiết |
| `job-tracker-cv-presigned` | POST /jobs/{jobId}/cv-url — cấp Presigned URL upload/download CV |
| `lambda-followup-checker` | Quét job đến hạn, gửi email nhắc (trigger bởi EventBridge) |

Các nguyên tắc bảo mật trong code:

- `userId` luôn lấy từ `event.requestContext.authorizer.jwt.claims.sub` (JWT đã được API Gateway xác thực) — **không tin dữ liệu client gửi lên**
- PUT/DELETE dùng `ConditionExpression: attribute_exists(jobId)` với key `{userId, jobId}` — không thể sửa/xoá job của người khác
- Mỗi Lambda có IAM inline policy riêng theo **least privilege** (ví dụ Lambda Get chỉ có `dynamodb:Query`/`GetItem`)

#### API Gateway — HTTP API

Nhóm chọn **HTTP API** thay vì REST API: rẻ hơn ~70%, cấu hình CORS một bước, và JWT authorizer tích hợp Cognito trực tiếp.

- 6 routes: `GET/POST /jobs`, `GET/PUT/DELETE /jobs/{jobId}`, `POST /jobs/{jobId}/cv-url`
- **JWT authorizer** `cognito-jwt`: Issuer = User Pool, Audience = Client ID, gắn vào **tất cả** routes
- CORS: giới hạn Allow-Origin theo domain frontend

![API Gateway routes](/images/capstone/apigw-routes.png)

#### Kiểm thử bằng Postman

Toàn bộ API được test bằng Postman collection (lấy JWT qua Cognito `InitiateAuth`, script tự lưu token):

![Postman 401 khi không có token](/images/capstone/postman-401.png)

{{% notice tip %}}
**Bài học: defense in depth.** Trong quá trình test, route `POST /jobs/{jobId}/cv-url` bị sót chưa gắn authorizer. Nhờ Lambda có lớp kiểm tra `userId` riêng, request không có JWT vẫn bị chặn với 401 — lỗ hổng cấu hình không dẫn đến lộ dữ liệu. Sau đó nhóm rà soát đủ 6 routes đều có badge JWT Auth.
{{% /notice %}}
