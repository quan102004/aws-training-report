---
title : "Worklog Tuần 12 "
date : "2026-07-06"
weight : 12
chapter : false
pre : " <b> 1.12. </b> "
---

### Mục tiêu tuần 12:

- Triển khai hệ thống lên môi trường production và gắn tên miền riêng.
- Hoàn thành bảng ước tính chi phí, tài liệu workshop và bài thuyết trình cuối khoá.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Thử triển khai giao diện qua CloudFront<br>- Chuyển sang AWS Amplify Hosting sau khi distribution bị chặn do tài khoản mới chưa xác minh | 06/07/2026 | 06/07/2026 | |
| 3 | - Luyện tập và trình bày bài bảo vệ dự án cuối khoá<br>- Trình bày kiến trúc và demo hệ thống đang chạy | 07/07/2026 | 07/07/2026 | |
| 4 | - Lập bảng ước tính chi phí cho toàn bộ dịch vụ đã sử dụng | 08/07/2026 | 08/07/2026 | |
| 5 | - Đăng ký tên miền riêng và tạo public hosted zone trên Route 53<br>- Uỷ quyền DNS bằng cách trỏ nameserver của nhà đăng ký về Route 53<br>- Gắn tên miền vào Amplify Hosting và cấp chứng chỉ ACM | 09/07/2026 | 09/07/2026 | |
| 6 | - Cập nhật danh sách origin được phép trên API Gateway, S3 và Cognito cho tên miền mới<br>- Viết tài liệu workshop và hướng dẫn dọn dẹp tài nguyên | 10/07/2026 | 10/07/2026 | |

### Kết quả đạt được tuần 12:

- Triển khai thành công ứng dụng qua AWS Amplify Hosting phục vụ hoạt động production ổn định.
- Cấu hình hosted zone trên Route 53, uỷ quyền tên miền từ nhà đăng ký ngoài và cấp SSL qua ACM thành công.
- Lập bảng ước tính chi phí chi tiết, xác thực hệ thống nằm hoàn toàn trong gói Free Tier của AWS.
- Hoàn thành bài thuyết trình bảo vệ dự án cuối khoá, làm rõ các quyết định thiết kế kiến trúc và giải pháp.
- Viết đầy đủ tài liệu workshop và hướng dẫn dọn dẹp tài nguyên.
