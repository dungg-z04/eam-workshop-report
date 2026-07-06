---
title: "Worklog Tuần 10"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

## Worklog Tuần 10

**Thời gian:** 19/06/2026 - 25/06/2026

Tuần này chuyển trọng tâm từ phát triển tính năng sang triển khai AWS. Backend, database, API Gateway và frontend được kết nối thành một luồng chạy thật để kiểm tra hệ thống qua môi trường public.

### Mục tiêu tuần 10:

- Triển khai backend lên Elastic Beanstalk và kết nối RDS MySQL.
- Cấu hình API Gateway làm điểm vào cho backend.
- Deploy frontend bằng Amplify và cấu hình rewrite cho API/upload.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Chuẩn bị RDS MySQL, security group và `DATABASE_URL` cho backend production. | 19/06/2026 | 19/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Tạo source bundle backend và kiểm tra cấu trúc ZIP phù hợp với Elastic Beanstalk Linux. | 20/06/2026 | 20/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Tạo/cấu hình Elastic Beanstalk environment và cập nhật environment properties. | 21/06/2026 | 21/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Cấu hình SES/SMTP, OTP, JWT, rate limit và CORS origin cho backend. | 22/06/2026 | 22/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Kiểm tra health endpoint trực tiếp qua Elastic Beanstalk và xử lý lỗi startup nếu có. | 23/06/2026 | 23/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Tạo API Gateway HTTP API, proxy route, integration đến Elastic Beanstalk và stage deploy. | 24/06/2026 | 24/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Deploy frontend bằng Amplify, cấu hình build settings, `/api/*`, `/uploads/*` rewrite và SPA fallback. | 25/06/2026 | 25/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 10:

- Backend đã được đóng gói, cấu hình environment properties và kiểm tra health endpoint.
- API Gateway đã chuyển tiếp request đến Elastic Beanstalk thông qua proxy route và integration.
- Frontend Amplify đã có build settings, rewrite `/api/*`, `/uploads/*` và SPA fallback để phục vụ ứng dụng production demo.

### Kế hoạch tuần tiếp theo

- Kiểm thử production, xử lý lỗi upload/inactive account và hoàn thiện tài liệu workshop.




