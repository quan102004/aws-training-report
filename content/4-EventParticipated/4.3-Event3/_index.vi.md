---
title: "Sự kiện 3 - FCAJ Community Day Tháng 6/2026"
date: 2026-06-27
weight: 4
chapter: false
pre: " <b> 4.3. </b> "
---

| Thông tin | Chi tiết |
|---|---|
| Ngày | 27/06/2026 |
| Địa điểm | Tầng 26, Tòa nhà Bitexco Financial Tower, Phường Sài Gòn, TP.Hồ Chí Minh |
| Vai trò | Người tham dự |

Trang này tổng hợp nội dung từ sự kiện **FCAJ Community Day tháng 6/2026**, tập trung vào các giải pháp thực tế: đưa AI vào quy trình vận hành hệ thống, tối ưu hóa hạ tầng và bảo mật dữ liệu ở quy mô doanh nghiệp lớn.

---

### Bảng tổng hợp các chủ đề tham luận chính

| Diễn giả | Chủ đề chia sẻ | Từ khóa kỹ thuật cốt lõi |
|---|---|---|
| Anh Steve Trần | Vận hành hạ tầng Cloud và Nền tảng Agentic | Agentic Platform, Multi-Agent, FinOps, Incident Investigation |
| Anh Hiếu Nghị, Anh Kiệt, Anh Trung | Trợ lý thoại Voice AI Assistant cho doanh nghiệp | STT, TTS, Bedrock Agent Core, Tool Calling |
| Chị Bảo, Anh Nguyên Nguyễn | Ứng dụng DevOps AI Agent thực tế trên AWS | DevOps Agent, MCP, Topology, RCA |
| Anh Trường, Chị Minh Anh | Tối ưu hóa quy trình nhân sự bằng Amazon Q | Amazon Q, CV Screening, Token Optimization, No-code App |
| Anh Toàn Nguyễn, Anh Hiếu Nghị | Private Security cho Amazon Q và MCP Server | VPC Connection, Private Subnet, Route 53 Resolver, ALB, Zero Trust |

---

### 1. Anh Steve Trần (Cloud Thinker) - Vận hành hạ tầng Cloud và kỷ nguyên Nền tảng Agentic

Khi doanh nghiệp chuyển dịch sang kiến trúc Microservices, hệ thống ngày càng phình to và trở nên phức tạp hơn. Diễn giả chỉ ra rằng các đội nhóm vận hành hiện tại đang bị quá tải bởi các công cụ giám sát (Observability tools) tách biệt, kèm theo đó là những phần &ldquo;nợ công nghệ&rdquo; tích tụ từ các hệ thống cũ. Nền tảng thông minh được đưa vào với vai trò hỗ trợ các kỹ sư Senior xử lý nhanh sự cố, giảm thiểu tối đa thời gian hệ thống bị gián đoạn (down-time).

**Nền tảng Agentic giải quyết 4 bài toán cốt lõi:**

| Bài toán | Mô tả |
|---|---|
| Incident Investigation | Tự động điều tra sự cố tốc độ cao, đọc log hệ thống tính bằng phút thay vì bằng giờ |
| Code Reviews | Rà soát tự động các thay đổi mã nguồn hạ tầng trước khi đưa lên Production |
| FinOps | Tối ưu hóa chi phí vận hành thông qua hiểu sâu cả hạ tầng đám mây lẫn dòng tiền doanh nghiệp |
| Security | Mô phỏng hành vi hacker để tự động hóa Pentesting và đánh giá cấu hình hệ thống |

**So sánh Single Agent vs Multi-Agent:**
- **Single Agent**: Nếu được thiết kế đủ tốt, hoàn toàn có thể xử lý mượt mà trên 95% tác vụ
- **Multi-Agent**: Ưu thế nhờ phân rã công việc cho các tác nhân chuyên biệt (Specialist agents), tối ưu hóa dung lượng ngữ cảnh và quản lý phân quyền (Role-Based Access Control) chặt chẽ

---

### 2. Anh Hiếu Nghị, Anh Kiệt và Anh Trung - Từng bước xây dựng trợ lý thoại Voice AI Assistant cho khối doanh nghiệp

Mảng Voice AI tại Việt Nam đang đứng trước cơ hội rất lớn do nguồn dữ liệu giọng nói chuẩn hóa phục vụ huấn luyện còn tương đối khan hiếm. Hai hướng đi phổ biến về kiến trúc:

**Hai hướng tiếp cận:**
- **Speech-to-Speech**: Dịch trực tiếp từ âm thanh sang âm thanh - rất tiềm năng nhưng hiện tại chủ yếu mới hỗ trợ tốt tiếng Anh
- **STT + LLM + TTS** (Giải pháp tối ưu cho tiếng Việt): Speech-to-Text chuyển giọng nói thành văn bản, LLM xử lý ngữ cảnh, Text-to-Speech phản hồi bằng âm thanh tự nhiên

**Ưu điểm cho môi trường doanh nghiệp (ví dụ ngành Ngân hàng):**
- Đưa dữ liệu qua định dạng văn bản trung gian giúp kiểm soát nội dung (Guardrails), hạn chế AI đưa thông tin sai lệch
- Hệ thống thoại tự động gọi API (Tool calling) theo thời gian thực để thực hiện tác vụ như khóa thẻ, xác thực thông tin khách hàng

**Các bài toán thực tế trên Production:**
- Sử dụng cơ chế truyền phát (Streaming) để giảm độ trễ
- Bổ sung dữ liệu giọng nói vùng miền (Accent)
- Tích hợp mô hình nhận diện giới tính để xưng hô phù hợp
- Xử lý tình huống ngắt lời ngẫu nhiên từ người dùng
- Tự động chuyển tiếp cuộc gọi sang nhân viên tổng đài khi vượt quá khả năng xử lý

---

### 3. Chị Bảo và Anh Nguyên Nguyễn (Cloud Kinetics) - Hiện thực hóa DevOps AI Agent trên môi trường AWS

Trong các hệ thống quy mô lớn, mỗi khi xảy ra sự cố, các kỹ sư thường mất nhiều thời gian điều tra do dữ liệu giám sát bị phân tán ở nhiều công cụ khác nhau. Giải pháp DevOps AI Agent tự động hóa hoàn toàn quy trình này ngay khi nhận được cảnh báo lỗi từ hệ thống (ví dụ từ CloudWatch) hoặc từ yêu cầu trực tiếp của kỹ sư vận hành.

**6 trụ cột của hệ thống DevOps Agent:**

| Trụ cột | Mô tả |
|---|---|
| Context Learning | Tự động học kiến trúc hệ thống thông qua Agent Space để vẽ bản đồ Topology trực quan |
| Control | Phân quyền nghiêm ngặt, giới hạn chính xác khu vực hoạt động và tài nguyên của Agent |
| Integration | Mở rộng liên kết dữ liệu và hạ tầng qua giao thức MCP (Model Context Protocol) |
| Collaboration | Kết nối linh hoạt với Slack, Jira, Service Now |
| Convenient | Thao tác kích hoạt đơn giản, nhanh chóng trực tiếp trên giao diện AWS Console |
| Cost Effective | Tính giá minh bạch theo thời gian chạy thực tế (~0.083 USD/giây) thay vì tính theo token |

**Quy trình xử lý sự cố 4 bước:**
1. Phân loại sơ bộ lỗi
2. Điều tra tìm nguyên nhân gốc rễ (RCA)
3. Đề xuất phương án xử lý nhanh
4. Đề xuất cải tiến dài hạn để ngăn ngừa lỗi lặp lại

> DevOps Agent chỉ dừng lại ở bước đưa ra phương án xử lý cụ thể để các kỹ sư duyệt và thực thi bằng tay, không tự ý can thiệp trực tiếp vào môi trường Production.

---

### 4. Anh Trường và Chị Minh Anh (Noventic) - Ứng dụng Amazon Q để tự động hóa quy trình Nhân sự

Bộ phận nhân sự truyền thống thường đối mặt với gánh nặng sàng lọc hồ sơ lớn một cách thủ công, dễ bỏ sót nhân tài và quy trình đánh giá đôi khi mang tính cảm tính. Việc sử dụng các công cụ AI công cộng để phân tích hồ sơ luôn tiềm ẩn nguy cơ rò rỉ dữ liệu nội bộ. Amazon Q giải quyết bài toán này bằng cách cung cấp nền tảng trợ lý thông minh trong môi trường bảo mật nội bộ.

**Khả năng kết nối:** Tích hợp đa dạng với Microsoft Workspace, Google Workspace, Jira, Salesforce, GitHub nhờ giao thức MCP.

**Kịch bản tuyển dụng tự động được demo:**
1. Hệ thống tự động phân tích file hướng dẫn để tạo năng lực chuyên biệt &ldquo;HR talent review assistant&rdquo;
2. AI hỗ trợ soạn thảo bản mô tả công việc (JD), tự động quét toàn bộ hồ sơ trong thư mục (kể cả định dạng ảnh scan nhờ OCR)
3. Đối chiếu, phân loại ứng viên theo mức độ phù hợp (Strong, Good, Low, Very Low) dựa trên bộ tiêu chí kỹ thuật
4. Đề xuất dải lương tương ứng (Salary benchmark) và xuất báo cáo đánh giá HTML, quản lý tiến trình ứng tuyển qua ứng dụng no-code

---

### 5. Anh Toàn Nguyễn và Anh Hiếu Nghị (Renova Cloud) - Thiết lập mô hình Private Security cho Amazon Q và MCP Server

Mặc định, các ứng dụng như Amazon Q kết nối qua internet công cộng. Việc mở Public endpoints khi AI cần tương tác với MCP Server nội bộ tạo ra rủi ro bảo mật lớn như DDoS hay Man-in-the-middle. Thiết lập mô hình bảo mật riêng tư theo tiêu chuẩn Zero Trust là vô cùng cấp thiết.

**Giải pháp kiến trúc:**
- Cô lập hoàn toàn MCP Server bên trong Private Subnet của VPC
- Amazon Q thiết lập Interface Endpoint an toàn thông qua VPC Connection
- Lưu lượng truy cập điều hướng qua ALB trong mạng riêng để mã hóa bằng TLS
- Kết hợp AWS Certificate Manager (ACM) và xác thực qua Amazon Cognito
- Route 53 Resolver quản lý toàn bộ DNS nội bộ của MCP Server trong VPC, đảm bảo địa chỉ máy chủ hoàn toàn ẩn giấu trước internet bên ngoài

**Chi phí vận hành ước tính:** 250 - 350 USD/tháng

---

### 6. Hình ảnh từ sự kiện

![Hình ảnh tại Event 3](/images/4-Event/4.3-Event3/event3-photo.png)
![Hình ảnh tại Event 3](/images/4-Event/4.2-Event2/event2-photo.png)

---

### 7. Kết luận

Tổng thể sự kiện FCAJ Community Day tháng 6/2026 mang lại thông điệp rõ ràng: **Giá trị thực sự của AI nằm ở cách thiết kế hệ sinh thái và quy trình vận hành xung quanh nó**, chứ không chỉ ở bản thân mô hình công nghệ.

| Đối tượng | Thông điệp chính |
|---|---|
| Kỹ sư / Cá nhân | AI là công cụ hỗ trợ và khuếch đại năng lực mạnh mẽ, không thay thế hoàn toàn vai trò con người |
| Doanh nghiệp | Khi đưa AI vào Production, Data Governance, Guardrails và Private Security luôn là điều kiện tiên quyết |
