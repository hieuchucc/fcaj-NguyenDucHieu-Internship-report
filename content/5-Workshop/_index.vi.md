---
title: "Workshop"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5. </b> "
---


# Kiến trúc hệ thống và giải pháp triển khai LMS & AI Proctoring trên AWS

#### Tổng quan
- AWS cung cấp một hệ sinh thái toàn diện với kiến trúc hướng sự kiện (Event-driven Architecture) và Serverless, cho phép xây dựng hệ thống quản lý học tập kết hợp giám thị thi cử tự động bằng trí tuệ nhân tạo một cách linh hoạt, bảo mật và tối ưu chi phí.

- Trong báo cáo này, chúng ta sẽ đi sâu vào cấu trúc công nghệ, các dịch vụ AWS cốt lõi và phương án triển khai để vận hành hệ thống LMS & AI Proctoring System.

- Hệ thống ứng dụng kết hợp nhiều dịch vụ chuyên biệt của AWS để xử lý đồng thời nghiệp vụ LMS, thu thập luồng video thời gian thực và vận hành pipeline AI.

+ *Frontend & Routing* - Triển khai giao diện web tương tác bằng ReactJS kết hợp AWS Amplify và bảo vệ lưu lượng truy cập thông qua Amazon Route 53 cùng AWS WAF.

+ *Core Services & AI* - Sử dụng AWS Lambda xử lý logic nghiệp vụ, Amazon Kinesis Video Streams thu nhận hình ảnh/âm thanh, kết hợp cùng Amazon Rekognition, Amazon Transcribe và Amazon Bedrock để giám sát gian lận và chấm bài tự động.

#### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Demo](5.3-Demo/)