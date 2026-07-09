---
title : "Worklog Tuần 10"
date : "2026-06-22"
weight : 10
chapter : false
pre : " <b> 1.10. </b> "
---

### Mục tiêu tuần 10:

- Xây dựng phần backend cốt lõi: xác thực, cơ sở dữ liệu và tầng API.
- Gỡ các lỗi tích hợp đầu tiên giữa các dịch vụ.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Tạo Cognito User Pool và app client<br>- Kiểm thử luồng đăng ký và đăng nhập | 22/06/2026 | 22/06/2026 | |
| 3 | - Thiết kế schema cho bảng DynamoDB<br>- Tạo Global Secondary Index phục vụ truy vấn follow-up | 23/06/2026 | 23/06/2026 | |
| 4 | - Viết bốn hàm Lambda: xem danh sách, tạo, cập nhật và xoá đơn ứng tuyển | 24/06/2026 | 25/06/2026 | |
| 5 | - Tạo HTTP API trên API Gateway<br>- Gắn JWT authorizer dựa trên Cognito User Pool | 25/06/2026 | 26/06/2026 | |
| 6 | - Kiểm thử toàn bộ route bằng Postman<br>- Sửa các lỗi phát sinh khi tích hợp | 26/06/2026 | 27/06/2026 | |

### Kết quả đạt được tuần 10:

- Hoàn thành luồng xác thực bằng Cognito và bảo vệ API bằng JWT authorizer.
- Xây dựng xong bảng DynamoDB kèm GSI, cùng bốn hàm Lambda phía sau.
- Gỡ được ba lỗi đáng ghi nhận:
  * **Sai partition key của GSI** — index được tạo trên `followUpFlag` trong khi thuộc tính ghi vào item lại là `followUpStatus`, khiến truy vấn trả về rỗng mà không báo lỗi.
  * **Thiếu JWT authorizer trên route `cv-url`** — các route khác đều được bảo vệ, riêng route này bị bỏ sót.
  * **Postman gửi sai loại token** — gửi `AccessToken` trong khi JWT authorizer của API Gateway yêu cầu `IdToken`.
- Rút ra bài học: kết quả rỗng thầm lặng từ DynamoDB thường là lỗi schema chứ không phải lỗi dữ liệu.
