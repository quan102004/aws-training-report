---
title : "Frontend React"
date : "2026-07-06"
weight : 6
chapter : false
pre : " <b> 5.6 </b> "
---

#### Công nghệ

- **Vite + React + TypeScript**, style bằng **Tailwind CSS v4**
- Gọi Cognito trực tiếp qua REST API (`InitiateAuth`, `SignUp`, `ConfirmSignUp`) bằng fetch — không cần thư viện Amplify
- Cấu hình (API URL, Client ID) tách vào `.env` (không commit), có `.env.example` cho thành viên mới
- Làm việc nhóm theo **branch-per-module + PR**: `feat/api-module`, `feat/auth-ui`, `feat/jobs-ui`...

#### Các màn hình

**Đăng nhập / Đăng ký / Xác nhận email** — tự đăng ký tài khoản qua Cognito, nhận mã 6 số:

![Màn đăng nhập](/images/capstone/ui-login.png)

**Quản lý đơn ứng tuyển** — danh sách với badge màu theo trạng thái, lọc theo trạng thái (đi thẳng vào query `?status=`), form tạo/sửa, modal xác nhận xoá, upload/tải CV:

![Màn quản lý job](/images/capstone/ui-jobs.png)

#### Xử lý token

- IdToken + RefreshToken lưu localStorage; app **tự refresh** bằng `REFRESH_TOKEN_AUTH` khi token còn dưới 2 phút → demo dài không bao giờ đứt phiên giữa chừng
- Mọi lời gọi API đi qua một hàm `call<T>()` duy nhất tự đính Bearer token

#### Cách ly dữ liệu

Đăng nhập 2 tài khoản trên 2 trình duyệt: mỗi người chỉ thấy job của mình — xác nhận cơ chế partition theo `userId` từ JWT hoạt động đúng.
