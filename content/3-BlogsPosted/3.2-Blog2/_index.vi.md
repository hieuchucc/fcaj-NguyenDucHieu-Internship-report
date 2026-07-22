---
title: "Giải pháp xây dựng kiến trúc Backend Serverless tự động mở rộng cho Web & Mobile"
date: 2026-07-18
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

Khi triển khai các hệ thống thực tế yêu cầu tương tác liên tục — chẳng hạn như một website đặt vé máy bay xây dựng bằng ReactJS hay một ứng dụng đặt dịch vụ trên điện thoại dùng React Native — việc duy trì các máy chủ backend (server) truyền thống thường tốn kém và tạo ra điểm nghẽn (*bottleneck*) khi lượng truy cập tăng vọt.

Bài viết này sẽ hướng dẫn cách xây dựng một kiến trúc Backend hoàn toàn **Serverless (không máy chủ)** trên AWS, giúp hệ thống cung cấp các REST API ổn định, có khả năng tự động mở rộng và tối ưu chi phí vận hành.

## Tổng quan giải pháp

Kiến trúc này loại bỏ hoàn toàn gánh nặng quản lý hệ điều hành, kết hợp các dịch vụ cốt lõi sau để tạo ra một luồng xử lý khép kín:

* **Amazon S3 & AWS Amplify:** Đảm nhận việc lưu trữ và phân phối các file tĩnh (HTML, CSS, JS) cho các ứng dụng frontend một cách nhanh chóng thông qua mạng phân phối nội dung (CDN).
* **Amazon API Gateway:** Đóng vai trò là "cửa ngõ" tiếp nhận toàn bộ các HTTP/REST request từ client. Dịch vụ này quản lý định tuyến, giới hạn lưu lượng (*rate limiting*) và bảo vệ backend khỏi các đợt tấn công DDoS.
* **AWS Lambda:** Nơi chứa logic cốt lõi của ứng dụng (Node.js, Java, Python...). Code chỉ được kích hoạt chạy khi có request từ API Gateway truyền tới, sau đó tự động tắt, không cần server chạy ngầm 24/7.
* **Amazon DynamoDB:** Cơ sở dữ liệu NoSQL được quản lý hoàn toàn, cung cấp tốc độ đọc/ghi dữ liệu (như thông tin user, lịch sử đặt chỗ, trạng thái vé) với độ trễ tính bằng mili-giây ở bất kỳ quy mô nào.

## Lợi ích cốt lõi

* **Khả năng tự động mở rộng (Auto-scaling):** Hệ thống có thể tự động xử lý từ vài request lên hàng chục nghìn request cùng lúc mà không cần thay đổi cấu hình.
* **Tối ưu chi phí (Pay-as-you-go):** Bạn chỉ trả tiền cho số lượt gọi API thực tế và số mili-giây Lambda thực thi code. Không có traffic = Không tốn tiền duy trì.
* **Thời gian ra mắt sản phẩm nhanh (Time-to-market):** Lập trình viên không cần bận tâm đến việc vá lỗi bảo mật OS hay cấu hình mạng lưới, chỉ cần tập trung vào nghiệp vụ code.

## Hướng dẫn triển khai

1. **Bước 1: Thiết lập cơ sở dữ liệu (DynamoDB)**  
   Tạo một bảng dữ liệu với Partition Key phù hợp (ví dụ: `BookingID`) để lưu trữ các giao dịch của người dùng.
2. **Bước 2: Viết logic xử lý (AWS Lambda)**  
   Viết các hàm thực hiện thao tác CRUD (Tạo, Đọc, Sửa, Xóa) dữ liệu và cấp quyền (IAM Role) cho phép Lambda ghi dữ liệu vào bảng DynamoDB.
3. **Bước 3: Xây dựng cổng giao tiếp (API Gateway)**  
   Định nghĩa các RESTful endpoints (VD: `/bookings`, `/services`). Bật tính năng CORS để cho phép các domain khác (frontend web/mobile) gọi được API một cách an toàn.
4. **Bước 4: Tích hợp và Xác thực**  
   Nối các endpoints của API Gateway với các hàm Lambda tương ứng. Có thể tích hợp thêm Amazon Cognito để cấp token, đảm bảo chỉ người dùng đã đăng nhập mới gọi được API.
5. **Bước 5: Kết nối Client**  
   Tích hợp các URL API vừa tạo vào ứng dụng client bằng các thư viện HTTP client (như Axios) để bắt đầu gửi và nhận dữ liệu thực tế.

---

> **Kết luận:** Bằng cách kết hợp API Gateway, Lambda và DynamoDB, doanh nghiệp có thể xây dựng một hệ thống backend REST API mạnh mẽ, linh hoạt và không cần bảo trì hạ tầng vật lý. Kiến trúc Serverless này chính là "chìa khóa" giúp các ứng dụng Web và Mobile hoạt động mượt mà, sẵn sàng phục vụ hàng triệu người dùng mà vẫn giữ mức chi phí vận hành hợp lý.

![blog picture](/images/3-BlogsPosted/blog2.png)

Links: <https://aws.amazon.com/vi/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/?content_source=fb&fb_content_id=Q9-wBQGs70PN9Vr2o4NP0uPjV3be8QzEL7QDy7SvdMB6XBTQH7o6xJGmo8RjDjMgsA&channel_type=fb&fbclid=IwY2xjawTMBWthZmRrCWxOZ2JMRzhVZWV4dG4DYWVtAjExAHNydGMGYXBwX2lkEDIyMjAzOTE3ODgyMDA4OTIAAR5d8sFBsac3PmGFP_hFCPt-is73FlV7N5gstD5OcLnsaJpPM1-DitYnNNcOVw_aem_7vn6ZBl9dHnqP4CTgbLnEg> <br> <https://www.facebook.com/groups/660548818043427/user/100037447715326>
