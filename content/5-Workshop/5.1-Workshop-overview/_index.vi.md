---
title: "Tổng quan workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Tổng quan workshop

Mục tiêu của workshop là triển khai EAM Workspace lên AWS và kiểm thử luồng end-to-end từ trình duyệt đến database. Nội dung được viết theo đúng mô hình đã triển khai trong project: Amplify Hosting cho frontend, API Gateway cho route `/api`, Elastic Beanstalk cho backend và RDS MySQL cho dữ liệu.

EAM Workspace có hai trải nghiệm người dùng chính:

- **Admin Portal**: quản lý nhân viên, phòng ban, danh mục, tài sản, bàn giao, thu hồi, bảo trì, kiểm kê, báo cáo, feedback, FAQ, chấm công, lịch sử đăng nhập và support chat.
- **Employee Portal**: xem tài sản được bàn giao, gửi yêu cầu hỗ trợ, đọc FAQ, cập nhật hồ sơ, đổi mật khẩu và xem lịch sử cá nhân.

Backend cung cấp REST API dưới prefix `/api`. Frontend gọi API bằng đường dẫn tương đối `/api`, Amplify rewrite request đến API Gateway, sau đó API Gateway chuyển tiếp đến backend Elastic Beanstalk. Các file upload như avatar hoặc hình ảnh tài sản được truy cập qua prefix `/uploads`, vì vậy môi trường Amplify cũng cần rewrite `/uploads/*` đến API Gateway để ảnh không bị trả về `404`.

## Kết quả mục tiêu

Sau khi hoàn thành workshop, hệ thống có:

- Frontend React được host trên AWS Amplify Hosting.
- Backend Node.js/Express chạy trên AWS Elastic Beanstalk.
- Amazon API Gateway HTTP API làm điểm vào cho backend.
- Database MySQL chạy trên Amazon RDS.
- Endpoint `/api/health` hoạt động qua cả API Gateway và Amplify domain.
- Luồng đăng nhập admin, user và các quy trình chính có thể kiểm thử trên trình duyệt.
- CloudWatch Logs hỗ trợ kiểm tra lỗi backend.

## Luồng triển khai

Luồng triển khai của workshop được xây dựng theo thứ tự từ hạ tầng dữ liệu, backend, lớp API trung gian đến frontend. Cách triển khai này giúp kiểm tra từng thành phần riêng lẻ trước khi kết nối thành một hệ thống hoàn chỉnh.

Đầu tiên, môi trường AWS, source code và các biến cấu hình cần được chuẩn bị đầy đủ. Sau đó, Amazon RDS for MySQL được cấu hình làm database chính cho hệ thống. Khi database sẵn sàng, backend Node.js/Express được đóng gói và triển khai lên AWS Elastic Beanstalk, đồng thời cấu hình các biến môi trường như `DATABASE_URL`, `JWT_SECRET`, thông tin SES SMTP và CORS origin.

Sau khi backend hoạt động ổn định và endpoint `/api/health` trả kết quả thành công, Amazon API Gateway được tạo để làm điểm truy cập public cho backend. Frontend React/Vite được triển khai lên AWS Amplify Hosting, sau đó cấu hình rewrite để các request `/api/*` và `/uploads/*` từ Amplify domain được chuyển tiếp đến API Gateway. Cuối cùng, hệ thống được kiểm thử bằng các luồng chính như đăng nhập admin, đăng nhập nhân viên, quản lý tài sản, bàn giao tài sản, kiểm tra API request trên DevTools và xác nhận tài khoản inactive bị chặn đăng nhập.

{{< mermaid >}}
flowchart TD
    A["Chuẩn bị AWS account, source code và biến môi trường"] --> B["Tạo hoặc cấu hình RDS MySQL"]
    B --> C["Đóng gói backend source bundle"]
    C --> D["Deploy backend lên Elastic Beanstalk"]
    D --> E["Cấu hình Environment Properties và kiểm tra health"]
    E --> F["Tạo API Gateway HTTP API"]
    F --> G["Deploy frontend lên Amplify Hosting"]
    G --> H["Thêm rewrite rule /api/* và /uploads/* đến API Gateway"]
    H --> I["Kiểm thử login, upload và workflow chính"]
    I --> J["Kiểm tra CloudWatch Logs và dọn dẹp tài nguyên"]
{{< /mermaid >}}

## Dịch vụ AWS trong phạm vi

| Dịch vụ | Mục đích |
| --- | --- |
| AWS Amplify Hosting | Host và build frontend React/Vite. |
| Amazon API Gateway | Cung cấp HTTP API public cho đường dẫn `/api/*`. |
| AWS Elastic Beanstalk | Chạy và quản lý backend Node.js. |
| Amazon RDS for MySQL | Lưu dữ liệu ứng dụng. |
| Amazon S3 | Hướng lưu trữ file sẵn sàng production. |
| Amazon SES | Gửi OTP và email thông báo nếu cấu hình mail được bật. |
| Amazon CloudWatch | Lưu log và hỗ trợ monitoring. |

## Bước 1: Quan sát kiến trúc triển khai

Trước khi bắt đầu cấu hình từng dịch vụ, cần nắm được luồng kết nối tổng thể của hệ thống.

![Sơ đồ kiến trúc tổng quan của workshop EAM Workspace](/eam-workshop-report/images/5-Workshop/5.1-Workshop-overview/5.1.1-architecture-overview.png)

*Hình 5.1.1. Sơ đồ kiến trúc tổng quan của workshop.*

Ảnh này giúp xác nhận các thành phần chính trong kiến trúc: frontend được phục vụ qua Amplify, request API đi qua API Gateway, backend chạy trên Elastic Beanstalk và dữ liệu được lưu trong Amazon RDS MySQL.

## Bước 2: Xác định các dịch vụ AWS được sử dụng

Sau khi hiểu kiến trúc tổng quan, đối chiếu các thành phần trong sơ đồ với các dịch vụ AWS sẽ được thao tác trong workshop.

![Tổng quan các dịch vụ AWS được sử dụng trong workshop](/eam-workshop-report/images/5-Workshop/5.1-Workshop-overview/5.1.2-aws-services-overview.png)

*Hình 5.1.2. Tổng quan các dịch vụ AWS được sử dụng trong workshop.*

Danh sách dịch vụ cần đối chiếu với phạm vi workshop, gồm Amplify, API Gateway, Elastic Beanstalk, RDS, SES và CloudWatch.

## Giới hạn của môi trường demo

Workshop này được giới hạn cho môi trường demo:

- RDS có thể dùng Single-AZ để giảm chi phí.
- Backend có thể chạy với một Elastic Beanstalk environment nhỏ.
- Amplify dùng domain mặc định.
- Không yêu cầu custom domain với Route 53.
- File upload có thể đi qua backend trong demo; S3 được định hướng cho bản sẵn sàng production.
