---
title : "Lưu trữ CV với Presigned URL"
date : "2026-07-06"
weight : 5
chapter : false
pre : " <b> 5.5 </b> "
---

#### S3 bucket riêng tư + KMS

Bucket `job-tracker-cv-tqt-2026` với **Block all public access bật toàn bộ**, mã hoá **SSE-KMS** (AWS managed key `aws/s3`, Bucket Key enabled để giảm chi phí gọi KMS). CORS chỉ cho phép PUT/GET từ domain frontend.

#### Luồng 7a–7b: upload/download trực tiếp

1. Client gọi `POST /jobs/{jobId}/cv-url` kèm JWT → Lambda kiểm tra job thuộc về đúng user → ký **Presigned URL** sống 5 phút
2. Client PUT/GET **trực tiếp với S3** bằng URL đó — file không đi qua Lambda, giảm tải và chi phí

CV lưu theo key `userId/jobId/ten-file.pdf` — mỗi user một "ngăn" riêng. Chỉ nhận file `.pdf`, Content-Type khoá cứng `application/pdf` trong chữ ký.

![Upload CV thành công](/images/capstone/s3-cv-uploaded.png)

#### Kiểm chứng bảo mật

Truy cập **Object URL trần** (không chữ ký) → S3 trả `AccessDenied`; chỉ Presigned URL còn hạn mới mở được file:

![AccessDenied với URL trần](/images/capstone/s3-access-denied.png)

{{% notice tip %}}
**Bài học khi test Presigned URL bằng Postman**: request PUT lên S3 phải **tắt Bearer token** (chữ ký đã nằm trong URL — hai cơ chế auth cùng lúc bị S3 từ chối) và header `Content-Type` phải khớp đúng giá trị đã ký.
{{% /notice %}}
