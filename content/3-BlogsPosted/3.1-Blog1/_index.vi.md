---
title: "Giải pháp Oracle HA trên AWS bằng Amazon FSx"
date: 2026-06-12
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
Các ứng dụng doanh nghiệp mang tính sống còn luôn phụ thuộc vào cơ sở dữ liệu Oracle, do đó việc đảm bảo tính sẵn sàng (High Availability - HA) liên tục là yếu tố bắt buộc. Các giải pháp Oracle HA truyền thống thường đòi hỏi phần mềm clustering phức tạp, hệ thống lưu trữ chia sẻ đắt đỏ và đội ngũ quản trị cơ sở dữ liệu chuyên biệt, dẫn đến rủi ro *single point of failure* và gánh nặng vận hành lớn.

Bằng cách kết hợp **Amazon FSx for NetApp ONTAP (FSxN)** với các dịch vụ tự động hóa của AWS, bài viết này sẽ hướng dẫn cách xây dựng một kiến trúc cơ sở dữ liệu Oracle có độ sẵn sàng cao, giảm thiểu tối đa thời gian phục hồi.

## Tổng quan giải pháp

Giải pháp là sự kết hợp của nhiều dịch vụ AWS để tạo ra một kiến trúc HA toàn diện:

* **Amazon FSx for NetApp ONTAP (Multi-AZ):** Cung cấp bộ lưu trữ dùng chung bền vững cho các tệp dữ liệu, phần mềm và cấu hình Oracle. Dữ liệu luôn có sẵn ngay cả khi EC2 instance bị thay thế.
* **Amazon EC2 Auto Scaling groups:** Quản lý vòng đời instance tự động. Nếu một instance bị lỗi, nó sẽ được thay thế bằng một instance mới với cấu hình giống hệt và tự động kết nối vào hệ thống lưu trữ FSxN.
* **AWS Backup:** Tạo các bản Amazon Machine Images (AMI) lưu lại trạng thái cấu hình mới nhất của máy chủ Oracle (bao gồm các bản vá và cài đặt).
* **AWS Lambda & Amazon EventBridge:** Trích xuất ID của AMI từ các bản sao lưu mới nhất và tự động cập nhật hệ thống.
* **AWS Systems Manager (SSM) Parameter Store:** Lưu trữ AMI ID mới nhất để Auto Scaling group luôn sử dụng cấu hình cập nhật nhất khi khởi chạy instance mới.

## Lợi ích cốt lõi

* **RTO (Thời gian phục hồi mục tiêu):** Chỉ từ 2–5 phút với cấu hình Oracle mới nhất.
* **RPO (Điểm phục hồi mục tiêu):** Gần như bằng 0 nhờ cơ chế đồng bộ hóa Multi-AZ.
* **Tính nhất quán:** Các instance mới luôn khởi chạy với thiết lập máy chủ Oracle hoàn toàn giống hệt bản cũ.
* **Quản lý AMI tự động:** Lên lịch tạo AMI và cập nhật Parameter Store hoàn toàn tự động, không cần thao tác thủ công.

## Hướng dẫn triển khai

1. **Bước 1: Lập "kho chứa" dữ liệu chung (FSxN)**  
   Tạo một không gian lưu trữ dùng chung có khả năng đồng bộ dữ liệu liên tục giữa 2 trung tâm dữ liệu (Multi-AZ). Sau đó, cấu hình mạng (iSCSI) để máy chủ có thể kết nối vào hệ thống lưu trữ này.
2. **Bước 2: Thiết lập bảo vệ EC2 instance (AWS Backup)**  
   Cấu hình tính năng tự động sao lưu (tạo bản ghi AMI) cho máy chủ Oracle hiện tại thông qua việc gắn thẻ (tag) nhận diện.
3. **Bước 3: Lấy mã số bản sao lưu mới nhất (Lambda)**  
   Mỗi khi Bước 2 hoàn tất, một function Lambda sẽ tự động được kích hoạt để trích xuất mã ID của bản sao lưu AMI vừa tạo.
4. **Bước 4: Cấu hình Systems Manager (SSM) Parameter Store**  
   Lambda ở Bước 3 sẽ tự động ghi đè mã ID mới nhất này vào SSM Parameter Store, giúp hệ thống luôn định vị được bản cấu hình mới nhất.
5. **Bước 5: Thiết lập Auto Scaling Group với hệ thống tự phục hồi**  
   Tạo một nhóm quản lý máy chủ với quy tắc duy trì luôn có **1 máy chủ hoạt động**. Nếu máy chủ hiện tại gặp sự cố, hệ thống sẽ đọc SSM Parameter Store để lấy AMI mới nhất, tạo máy chủ thay thế, tự động kết nối vào kho dữ liệu chung (FSxN) và khởi động Oracle.

---

> **Kết luận:** Bằng cách kết hợp lưu trữ chia sẻ FSxN Multi-AZ cùng hệ thống tự động hóa AMI bằng AWS Backup và Lambda, doanh nghiệp có thể đạt được độ sẵn sàng cao cho Oracle mà vẫn giữ vững tính nhất quán của cấu hình. Hệ thống tự động phục hồi lỗi chỉ trong vài phút, giúp giảm thiểu rủi ro vận hành và duy trì hoạt động liên tục.

![blog picture](/images/3-BlogsPosted/blog1.jpg)

Links: <https://aws.amazon.com/vi/blogs/architecture/building-highly-available-oracle-databases-with-amazon-fsx-for-netapp-ontap/> <br> <https://www.facebook.com/groups/660548818043427/user/100081065478266>