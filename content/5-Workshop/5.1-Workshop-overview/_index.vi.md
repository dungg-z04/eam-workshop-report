---
title: "Tổng quan workshop"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 5.1. </b> "
---

## Tổng quan workshop

Mục tiêu của workshop này là triển khai EAM Workspace lên AWS và kiểm thử luồng end-to-end từ trình duyệt đến database.

EAM Workspace có hai trải nghiệm người dùng chính:

- **Admin Portal**: quản lý nhân viên, phòng ban, danh mục, tài sản, bàn giao, yêu cầu bảo trì, phiên kiểm kê, vị trí, báo cáo, feedback, FAQ, lịch sử chấm công, lịch sử đăng nhập và support chat.
- **Employee Portal**: xem tài sản được bàn giao, gửi yêu cầu hỗ trợ, đọc FAQ, cập nhật hồ sơ, đổi mật khẩu và xem lịch sử cá nhân.

Backend cung cấp REST API dưới prefix `/api`. Frontend gọi backend bằng đường dẫn tương đối `/api`, sau đó AWS Amplify rewrite các request API này đến DNS name của Application Load Balancer.

## Kết quả mục tiêu

Sau khi hoàn thành workshop, bạn sẽ có:

- Frontend React được host trên AWS Amplify Hosting.
- Backend Node.js/Express chạy trên AWS Elastic Beanstalk.
- Database MySQL chạy trên Amazon RDS.
- Endpoint `/api/health` hoạt động.
- Luồng trên trình duyệt có thể đăng nhập và gọi backend API thông qua URL Amplify.
- CloudWatch Logs để hỗ trợ kiểm tra lỗi backend.

## Luồng triển khai

{{< mermaid >}}
flowchart TD
    A["Chuẩn bị AWS account và source code"] --> B["Tạo network và RDS MySQL"]
    B --> C["Đóng gói backend source bundle"]
    C --> D["Tạo Elastic Beanstalk environment"]
    D --> E["Chạy Prisma migration"]
    E --> F["Deploy frontend lên Amplify"]
    F --> G["Thêm rewrite rule /api"]
    G --> H["Kiểm thử login và workflow chính"]
    H --> I["Kiểm tra CloudWatch Logs và dọn dẹp"]
{{< /mermaid >}}

## Dịch vụ AWS trong phạm vi

| Dịch vụ | Mục đích |
| --- | --- |
| AWS Amplify Hosting | Host và build frontend React. |
| Application Load Balancer | Entry point public cho backend request. |
| AWS Elastic Beanstalk | Chạy và quản lý backend Node.js. |
| Amazon RDS for MySQL | Lưu dữ liệu ứng dụng. |
| Amazon S3 | Đích lưu trữ production-ready cho file upload. |
| Amazon SES | Gửi OTP và email thông báo. |
| Amazon CloudWatch | Lưu log và hỗ trợ monitoring. |

## Giới hạn của môi trường demo

Workshop này được giới hạn cho môi trường demo:

- RDS có thể dùng Single-AZ để giảm chi phí.
- Backend có thể chạy với một instance.
- Amplify dùng domain mặc định.
- Không yêu cầu custom domain với Route 53.
- Codebase hiện tại có thể dùng local storage cho upload, còn S3 được tài liệu hóa như hướng cải tiến production-ready.
