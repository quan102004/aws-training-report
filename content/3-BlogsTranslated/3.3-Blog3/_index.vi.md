---
title: "Blog 3: Phân tích thời gian thực với Amazon Aurora & QuickSight"
date: 2026-06-29
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

### [DATA/Architecture] TÁCH BẠCH DỮ LIỆU ĐỂ PHÂN TÍCH THỜI GIAN THỰC: BÀI HỌC TỪ OLDCASTLE VỚI AMAZON AURORA & QUICKSIGHT

Chào các anh chị em cộng đồng,

Trong doanh nghiệp sản xuất hay logistics, dữ liệu vận hành thay đổi từng giây. Việc trích xuất dữ liệu từ các hệ thống ERP lõi lên các Dashboard thời gian thực (Real-time Analytics) mà không làm "sập" hay chậm hệ thống đang chạy luôn là một cơn đau đầu trong thiết kế kiến trúc đám mây.

Một case study cực kỳ điển hình giải quyết trọn vẹn bài toán này vừa được AWS chia sẻ là của **Oldcastle APG** – một ông lớn cung cấp vật liệu xây dựng ở Bắc Mỹ với hơn 150 cơ sở. Khi chuyển hệ thống từ on-premises lên Infor Cloud ERP trên AWS, họ gặp một rào cản lớn: Tính năng báo cáo có sẵn của Infor Cloud ERP chỉ hỗ trợ số lượng báo cáo rất hạn chế. Người dùng ở các phòng ban phải đợi batch report (báo cáo chạy theo lô), gây trễ nải nghiêm trọng trong việc ra quyết định.

Thay vì chọc thẳng các công cụ BI vào ERP, Oldcastle đã chọn một hướng đi tối ưu hơn: **Xây dựng kiến trúc tách bạch hoàn toàn dữ liệu bằng Infor Data Fabric Stream Pipelines và các dịch vụ AWS.**

#### Kiến Trúc Data Streaming Thực Chiến Mượt Mà

![Kiến trúc phân tích thời gian thực với Amazon Aurora & QuickSight](/images/3-Blog/blog_3.jpg)
Ý tưởng ở đây là bắt (capture) dữ liệu thay đổi và đẩy ra ngoài ngay lập tức. Luồng xử lý cực kỳ chặt chẽ:

* **Bắt sự kiện (Ingestion):** Infor Data Fabric stream các thay đổi (insert, update, delete) ngay lập tức mà không cần đợi lưu vào data lake.
* **Giải quyết bài toán Network (Load Distribution):** Vì hệ thống Infor không thể truy cập trực tiếp vào private VPC, họ phải dùng Network Load Balancer (NLB) với Elastic IP tĩnh đặt ở public subnet. Đứng sau đó là các EC2 instance đóng vai trò RDS Router, dùng `iptables NAT rules` để forward traffic an toàn vào database nằm trong private subnet.
* **Quản lý kết nối (Connection Management):** Với luồng dữ liệu streaming tần suất cao, họ dùng **Amazon RDS Proxy** đặt giữa router và database để quản lý connection pool, chịu tải khi traffic tăng vọt và tự động chuyển đổi dự phòng (failover).
* **Lưu trữ linh hoạt (Storage):** Dữ liệu hạ cánh tại **Amazon Aurora PostgreSQL** (triển khai Multi-AZ). Một điểm kỹ thuật rất hay là họ lưu luồng dữ liệu streaming vào các cột `JSONB` để truy vấn linh hoạt, sử dụng hàm JSON native của Aurora khi cần parse dữ liệu.

#### Đưa Dashboard Vào Tận Tay Người Dùng
Phân tích xong thì phải hiển thị sao cho mượt. **Amazon QuickSight** được lựa chọn và tận dụng tối đa sức mạnh của bộ nhớ đệm SPICE để tăng tốc độ query.

Nhưng điều tuyệt vời nhất là cơ chế **Embedded Integration (Tích hợp nhúng)**. Thay vì bắt người dùng mở một đường link BI (Business Intelligence) khác, họ dùng Amazon API Gateway và AWS Lambda để xác thực, sau đó gọi API của QuickSight để tạo URL động (kèm phân quyền Row-Level Security). Kết quả là các Dashboard này được nhúng thẳng vào giao diện Infor OS quen thuộc của người dùng bằng `iframe`.

#### Kết Quả Thực Tế Đáng Nể
* Chỉ trong vòng 8 tháng, họ đã triển khai thành công hơn **50 dashboard** và báo cáo phức tạp.
* Hệ thống gánh được hơn **100 user truy cập đồng thời** và xử lý hàng triệu giao dịch mỗi ngày mà không hề suy giảm hiệu năng.

> Đây là một architecture pattern "chuẩn sách giáo khoa" cho các anh em đang làm việc với Cloud ERP, Data Analytics hay System Integration. Việc tách rời tầng phân tích khỏi hệ thống giao dịch (OLTP) không chỉ giải phóng tải cho ERP mà còn mở đường cho các tính năng AI/ML nâng cao sau này.

---
**Nguồn tham khảo:**
* **Link bài gốc:** [Real-time analytics with Infor Cloud ERP and AWS services](https://aws.amazon.com/blogs/architecture/real-time-analytics-with-infor-cloud-erp-and-aws-services/)
* **Link bài đăng trên group:** [Cộng đồng AWS Study Group FCAJ](https://www.facebook.com/groups/660548818043427/?multi_permalinks=2206817163416577)