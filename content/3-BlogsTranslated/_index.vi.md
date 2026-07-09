---
title: "Các bài blogs đã đăng"
date: 2026-06-30
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

###  [Blog 1 - Tư duy hạ tầng "miễn nhiễm" với Ransomware trên AWS](3.1-Blog1/)
Blog này đi sâu vào phân tích chiến lược xây dựng kiến trúc AWS phòng chống lại các chiến dịch tấn công Ransomware có tổ chức. Thay vì phụ thuộc vào các công cụ đắt tiền, bài viết nhấn mạnh tầm quan trọng của việc quy hoạch hạ tầng mạng để tự động bẻ gãy chuỗi lây lan của mã độc trong "72 giờ vàng" đầu tiên. Nội dung bóc tách 4 chốt chặn sinh tử: (1) Sử dụng IAM Temporary Elevated Access vô hiệu hóa rủi ro leo thang đặc quyền; (2) Triển khai VPC Endpoints thay cho NAT Gateway nhằm cô lập luồng mạng, chặn đứng kết nối về máy chủ C&C; (3) Áp dụng tư duy "Shift-Left" đưa công cụ rà quét vào thẳng pipeline CI/CD; và (4) Xây dựng trung tâm giám sát đồng nhất dựa trên kiến trúc AWS SRA. 

###  [Blog 2 - Kiểm soát truy cập an toàn cho ứng dụng RAG đa người dùng](3.2-Blog2/)
Blog này tập trung giải quyết một trong những bài toán hóc búa nhất khi xây dựng các ứng dụng Generative AI nội bộ: Kiểm soát quyền truy cập tài liệu RAG (Retrieval-Augmented Generation) cho nhiều phòng ban trên cùng một Knowledge Base. Thay vì nhân bản cơ sở tri thức gây tốn kém, bài viết giới thiệu mẫu kiến trúc bảo mật đa lớp (Defense-in-Depth) kết hợp giữa Amazon Bedrock và Amazon Verified Permissions. Luồng xác thực được chia làm hai chốt chặn độc lập: Tầng 1 sử dụng API Gateway và Lambda Authorizer để chặn request trái phép từ cửa; Tầng 2 sử dụng Metadata Filter động truyền vào API RetrieveAndGenerate để giới hạn tầm vực đọc của LLM. Toàn bộ logic phân quyền được quản lý tập trung bằng ngôn ngữ Cedar cực kỳ trực quan và bảo mật.

###  [Blog 3 - Tách bạch dữ liệu để phân tích thời gian thực với Aurora & QuickSight](3.3-Blog3/)
Blog này mang đến một case study thực chiến xuất sắc từ tập đoàn Oldcastle APG trong việc hiện thực hóa kiến trúc Phân tích Dữ liệu Thời gian thực (Real-time Analytics). Bài viết mổ xẻ cách đội ngũ kỹ sư đồng bộ dữ liệu từ hệ thống Infor Cloud ERP lõi lên Dashboard mà không làm suy giảm hiệu năng của các giao dịch OLTP. Điểm nhấn của kiến trúc nằm ở việc tách bạch hoàn toàn luồng dữ liệu thông qua Infor Data Fabric, kết hợp cùng Network Load Balancer, RDS Proxy và Amazon Aurora PostgreSQL để xử lý hàng triệu giao dịch an toàn qua Private Subnet. Cuối cùng, bài viết hướng dẫn cách ứng dụng Amazon QuickSight với cơ chế Embedded Integration để nhúng trực tiếp Dashboard động vào giao diện người dùng.