---
title: "Bản đề xuất"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# LMS & AI Proctoring System
## Hệ thống quản lý học tập và giám thị AI Serverless trên nền tảng AWS

### 1. Tóm tắt điều hành
LMS & AI Proctoring System là một hệ thống quản lý học tập (LMS) kết hợp giám thị thi cử bằng trí tuệ nhân tạo, được xây dựng theo kiến trúc hướng sự kiện (Event-driven Architecture) trên nền tảng đám mây AWS. Hệ thống hỗ trợ toàn diện vòng đời kiểm tra trực tuyến: từ tạo khóa học, đề thi đến quá trình làm bài và nhận kết quả. Điểm khác biệt cốt lõi của nền tảng là việc ứng dụng AI để tự động chấm điểm (trắc nghiệm và tự luận) và giám sát hành vi thí sinh qua webcam nhằm phát hiện gian lận theo thời gian thực. Bằng việc tận dụng kiến trúc Serverless, hệ thống tối ưu hóa chi phí vận hành, giảm thiểu công sức giám sát thủ công và đảm bảo khả năng mở rộng linh hoạt theo số lượng thí sinh.

### 2. Tuyên bố vấn đề
*Vấn đề hiện tại*
Việc tổ chức thi trực tuyến tại nhiều cơ sở đào tạo gặp khó khăn lớn trong khâu giám sát, dẫn đến tình trạng gian lận dễ dàng xảy ra (xem tài liệu, nhờ người làm hộ). Giảng viên phải tốn nhiều nhân lực và thời gian để trực tiếp giám sát video hoặc chấm bài tự luận thủ công. Ngoài ra, các hệ thống LMS truyền thống thường rời rạc, không tích hợp sẵn cơ chế giám thị và rất dễ quá tải khi lượng thí sinh truy cập đồng thời tăng cao vào các mùa thi cuối kỳ.

*Giải pháp*
Dự án xây dựng một nền tảng hợp nhất tích hợp LMS và pipeline giám thị AI. Hệ thống sử dụng luồng Kinesis Video Streams để thu nhận video thí sinh, chuyển tiếp qua hệ sinh thái AI của AWS (Rekognition, Transcribe, Bedrock) để nhận diện khuôn mặt, vật thể cấm và bóc tách giọng nói. Dữ liệu gian lận được tính điểm rủi ro và lưu trữ tốc độ cao trên DynamoDB, đồng thời gửi cảnh báo khẩn cấp qua SNS. 

*Mục tiêu*
Đảm bảo tính công bằng trong thi cử trực tuyến, giảm tải khối lượng công việc cho giảng viên và cung cấp một hạ tầng có tính sẵn sàng cao, chỉ trả tiền theo mức độ sử dụng thực tế (Pay-as-you-go).

### 3. Kiến trúc giải pháp
Nền tảng áp dụng kiến trúc AWS Serverless, phân tách rõ ràng giữa Frontend (Client), nghiệp vụ LMS lõi (Backend) và luồng xử lý giám thị tự động (AI Proctoring Pipeline).

*Dịch vụ AWS sử dụng
- *Frontend & Security*: Amazon Route 53, AWS WAF, AWS Amplify.
- *Authentication & API*: Amazon Cognito (phân quyền STUDENT/INSTRUCTOR), Amazon API Gateway.
- *Core Compute & Integration*: AWS Lambda (xử lý nghiệp vụ), Amazon EventBridge, Amazon SQS, AWS Step Functions (điều phối luồng AI).
- *Video & AI Proctoring*: Amazon Kinesis Video Streams, Amazon Polly (đọc đề/hướng dẫn), Amazon Rekognition, Amazon Transcribe, Amazon Bedrock.
- *Data Persistence*: Amazon Aurora DB (dữ liệu LMS), Amazon S3 (lưu trữ video thô), Amazon DynamoDB (lưu log gian lận).
- *Observability & Alerts*: Amazon CloudWatch, AWS X-Ray, Amazon SNS (cảnh báo tức thời).
- *Security & Governance*: AWS IAM, AWS KMS, AWS Secrets Manager, AWS SAM/CDK (IaC).
![Architecture](/images/2-Proposal/platform_architecture.jpg)

### 4. Triển khai kỹ thuật
*Yêu cầu công nghệ & Hạ tầng*
- *Frontend*: ReactJS, Vite, Tailwind CSS. Giao diện được host tĩnh trên AWS Amplify kết hợp S3 lưu trữ tài nguyên.
- *Backend & Pipeline*: Xử lý hoàn toàn thông qua Amazon API Gateway (REST API) và AWS Lambda để đáp ứng mô hình hướng sự kiện.
- *Cơ sở dữ liệu*: Dữ liệu quan hệ (khóa học, người dùng) đặt tại Aurora DB; dữ liệu cần ghi/đọc tốc độ cực cao trong lúc thi (log giám sát) đặt tại DynamoDB.

*Yêu cầu phi chức năng*
- Thời gian phản hồi API dưới 2 giây ở điều kiện bình thường.
- Độ trễ phát hiện và ghi nhận hành vi bất thường trong luồng video/audio dưới 5 giây.
- Hệ thống có khả năng tự động mở rộng theo lưu lượng, đảm bảo backup (sao lưu) và khôi phục dữ liệu khi có sự cố.

### 5. Ước tính ngân sách
Giả định hệ thống phục vụ quy mô 500 sinh viên, tổ chức 50 lượt thi/tháng, mỗi lượt thi kéo dài trung bình 45 phút stream video. Nền tảng không yêu cầu chi phí đầu tư phần cứng (0 VNĐ).

*Chi phí hạ tầng AWS dự kiến hàng tháng:*
- AWS Lambda (20.000 req, 512MB): 0 USD
- Amazon API Gateway (20.000 req): 0,02 USD
- Amazon DynamoDB (On-demand): 1,19 USD
- Amazon S3 (Lưu trữ video và media): 1,26 USD
- Amazon Kinesis Video Streams: 0,18 USD
- Amazon Rekognition: 4,09 USD
- Amazon Transcribe: 0,60 USD
- Amazon Bedrock: 8,64 USD
- Amazon CloudWatch (15 metrics): 4,50 USD
- Amazon SNS (10.000 req): 0 USD
- AWS Security (IAM Access Analyzer / KMS / Secrets Manager): 4,46 USD
- Amazon Cognito: 0,07 USD

*Tổng cộng*: ~25,01 USD/tháng (tương đương ~650.000 VNĐ). <br>
*Chi phí năm*: ~300,12 USD/năm.

### 6. Đánh giá rủi ro
*Ma trận rủi ro chính*
- *Quá tải hệ thống (Giờ cao điểm)*: Ảnh hưởng cao, xác suất trung bình.
- *Chi phí AWS vượt dự kiến (Gọi dư thừa AI)*: Ảnh hưởng trung bình, xác suất cao.
- *Mất hoặc sai lệch dữ liệu*: Ảnh hưởng nghiêm trọng, xác suất thấp.
- *Gian lận bằng công nghệ cao (Deepfake)*: Ảnh hưởng trung bình, xác suất thấp.

*Chiến lược giảm thiểu & Dự phòng*
- Sử dụng Rate Limiting của AWS WAF và bản chất tự mở rộng của Serverless để chống quá tải.
- Thiết lập AWS Budgets và CloudWatch Billing Alarm để ngắt hoặc cảnh báo khi chi phí chạm ngưỡng.
- Kích hoạt Point-in-Time Recovery (PITR) trên database để phòng hờ sự cố mất dữ liệu.
- *Kế hoạch dự phòng*: Nếu các dịch vụ AI AWS gặp sự cố gián đoạn, hệ thống tự động fallback: vẫn cho phép nộp bài bình thường, tạm vô hiệu hóa AI và cờ đánh dấu (flag) luồng video đó để giảng viên xem lại thủ công sau khi thi xong.

### 7. Kết quả kỳ vọng
*Cải tiến kỹ thuật*
Xây dựng thành công toàn bộ luồng nghiệp vụ khép kín từ khâu ra đề đến chấm điểm trực tuyến trên nền tảng AWS Serverless. Khắc phục được độ trễ trong giám sát truyền thống, đưa ra cảnh báo thời gian thực và quản lý tập trung toàn bộ dữ liệu học tập/thi cử.

*Giá trị dài hạn*
Giải pháp mang lại môi trường giáo dục minh bạch, tiết kiệm hàng trăm giờ công cho giảng viên trong việc giám thị và chấm bài. Kiến trúc hệ thống là tiền đề để sinh viên rèn luyện kỹ năng Cloud thực chiến, đồng thời có thể dễ dàng mở rộng thêm các tính năng (như thi vấn đáp AI, phân tích học lực cá nhân hóa) tiến tới hoàn thiện một sản phẩm thương mại thực thụ.