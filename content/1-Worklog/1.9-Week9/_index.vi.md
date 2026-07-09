---
title : "Worklog Tuần 9"
date : "2026-06-15"
weight : 9
chapter : false
pre : " <b> 1.9. </b> "
---

### Mục tiêu tuần 9:

- Hoàn thành đề cương dự án và đưa kiến trúc vào rà soát.
- Tìm hiểu cơ chế presigned URL của S3 dùng cho việc tải lên và tải xuống CV.

### Công việc thực hiện trong tuần:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu presigned URL của S3: cách sinh, thời hạn và cơ chế phân quyền | 15/06/2026 | 15/06/2026 | |
| 3 | - **Thực hành:** sinh presigned URL bằng AWS SDK for JavaScript v3<br>- Cấu hình CORS cho bucket để trình duyệt tải tệp lên | 16/06/2026 | 16/06/2026 | |
| 4 | - Viết đề cương dự án: mục tiêu, phạm vi, kiến trúc, danh sách dịch vụ | 17/06/2026 | 17/06/2026 | |
| 5 | - Gửi kiến trúc để rà soát nội bộ<br>- Nhận góp ý: thiếu IaC, bảng chi phí, dead-letter queue và presigned URL | 18/06/2026 | 18/06/2026 | |
| 6 | - Chỉnh sửa kiến trúc theo góp ý<br>- Vẽ lại sơ đồ và kiểm tra lại toàn bộ luồng dữ liệu | 19/06/2026 | 19/06/2026 | |

### Kết quả đạt được tuần 9:

- Hiểu được cách presigned URL cho phép trình duyệt làm việc trực tiếp với S3, tệp CV không cần đi qua Lambda.
- Rút ra rằng request `PUT` bằng presigned URL phải được gửi **không kèm** header `Authorization`, vì chữ ký đã nằm sẵn trong URL.
- Hoàn thành đề cương dự án.
- Nhận điểm rà soát khoảng 7.5/10, kèm các thiếu sót cụ thể: chưa có Infrastructure as Code, chưa có bảng ước tính chi phí, chưa có DLQ và chưa thiết kế presigned URL.
- Chỉnh sửa kiến trúc để mỗi thiếu sót được nêu trong buổi rà soát đều có thành phần tương ứng.
