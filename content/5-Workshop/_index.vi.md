---
title: "Workshop"
date: "2026-07-06"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Serverless Job Application Tracker

#### Tổng quan

Đề tài capstone của nhóm là xây dựng **Serverless Job Application Tracker** — hệ thống hỗ trợ người dùng quản lý và theo dõi quá trình ứng tuyển việc làm, triển khai hoàn toàn theo kiến trúc serverless trên AWS, region **ap-southeast-1 (Singapore)**.

Chức năng chính:

- Tạo, theo dõi và cập nhật trạng thái từng đơn ứng tuyển (Đã nộp / Phỏng vấn / Offer / Từ chối)
- Đính kèm CV (PDF) cho mỗi đơn, upload/download **trực tiếp với S3 qua Presigned URL**
- **Tự động gửi email nhắc nhở** khi đơn đến hạn follow-up (cron 9:00 sáng hằng ngày)
- Giám sát vận hành (CloudWatch Alarm → SNS) và audit toàn bộ API call (CloudTrail)

#### Kiến trúc

![Architecture Diagram](/images/capstone/architecture-v6.png)

Hệ thống gồm 10 luồng chính, được đánh số trên sơ đồ và trình bày chi tiết trong từng mục con.

#### Nội dung

{{% children /%}}
