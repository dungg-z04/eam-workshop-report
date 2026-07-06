---
title: "Worklog Tuần 11"
date: 2026-06-26
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

## Worklog Tuần 11

**Thời gian:** 26/06/2026 - 02/07/2026

Sau khi hệ thống đã deploy, tuần này tập trung kiểm thử production và xử lý các lỗi phát sinh trong môi trường thật. Đây cũng là giai đoạn bổ sung ảnh chụp và nội dung cho phần workshop của báo cáo.

### Mục tiêu tuần 11:

- Kiểm thử các flow chính trên môi trường Amplify production.
- Sửa lỗi upload ảnh, rewrite `/uploads/*` và tài khoản inactive.
- Bổ sung ảnh chụp, nội dung workshop và tài liệu triển khai.

### Các công việc cần triển khai trong tuần này:

| Ngày | Nội dung thực hiện | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| Thứ 6 | - Kiểm thử login admin qua Amplify và xác nhận API đi qua Amplify rewrite, API Gateway, Elastic Beanstalk. | 26/06/2026 | 26/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 7 | - Sửa lỗi upload ảnh/avatar, kiểm tra `/uploads/*` rewrite và response ảnh trả `200`. | 27/06/2026 | 27/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Chủ nhật | - Sửa logic tài khoản inactive và xác nhận tài khoản ngừng hoạt động không đăng nhập được. | 28/06/2026 | 28/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 2 | - Kiểm thử regression các flow chính: dashboard, tài sản, nhân viên, phòng ban, bàn giao và bảo trì. | 29/06/2026 | 29/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 3 | - Chụp ảnh AWS Console cho workshop: RDS, security group, Elastic Beanstalk, API Gateway và Amplify. | 30/06/2026 | 30/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 4 | - Bổ sung nội dung workshop, mô tả từng ảnh và làm rõ SES/SMTP, Prisma migration. | 01/07/2026 | 01/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thứ 5 | - Chuẩn hóa tài liệu backend/frontend và đối chiếu lại với nội dung worklog/proposal. | 02/07/2026 | 02/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Kết quả đạt được tuần 11:

- Các flow chính như đăng nhập admin, dashboard, quản lý tài sản, nhân viên, phòng ban, bàn giao và bảo trì đã được kiểm thử lại.
- Các lỗi tích hợp quan trọng như upload ảnh và inactive account được xử lý rõ ràng hơn.
- Phần workshop có thêm ảnh chụp AWS Console và mô tả cụ thể cho từng bước triển khai.

### Kế hoạch tuần tiếp theo

- Hoàn thiện báo cáo cuối kỳ, rà soát toàn bộ site Hugo và chuẩn bị nộp.




