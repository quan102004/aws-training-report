---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 8:

* Thiết kế, triển khai và hoàn thiện dự án Capstone: **Serverless Job Application Tracker**.
* Tích hợp thành công các dịch vụ Serverless: API Gateway, Cognito, DynamoDB, Lambda, S3, Amplify, WAF, Route 53, SES và CloudWatch/CloudTrail.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 1 | - Khảo sát yêu cầu và thiết kế kiến trúc hệ thống tổng quan <br> - Thiết lập CSDL Amazon DynamoDB và cấu hình Amazon Cognito để quản lý người dùng | 08/06/2026 | 08/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 2 | - Phát triển các hàm AWS Lambda xử lý các tác vụ CRUD ứng tuyển việc làm <br> - Tích hợp và cấu hình Amazon API Gateway | 09/06/2026 | 09/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 3 | - Tạo S3 bucket lưu trữ CV <br> - Viết logic sinh Presigned URL để upload/download CV trực tiếp từ trình duyệt một cách an toàn | 10/06/2026 | 10/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4 | - Cấu hình Amazon SES để gửi email <br> - Thiết lập Amazon EventBridge Scheduler kích hoạt Lambda gửi thông báo nhắc nhở hằng ngày | 11/06/2026 | 11/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5 | - Triển khai ứng dụng Frontend lên AWS Amplify <br> - Cấu hình giám sát vận hành qua CloudWatch Alarm, SNS và ghi log kiểm toán qua CloudTrail | 12/06/2026 | 12/06/2026 | <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 8:

* Thiết kế và triển khai hoàn chỉnh ứng dụng **Serverless Job Application Tracker** hoạt động ổn định trên AWS, đáp ứng đầy đủ yêu cầu nghiệp vụ.
* Đảm bảo tính bảo mật cho hệ thống bằng cách phân quyền chi tiết với IAM, xác thực người dùng với Cognito và tích hợp WAF để chống lạm dụng.
* Hoàn thành triển khai luồng upload/download file CV an toàn qua S3 Presigned URL, giúp giảm tải băng thông cho máy chủ và tăng tốc độ xử lý.
* Xây dựng thành công cơ chế gửi email nhắc nhở tự động, đảm bảo người dùng luôn được thông báo đúng hạn follow-up.
* Cấu hình đầy đủ các hệ thống giám sát tự động giúp phát hiện sự cố nhanh chóng và theo dõi hoạt động hệ thống qua log kiểm toán (audit log).



