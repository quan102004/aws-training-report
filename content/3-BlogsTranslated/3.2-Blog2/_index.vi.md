---
title: "Blog 2: Kiểm soát truy cập an toàn cho ứng dụng RAG đa người dùng"
date: 2026-06-22
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

### [SECURITY/Architecture] KIỂM SOÁT TRUY CẬP AN TOÀN CHO ỨNG DỤNG RAG ĐA NGƯỜI DÙNG VỚI AMAZON BEDROCK VÀ VERIFIED PERMISSIONS

Chào các anh chị em cộng đồng,

Xây dựng các ứng dụng Generative AI nội bộ sử dụng kỹ thuật RAG (Retrieval-Augmented Generation) luôn là một chủ đề hấp dẫn nhưng đầy thách thức về mặt kiến trúc và bảo mật. Chúng ta đều biết việc cá nhân hóa quyền truy cập tài liệu là bắt buộc (ví dụ: nhân sự phòng HR chỉ được xem tài liệu HR, Sales xem tài liệu Sales), nhưng việc triển khai luồng phân quyền này vào thực tế hạ tầng lại không hề đơn giản.

Nhiều hệ thống hiện nay phải chọn cách tạo ra các Knowledge Base (cơ sở tri thức) riêng biệt cho từng phòng ban. Rào cản lớn nhất của cách làm này là hạ tầng bị nhân bản một cách cồng kềnh, chi phí duy trì tăng vọt và kéo theo cơn ác mộng về quản lý khi tổ chức có sự thay đổi.

Gần đây, khi nghiên cứu các mẫu kiến trúc mạng đám mây và bảo mật dữ liệu, mình muốn giới thiệu với mọi người một hướng tiếp cận giúp giải quyết triệt để nút thắt này. Thay vì chia cắt vật lý, chúng ta có thể sử dụng một Knowledge Base duy nhất và kiểm soát quyền truy cập bằng sự kết hợp giữa **Amazon Bedrock** và **Amazon Verified Permissions**.

#### Kiến Trúc Bảo Mật Đa Lớp (Defense-in-Depth)

![Kiến trúc bảo mật RAG đa người dùng](/images/3-Blog/blog_2.jpg)
Ý tưởng cốt lõi của mẫu kiến trúc này là tách biệt hoàn toàn logic ủy quyền ra khỏi mã nguồn ứng dụng và áp dụng tự động hóa bảo mật ở hai tầng độc lập:

* **1. Tầng 1 (API Access) - Chặn ngay từ cửa:** Khi người dùng gửi request, hệ thống không đi thẳng vào database. Amazon API Gateway sẽ gọi một Lambda Authorizer để kiểm tra với Verified Permissions xem người dùng này (dựa trên nhóm trong JWT token) có quyền gọi API hay không. Nếu không hợp lệ, request bị từ chối ngay lập tức, giảm thiểu rủi ro bị tấn công trực diện.
* **2. Tầng 2 (Document Access) - Bộ lọc dữ liệu tận gốc:** Nếu vượt qua được cửa đầu tiên, một Middleware Lambda sẽ tiếp tục gọi Verified Permissions lần thứ hai để xác định chính xác người dùng được phép xem tài liệu của những phòng ban nào. Từ quyết định này, hệ thống tự động tạo ra một bộ lọc (Metadata Filter) và truyền thẳng vào API `RetrieveAndGenerate` của Amazon Bedrock. Nhờ vậy, mô hình ngôn ngữ (LLM) chỉ có thể tìm kiếm và tạo ra câu trả lời dựa trên những tài liệu đã được khoanh vùng nghiêm ngặt. Dù Tầng 1 có vô tình bị cấu hình sai, Tầng 2 vẫn chặn đứng nguy cơ rò rỉ dữ liệu chéo.

#### Quản Lý Chính Sách Tập Trung Bằng Cedar
Toàn bộ logic phân quyền được viết bằng ngôn ngữ **Cedar** trực quan. Khi cần cấp quyền cho một phòng ban mới hoặc một nhân sự cấp cao, chúng ta chỉ cần cập nhật policy trên console mà không cần viết lại mã hay redeploy ứng dụng. Hệ thống tuân thủ chặt chẽ nguyên tắc "Deny-by-default", tự động đóng băng truy cập nếu service check quyền bị lỗi.

Hướng tiếp cận này giúp các tổ chức có thể nhanh chóng triển khai một ứng dụng GenAI an toàn, phục vụ hàng chục phòng ban mà vẫn tiết kiệm tối đa chi phí vận hành.

Để hiểu rõ hơn về cách triển khai thực tế, bài viết trên AWS Architecture Blog đã phân tích rất chất lượng mẫu kiến trúc này. Nếu các anh chị em đang có ý định xây dựng hoặc nâng cấp hệ thống AI nội bộ, mình khuyên mọi người nên dành chút thời gian đọc bài viết gốc để nắm bắt các khía cạnh kỹ thuật sâu hơn.

Rất mong bài chia sẻ này mang lại góc nhìn hữu ích cho các anh chị em làm Cloud Networking và System Architecture.

---
**Nguồn tham khảo:**
* **Link bài gốc:** [Secure multi-tenant RAG with Amazon Bedrock and Verified Permissions](https://aws.amazon.com/vi/blogs/architecture/secure-multi-tenant-rag-with-amazon-bedrock-and-verified-permissions/)
* **Link bài đăng trên group:** [Cộng đồng AWS Study Group FCAJ](https://www.facebook.com/groups/660548818043427/?multi_permalinks=2202713613826932)