---
title : "CloudFront, WAF & Route 53"
date : "2026-07-06"
weight : 9
chapter : false
pre : " <b> 5.9 </b> "
---

#### Thiết kế tầng edge (luồng 1–2)

Trong kiến trúc đầy đủ, giao diện React build tĩnh được lưu trên **S3 bucket riêng tư** (Block all public access) và phân phối qua **Amazon CloudFront**:

- **Origin Access Control (OAC)**: chỉ CloudFront được đọc bucket qua bucket policy — bucket không mở public dưới bất kỳ hình thức nào
- **AWS WAF** gắn vào CloudFront dưới dạng rule set: request được đối chiếu với managed rules (SQLi, XSS, bot...) ngay tại edge, hợp lệ mới cho qua — bảo vệ cả static content lẫn API
- **Default root object** `index.html` + custom error response 403/404 → `/index.html` (code 200) để hỗ trợ SPA routing
- **Route 53** đảm nhận DNS cho domain riêng, trỏ alias record về CloudFront

![Cấu hình CloudFront](/images/capstone/cloudfront-config.png)

#### Trạng thái triển khai thực tế

{{% notice warning %}}
Tài khoản AWS của nhóm (tạo mới trong năm 2026) đang bị giới hạn tạo CloudFront distribution theo cơ chế **chống lạm dụng với account mới** của AWS: *"Your account must be verified before you can add new CloudFront resources"*. Nhóm đã mở support case và được **escalate lên specialized program support team** (có xác nhận bằng văn bản từ AWS Support). Đây không phải lỗi cấu hình hay thanh toán — billing của account hợp lệ và các dịch vụ khác hoạt động bình thường.
{{% /notice %}}

![Support case escalation](/images/capstone/support-case.png)

Toàn bộ cấu hình CloudFront (plan Free, OAC, WAF, error pages) đã được nhóm chuẩn bị và thực hiện đến bước cuối của wizard. Ngay khi account được verify, việc hoàn tất chỉ mất ~15 phút và **không thay đổi bất kỳ thành phần nào khác** của hệ thống.

Trong phạm vi demo, ứng dụng được trình diễn qua môi trường dev (frontend local kết nối backend AWS thật) — toàn bộ luồng 3→10 hoạt động đầy đủ.

#### Quyết định về Route 53

Nhóm đã tìm hiểu và xác nhận: **phí đăng ký domain không được trừ vào promotional credits** (khoản pass-through trả cho registry). Với phạm vi demo, nhóm quyết định dùng domain mặc định của CloudFront — chi phí bằng 0, kiến trúc không đổi. Đây là quyết định theo đúng trụ cột **Cost Optimization** của Well-Architected Framework: chỉ trả cho thứ tạo giá trị ở giai đoạn hiện tại.
