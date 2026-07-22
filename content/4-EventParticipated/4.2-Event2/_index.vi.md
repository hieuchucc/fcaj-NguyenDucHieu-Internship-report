---
title: "Event 2"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Bài thu hoạch

### Mục Đích Của Sự Kiện

- Chia sẻ tư duy và khung ứng dụng hệ thống ngữ cảnh chuẩn (Context engineering) để tối ưu hóa hiệu suất mô hình AI.
- Giới thiệu giải pháp trợ lý thông minh và năng lực đại lý AI (Agentic AI) để tự động hóa quy trình làm việc doanh nghiệp.
- Cung cấp các giải pháp toàn diện của Amazon CloudFront nhằm tối ưu hóa chi phí CDN, tăng cường bảo mật và nâng cao hiệu năng mạng lưới.
- Chia sẻ hành trình thực tế phát triển sản phẩm ứng dụng giao diện thần kinh (Neural Interface) từ ý tưởng đến thực tế trong cuộc thi Hackathon.
- Phân tích nguyên nhân kỹ thuật gây ra hiện tượng mất tính nhất quán (non-determinism) của LLM và đề xuất chiến lược giảm thiểu rủi ro.
- Giới thiệu kiến trúc nhiều đại lý (Multi-Agent Paradigm) giải quyết bài toán đánh giá hồ sơ tài chính startup trong hệ thống ngân hàng. 

### Danh Sách Diễn Giả

- **Tinh Truong** - Platform Engineer, GoTymeX
- **Pham Nguyen Hai Anh** - G-AsiaPacific Vietnam, AWS Community Builder
- **Nguyen Tuan Thinh** - DevOps Engineer, First Cloud AI Journey
- LotusHacks 2026
- **Duc Dao** - Solution Architect, Cloud Kinetics
- **Vy Lam** - Senior Business Systems Analyst, VPBank  

### Nội Dung Nổi Bật

#### Đưa ra các ảnh hưởng tiêu cực của kiến trúc ứng dụng cũ

- Cách đặt câu lệnh sai lầm: Người dùng thường nhồi nhét dữ liệu thô, lặp lại điều hiển nhiên, hoặc đưa ra prompt mơ hồ làm giảm hiệu suất AI.
- Dữ liệu phân tán: Doanh nghiệp tốn nhiều thời gian, giảm năng suất do quy trình thủ công, xử lý các tác vụ lặp đi lặp lại và dữ liệu bị phân tán.
- Rủi ro CDN & Bảo mật: Doanh nghiệp dễ đối mặt với nguy cơ phát sinh chi phí CDN đột biến và rủi ro từ các cuộc tấn công volumetric (DDoS).
- Mất tính nhất quán của LLM: Việc tin tưởng tuyệt đối vào tham số temperature = 0 sẽ luôn trả về một kết quả duy nhất là sai lầm trong môi trường production.
- Bất đối xứng dữ liệu tài chính: Hệ thống ngân hàng truyền thống thường từ chối hồ sơ của các công ty khởi nghiệp do sự bất đối xứng về mô hình dữ liệu tài chính.

#### Giải pháp tối ưu hóa ngữ cảnh và trợ lý thông minh (GenAI)

- **Khung ứng dụng ngữ cảnh chuẩn:** Mô hình hóa ngữ cảnh dựa trên 4 yếu tố: **Goal** (Mục tiêu), **Relevant info** (Thông tin liên quan), **Constraints** (Ràng buộc), **Success criteria** (Tiêu chí thành công).
- **Mô hình "Second AI Brain":** Kiến trúc xây dựng bộ não thứ hai trên đám mây AWS sử dụng S3 và Bedrock.
- **Amazon Q Suite:** Giải pháp trợ lý thông minh kết nối dữ liệu bảo mật (Bedrock, Databases, Web search) đi kèm hàng rào an toàn (Guardrails). 

#### Tối ưu hóa hạ tầng và truyền tải với Amazon CloudFront

- **Cơ chế phòng thủ lớp biên:** Chống tấn công DDoS thông qua AWS Shield, WAF và cơ chế ẩn giấu máy chủ gốc (Origin Cloaking với VPC/OAC).
- **Tối ưu chi phí và hiệu năng:** Áp dụng mô hình gói giá cố định mới (Fixed-Price Plans) và kiến trúc bộ nhớ đệm nhiều lớp qua HTTP/3.
- **Điều hướng logic tại vùng biên:** Nén dữ liệu tự động, thiết lập chứng thực Mutual TLS, kiểm soát quyền truy cập qua Signed URL và xử lý logic bằng **CloudFront Functions / Lambda@Edge**.

#### Phát triển sản phẩm AI từ cuộc thi Hackathon (UTMorpho)

- **Ứng dụng Neural Interface:** Sản phẩm UTMorpho hỗ trợ chuyển đổi bản vẽ phác thảo thành giao diện lập trình trực tiếp bằng mô hình Claude Sonnet 4.
- **Quy trình áp lực cao:** Kinh nghiệm thiết lập mục tiêu, xây dựng tính năng cốt lõi, tích hợp, hoàn thiện và thuyết trình sản phẩm trong vòng 36 giờ.

#### Xử lý tính bất định (Non-Determinism) của LLM

- **Nguyên nhân kỹ thuật:** Hiện tượng mất tính nhất quán do phép toán số thực dấu phẩy động trên GPU không có tính kết hợp và do cơ chế gộp cụm yêu cầu (inference batching) từ cloud providers.
- **Chiến lược giảm thiểu:** Đặt tham số **temperature = 0.1** để tránh lặp từ, thực hiện chạy thử nhiều lần kết hợp bỏ phiếu số đông (majority voting).

#### Kiến trúc Multi-Agent trong Doanh nghiệp

- **Hội đồng tín dụng ảo (Virtual Credit Committee):** Kiến trúc Multi-Agent giúp đánh giá hồ sơ startup đa chiều, cắt giảm hơn 95% chi phí và thời gian xử lý hồ sơ.
- **Phân rã chuyên môn:** Tách biệt các đại lý chuyên biệt bao gồm Tài chính, Thị trường, Đội ngũ, Rủi ro, và Tuân thủ để tạo cơ chế kiểm soát chéo **(Checks & Balances)**.  

### Những Gì Học Được

#### Tư Duy Thiết Kế

- **Context Quality > Context Quantity:** Chất lượng của ngữ cảnh quan trọng hơn số lượng thông tin cung cấp khi tương tác với AI.
- **Tư duy tự động hóa quy trình (Automation Flows):** Cách kết nối các nguồn dữ liệu đa dạng để rút ngắn thời gian từ phân tích đến hành động liên phòng ban.
- **Tư duy tối ưu lớp biên (Edge Computing):** Tăng cường tính sẵn sàng cao với cơ chế tự động chuyển vùng khi máy chủ gốc gặp sự cố (Origin Failover).
- **Chấp nhận tính xác suất:** Hiểu rõ bản chất của LLM để thiết kế logic hệ thống linh hoạt hơn, thay vì kỳ vọng tính định hướng tuyệt đối.
- **Kiểm soát và cân bằng:** Ý thức được hạn chế của Single Agent (giới hạn ngữ cảnh, loãng chuyên môn) để chuyển dịch sang hệ thống Multi-Agent. 

#### Kiến Trúc Kỹ Thuật

- Hình thành tư duy thiết kế hệ thống ngữ cảnh **(Context engineering)**.
- Nguyên lý vận hành của Agentic AI gắn liền với cơ chế bảo mật, kiểm soát truy cập **(Governance & Data Security)**.
- Kỹ thuật bắt buộc định dạng đầu ra **(JSON mode, regex grammars)** bằng cấu hình thay vì chỉ dùng prompt thuần túy.
- **Khung kiến trúc thiết lập rào chắn (Guardrails) ba lớp:** đầu vào **(Input)**, xử lý **(Processing)** và đầu ra **(Output)** để bảo vệ dữ liệu nhạy cảm.
- **Cách thức vượt qua rào cản kỹ thuật:** Kiểm soát hiện tượng AI tự tạo dữ liệu thừa **(AI Overgeneration)** và xử lý giới hạn token **(Token Limits)**. 

### Ứng Dụng Vào Công Việc

- Áp dụng khung cấu trúc ngữ cảnh chuẩn **(Goal, Relevant info, Constraints, Success criteria)** khi thiết lập prompt hệ thống cho các dự án AI hiện tại.
- Nghiên cứu tích hợp Amazon Q Suite để xây dựng các trợ lý tự động hóa quy trình nội bộ (ví dụ: Tự động hóa tạo biên bản cuộc họp MoM, gửi email, lên lịch).
- Áp dụng tư duy Edge Computing của CloudFront vào hệ thống để tối ưu hóa chi phí truyền tải, tự động nén dữ liệu và bảo mật máy chủ gốc bằng OAC.
- **Cấu hình lại các tham số LLM trong môi trường production:** Chuyển đổi sang temperature = 0.1, áp dụng cơ chế định dạng cấu trúc đầu ra bằng JSON mode để đảm bảo tính ổn định hệ thống.
- Triển khai thử nghiệm mã nguồn Multi-Agent thông qua Docker, Bedrock AgentCore và Terraform nhằm ứng dụng quy trình phân rã chuyên môn cho các bài toán logic phức tạp. 

### Trải nghiệm trong event

Tham gia chuỗi hội thảo là một trải nghiệm vô cùng thực tế và giá trị, giúp tôi mở rộng toàn diện tư duy từ hạ tầng Cloud, tối ưu hóa hệ thống cho đến các kiến trúc GenAI tiên tiến nhất hiện nay. Một số trải nghiệm nổi bật:

#### Học hỏi từ các diễn giả có chuyên môn cao
- Các diễn giả đến từ những tổ chức công nghệ uy tín như AWS, GoTymeX, Cloud Kinetics, VPBank đã mang lại các góc nhìn chuyên sâu và thực chiến.
- Được lắng nghe phân tích từ các bài toán thực tế của doanh nghiệp như tối ưu chi phí CDN cho đến cách xây dựng hệ thống thẩm định tài chính tự động trong ngành ngân hàng.  

#### Trải nghiệm kỹ thuật thực tế
- Tiếp cận trực tiếp với các buổi demo trực quan trên môi trường đám mây AWS (S3, Bedrock, Amazon Q, CloudFront).
- Được chứng kiến các case study thực tế như cách Trợ lý PM tự động hóa công việc, cách một ứng dụng vẽ phác thảo tích hợp Claude Sonnet 4 vận hành dưới áp lực thời gian 36 giờ của một cuộc thi Hackathon.

#### Ứng dụng công cụ hiện đại
- Hiểu sâu sắc các khái niệm kỹ thuật cốt lõi: từ lý do GPU làm mất tính nhất quán của LLM đến cách thiết lập hệ thống rào chắn (Guardrails) 3 lớp bảo mật cho ứng dụng doanh nghiệp.
- Tiếp cận tư duy thiết kế hệ thống phân rã chuyên môn để giải quyết bài toán giới hạn dữ liệu và ngữ cảnh.

#### Bài học rút ra
- Khi làm việc với AI, chất lượng của ngữ cảnh luôn quan trọng hơn số lượng thông tin cung cấp (Context Quality > Context Quantity).
- Triển khai AI trong môi trường doanh nghiệp không chỉ là làm cho ứng dụng chạy được, mà bắt buộc phải đảm bảo các yếu tố bảo mật, quản trị rủi ro và tuân thủ chính sách ngay từ ngày đầu tiên.
- Những ý tưởng thực tế và có giá trị nhất luôn bắt nguồn từ chính việc tập trung giải quyết triệt để các khó khăn cụ thể gặp phải trong công việc hàng ngày. 

#### Một số hình ảnh khi tham gia sự kiện
* Thêm các hình ảnh của các bạn tại đây
![Event 1](/images/4-EventParticipated/event2.jpg)
> Tổng thể, sự kiện không chỉ cung cấp kiến thức kỹ thuật mà còn giúp tôi thay đổi cách tư duy về thiết kế ứng dụng, hiện đại hóa hệ thống và phối hợp hiệu quả hơn giữa các team.
