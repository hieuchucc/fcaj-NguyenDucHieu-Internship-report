---
title: "Event 1"
date: 2026-05-09
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---



# Bài thu hoạch “Automated Prompt Engineering”


### Danh Sách Diễn Giả

- **Nguyễn Tuấn Thịnh** - DevOps/Cloud Engineer


### Nội Dung Nổi Bật

#### Tầm Quan Trọng Của Prompt Engineering

Việc giao tiếp không hiệu quả với AI đem lại nhiều hệ quả tiêu cực:
- **Câu lệnh chung chung (Generic prompts) → Kết quả chung chung**: Không đáp ứng được yêu cầu cụ thể của bài toán.
- **Lãng phí token → Tăng chi phí**: Mô hình xử lý các đoạn text dài dòng, không cần thiết.
- **Chỉ dẫn mơ hồ**: Dẫn đến việc giao tiếp kém hiệu quả với LLM.
- **Kết quả không nhất quán & Giảm năng suất**: Tốn thời gian thử đi thử lại nhiều lần.

#### Các Thành Phần Của Một Prompt Chất Lượng (Key Components)

Để xây dựng một prompt hiệu quả, cần cấu trúc rõ ràng các thành phần sau:
- **Role**: Vai trò mà mô hình cần đóng vai (VD: Career coach cho sinh viên mới tốt nghiệp).
- **Instruction**: Nhiệm vụ cụ thể mô hình cần thực hiện (VD: Cải thiện đoạn giới thiệu bản thân khi phỏng vấn thực tập).
- **Context**: Thông tin nền tảng, bối cảnh liên quan (VD: DevOps Engineer có kinh nghiệm AWS, backend).
- **Input Data**: Dữ liệu/văn bản đầu vào cần xử lý (VD: "Hello, my name is Thinh...").
- **Output Format**: Cấu trúc, định dạng, phong cách đầu ra mong muốn.
- **Examples**: Các ví dụ minh họa (Few-shot demonstrations).
- **Constraints/Guidelines**: Các giới hạn, ràng buộc (VD: Dưới 80 từ, dùng từ ngữ đơn giản, tự nhiên, tự tin, không làm những việc nằm ngoài phạm vi).

#### Nghệ Thuật Giao Tiếp Với AI & Token Economics

- **Nguyên tắc vàng khi prompt**:
  - Rõ ràng & cụ thể; sử dụng ngôn ngữ mang tính chỉ thị (Directive Language).
  - Dùng dấu phân cách (Delimiters) để chia rõ các phần trong câu lệnh.
  - Mô tả những việc **NÊN làm (DOs)** thay vì những việc **KHÔNG NÊN làm (DON'TS)**.
  - Không nên yêu cầu LLM tự tính toán toán học phức tạp; cho phép mô hình trả lời "Tôi không biết" để tránh bịa thông tin (hallucination).
  - Chia nhỏ các input quá dài thành từng đoạn nhỏ hơn.
- **Hiểu về chi phí (Token Economics)**:
  - Token là các đơn vị subword (không phải lúc nào cũng tương đương 1 từ).
  - Số lượng token tiêu tốn khác nhau tùy thuộc vào ngôn ngữ sử dụng.
  - *Ví dụ chi phí (Mô hình Claude Opus 4.6)*: Input tokens ~ $5.00 / 1M tokens; Output tokens ~ $25.00 / 1M tokens.

#### Các Kỹ Thuật Nâng Cao (Advanced Techniques)

- **Chain-of-Thought (CoT) Prompting**: Hướng dẫn mô hình suy luận từng bước trước khi đưa ra kết quả.
- **Self-Consistency**: Mở rộng từ CoT bằng cách tạo ra nhiều luồng suy luận và chọn câu trả lời phổ biến/hợp lý nhất.
- **Tree-of-Thoughts (ToT)**: Mô hình hóa các hướng suy luận như một cái cây, khám phá và đánh giá các nhánh khác nhau để tìm ra giải pháp tối ưu.
- **Retrieval-Augmented Generation (RAG)** & **Role Prompting**: Kết hợp truy xuất kiến thức bên ngoài và định hình vai trò chuyên sâu cho AI.

#### Giới Thiệu Công Cụ Proptimizer & Kiến Trúc AWS

**Proptimizer** là tiện ích mở rộng trên trình duyệt (browser extension) giúp tự động hóa quá trình tối ưu prompt và cho phép trò chuyện với AI ở bất kỳ đâu trên web.

- **Frontend & Content Delivery**:
  - **AWS CloudFront**: Mạng phân phối nội dung toàn cầu (CDN), độ trễ thấp, cache tài nguyên tĩnh.
  - **Amazon S3**: Lưu trữ tài nguyên web tĩnh, hình ảnh với độ bền cao (99.999999999%).
- **Authentication & Security**:
  - **Amazon Cognito**: Quản lý xác thực và phân quyền người dùng, xử lý JWT token, sign-up/sign-in.
- **API & Backend Logic**:
  - **Amazon API Gateway**: Điều hướng traffic, xử lý API calls, rate limiting và phân quyền.
  - **AWS Lambda**: Xử lý logic backend không máy chủ (serverless compute), chạy code khi có trigger và tự tắt để tối ưu chi phí.
- **AI Integration & Data Storage**:
  - **Amazon Bedrock**: Cung cấp quyền truy cập vào các Foundation AI models (Claude, GPT...) để thực hiện tối ưu prompt mà không cần tự train model.
  - **Amazon DynamoDB**: Cơ sở dữ liệu NoSQL lưu trữ dữ liệu người dùng, lịch sử prompt với thời gian phản hồi mili-giây và tự động mở rộng.
- **Monitoring & Operations**:
  - **Amazon CloudWatch Logs & Metrics**: Thu thập log từ Lambda/API Gateway, theo dõi hiệu năng hệ thống theo thời gian thực.
- **Chi phí vận hành**: Được tối ưu tận dụng kiến trúc Serverless với chi phí cơ sở hạ tầng có thể đạt mức **$0** (chưa bao gồm phí sử dụng dịch vụ Amazon Bedrock).

---

### Những Gì Học Được

#### Tư Duy Tối Ưu Prompt (Prompt Engineering Mindset)

- **Nguyên lý rõ ràng**: Hiểu được vì sao một prompt chung chung lại thất bại và tầm quan trọng của việc cung cấp Context, Role và Constraints.
- **Quản lý chi phí token**: Nhận thức được cách LLM tính phí trên subword và sự chênh lệch chi phí giữa Input/Output tokens để tối ưu hóa câu lệnh.

#### Kỹ Thuật Giao Tiếp Với LLM

- Làm chủ cấu trúc prompt 6 thành phần: Role, Instruction, Context, Input, Output format và Examples.
- Hiểu và áp dụng được các mô hình suy luận nâng cao từ **Chain-of-Thought (CoT)**, **Self-Consistency** cho đến **Tree-of-Thoughts (ToT)** để giải quyết các bài toán suy luận phức tạp.
- Cải thiện chất lượng câu trả lời bằng cách dùng ngôn ngữ chỉ thị rõ ràng và hạn chế việc dùng các từ phủ định (DON'TS).

#### Kiến Trúc Serverless Cho Ứng Dụng AI (Proptimizer Architecture)

- Cách thiết kế một hệ thống AI tích hợp trình duyệt extension hoàn toàn trên kiến trúc **AWS Serverless**.
- Gắn kết trơn tru giữa **Frontend (CloudFront/S3)**, **Xác thực (Cognito)**, **Backend (API Gateway/Lambda)** và **AI Engine (Amazon Bedrock)**.
- Hiểu được lợi ích kinh tế (Token Economics & Serverless Pricing) khi xây dựng các ứng dụng thực tế ứng dụng GenAI với chi phí vận hành tối ưu.

---

### Ứng Dụng Vào Công Việc

- **Chuẩn hóa quy trình viết Prompt**: Áp dụng khung cấu trúc prompt (Role - Task - Context - Constraints) vào công việc hàng ngày của team để tăng chất lượng đầu ra từ AI.
- **Áp dụng CoT và ToT**: Sử dụng kỹ thuật Chain-of-Thought và Tree-of-Thoughts khi dùng AI hỗ trợ debug code, thiết kế kiến trúc hoặc giải quyết các vấn đề kỹ thuật nhiều bước.
- **Tối ưu chi phí sử dụng LLM**: Kiểm soát độ dài prompt và hạn chế token dư thừa trong các ứng dụng tích hợp LLM của dự án hiện tại.
- **Xây dựng kiến trúc Serverless kết hợp GenAI**: Tham khảo mô hình kiến trúc của Proptimizer để pilot các microservice hoặc internal tools tích hợp **Amazon Bedrock** và **AWS Lambda**.
- **Sử dụng Proptimizer**: Trải nghiệm công cụ hỗ trợ tự động tối ưu câu lệnh trực tiếp trên trình duyệt nhằm tiết kiệm thời gian giao tiếp với các mô hình AI.

---

### Trải Nghiệm Trong Event (AWS First Cloud AI Journey)

Tham gia phiên chia sẻ **“Automated Prompt Engineering: Enhancing LLM Output Quality”** của anh **Nguyễn Tuấn Thịnh** tại sự kiện AWS First Cloud AI Journey là một trải nghiệm mở rộng góc nhìn từ cả khía cạnh sử dụng AI lẫn thiết kế hệ thống.

#### Học hỏi từ thực chiến
- Bài giảng đi thẳng vào vấn đề thực tế: lý do vì sao chúng ta thường nhận được các câu trả lời chung chung từ AI và giải quyết triệt để bằng tư duy kỹ thuật rõ ràng.
- Các ví dụ so sánh trước và sau khi áp dụng Prompt Engineering (ví dụ bài toán Career Coach cho sinh viên) rất trực quan và dễ tiếp thu.

#### Kết hợp hoàn hảo giữa Prompt Engineering và Cloud Architecture
- Không chỉ dừng lại ở việc "mẹo viết câu lệnh", diễn giả còn giới thiệu kiến trúc thực tế của project **Proptimizer** chạy trên AWS.
- Trải nghiệm được cách kết hợp các dịch vụ AWS quen thuộc (S3, CloudFront, Lambda, DynamoDB) với **Amazon Bedrock** để tạo ra một sản phẩm GenAI thực thụ với chi phí hạ tầng tối ưu ($0 trừ phí model).

#### Bài học rút ra
- Viết prompt là một "nghệ thuật giao tiếp" nhưng dựa trên các nguyên tắc khoa học rõ ràng (cấu trúc thành phần, quản lý token, kỹ thuật suy luận).
- Tự động hóa Prompt Engineering (Automated Prompt Engineering) là hướng đi tất yếu để nâng cao năng suất và đảm bảo tính nhất quán cho các ứng dụng tích hợp AI trong doanh nghiệp.

#### Một số hình ảnh khi tham gia sự kiện
![Event 1](/images/4-EventParticipated/event1.jpg)

> Tổng thể, buổi chia sẻ mang lại những kiến thức thực tế, giúp tôi không chỉ giao tiếp với AI hiệu quả hơn mà còn học hỏi được mẫu kiến trúc chuẩn mực để xây dựng các sản phẩm AI trên nền tảng đám mây AWS.
