---
title : "Cognito & DynamoDB"
date : "2026-07-06"
weight : 3
chapter : false
pre : " <b> 5.3 </b> "
---

#### Amazon Cognito — xác thực người dùng

Tạo **User Pool** với đăng nhập bằng email, app client dạng SPA (không có client secret). Người dùng tự đăng ký, nhận mã xác nhận 6 số qua email và kích hoạt tài khoản.

![Cognito User Pool](/images/capstone/cognito-pool.png)

Để test bằng Postman, nhóm bật thêm auth flow `ALLOW_USER_PASSWORD_AUTH` cho app client.

{{% notice tip %}}
**Bài học: IdToken vs AccessToken.** JWT authorizer của API Gateway cấu hình Audience = Client ID, mà chỉ **IdToken** mới chứa claim `aud`. Dùng nhầm AccessToken sẽ nhận 401 dù token hoàn toàn hợp lệ — nhóm mất một buổi debug để rút ra điều này.
{{% /notice %}}

#### DynamoDB — lưu trữ dữ liệu job

Bảng `JobTrackerJobs`, capacity mode **On-demand**, mã hoá at-rest bằng AWS managed KMS key:

- **Partition key**: `userId` (String) — lấy từ claim `sub` trong JWT
- **Sort key**: `jobId` (String) — UUID sinh khi tạo job

![DynamoDB table](/images/capstone/dynamodb-table.png)

**GSI `FollowUpIndex`** phục vụ luồng nhắc nhở:

- Partition key: `followUpStatus` (PENDING / NOTIFIED / NONE)
- Sort key: `followUpDate` (YYYY-MM-DD)

Nhờ GSI này, Lambda nhắc nhở **query đúng các job PENDING đến hạn** thay vì Scan cả bảng.

{{% notice warning %}}
**Bài học: key của GSI không sửa được.** Lần đầu nhóm tạo nhầm partition key là `followUpFlag`, Lambda báo `ValidationException: Query condition missed key schema element`. Phải xoá index và tạo lại đúng tên `followUpStatus` — thao tác xoá index không ảnh hưởng dữ liệu trong bảng.
{{% /notice %}}
