---
title : "Worklog Tuần 11"
date : "2026-06-29"
weight : 11
chapter : false
pre : " <b> 1.11. </b> "
---

### Mục tiêu tuần 11:

- Hoàn thiện phần lưu trữ CV, luồng nhắc lịch và tầng giám sát.
- Xây dựng giao diện React và hoàn thiện sơ đồ kiến trúc.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Tạo bucket lưu CV với mã hoá KMS khi lưu trữ<br>- Viết hàm Lambda sinh presigned URL cho việc tải lên và tải xuống | 29/06/2026 | 29/06/2026 | |
| 3 | - Cấu hình EventBridge Scheduler để kích hoạt kiểm tra follow-up hằng ngày<br>- Xác thực địa chỉ gửi trong SES và gửi email nhắc lịch | 30/06/2026 | 30/06/2026 | |
| 4 | - Gắn SQS dead-letter queue cho hàm Lambda nhắc lịch<br>- Tạo CloudWatch alarm và gửi thông báo qua SNS<br>- Bật CloudTrail để ghi nhật ký kiểm toán | 01/07/2026 | 01/07/2026 | |
| 5 | - Xây dựng giao diện React: danh sách đơn, lọc theo trạng thái, thêm/sửa/xoá, tải CV lên | 02/07/2026 | 02/07/2026 | |
| 6 | - Hoàn thiện sơ đồ kiến trúc sau nhiều vòng rà soát<br>- Áp dụng góp ý về đánh số luồng, định tuyến đường nối và vị trí đặt WAF | 03/07/2026 | 03/07/2026 | |

### Kết quả đạt được tuần 11:

- Hoàn thiện phần lưu trữ CV: tệp được mã hoá bằng KMS và tải lên trực tiếp từ trình duyệt thông qua presigned URL.
- Hoàn thiện luồng nhắc lịch: EventBridge Scheduler đến Lambda đến SES, kèm SQS dead-letter queue hứng các lần gọi thất bại.
- Bổ sung tầng giám sát: CloudWatch alarm, thông báo qua SNS và nhật ký kiểm toán CloudTrail.
- Hoàn thành giao diện React đáp ứng đầy đủ vòng đời của một đơn ứng tuyển.
- Chỉnh sửa sơ đồ kiến trúc qua nhiều phiên bản, và rút ra rằng sơ đồ là một công cụ truyền đạt — việc đánh số luồng và sắp xếp đường nối gọn gàng quan trọng không kém bản thân các thành phần.
