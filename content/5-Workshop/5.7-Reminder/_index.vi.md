---
title : "Nhắc nhở tự động (EventBridge + SES)"
date : "2026-07-06"
weight : 7
chapter : false
pre : " <b> 5.7 </b> "
---

#### Luồng 8: hoàn toàn tự động

**EventBridge Scheduler** (`daily-followup-check`, cron `0 9 * * ? *` timezone Asia/Saigon) → invoke **Lambda Follow-up Checker** → query GSI `FollowUpIndex` điều kiện `followUpStatus = PENDING AND followUpDate <= hôm nay` → gửi email nhắc qua **Amazon SES** → cập nhật job sang `NOTIFIED`.

![EventBridge schedule](/images/capstone/eventbridge-schedule.png)

#### Chống gửi trùng

Cron chạy mỗi ngày nhưng người dùng **không bị spam**: job sau khi nhắc chuyển `NOTIFIED` và bị loại khỏi query; khi người dùng đổi ngày follow-up, Lambda CRUD tự reset về `PENDING` để được nhắc lại theo hạn mới.

#### Xử lý lỗi — SQS Dead Letter Queue

Lambda cấu hình asynchronous invocation: lỗi thì retry 2 lần, vẫn thất bại thì message rơi vào queue **`followup-dlq`** — không mất dữ liệu, có thể xử lý lại sau.

#### Kết quả

Test tay trả về `{"checked": 2, "sent": 2}`, chạy lần hai trả `{"checked": 0, "sent": 0}` (chống trùng hoạt động). Sáng hôm sau, đúng 9:00, hệ thống **tự gửi email không cần thao tác nào**:

![Email nhắc nhở tự động](/images/capstone/reminder-email.png)

{{% notice note %}}
SES đang ở **sandbox mode** — chỉ gửi tới địa chỉ đã verify, phù hợp phạm vi demo (verify email các thành viên). Khi go-live thật sẽ xin production access.
{{% /notice %}}
