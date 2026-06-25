---
title: "Kiểm thử, monitoring và xử lý lỗi"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Kiểm thử, monitoring và xử lý lỗi

Sau khi frontend và backend đã deploy, cần kiểm thử toàn bộ hệ thống và kiểm tra log vận hành.

## Test 1: Backend health

Mở:

```text
https://<amplify-domain>/api/health
```

hoặc:

```text
http://<alb-dns-name>/api/health
```

Kết quả mong đợi:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

Nếu lỗi, kiểm tra ALB target health và Elastic Beanstalk logs.

## Test 2: Admin login

Mở URL Amplify và đăng nhập bằng tài khoản admin từ seed data.

Kết quả mong đợi:

- User được redirect đến `/admin/dashboard`.
- Dashboard metrics hiển thị.
- Sidebar và navigation hoạt động.
- API call trả `200` hoặc response nghiệp vụ mong đợi.

## Test 3: Workflow admin chính

Kiểm thử ít nhất một workflow từ mỗi module admin lớn:

| Module | Hành động kiểm thử |
| --- | --- |
| Categories | Tạo hoặc tìm kiếm danh mục tài sản. |
| Assets | Tạo, cập nhật hoặc tìm kiếm tài sản. |
| Employees | Xem danh sách nhân viên và chi tiết nhân viên. |
| Departments | Xem hoặc cập nhật thông tin phòng ban. |
| Assignments | Bàn giao tài sản available cho nhân viên. |
| Maintenance | Tạo hoặc cập nhật yêu cầu hỗ trợ/bảo trì. |
| Inventory | Xem hoặc tạo phiên kiểm kê. |
| Reports | Mở báo cáo tổng quan hoặc báo cáo tài sản. |

## Test 4: Workflow nhân viên

Đăng nhập bằng tài khoản nhân viên và kiểm tra:

- Employee dashboard.
- Trang tài sản của tôi.
- Trang chi tiết tài sản.
- Tạo yêu cầu hỗ trợ.
- Trang FAQ.
- Trang hồ sơ và lịch sử.

## Test 5: Browser DevTools

Mở DevTools và kiểm tra tab Network:

- API request nên dùng Amplify domain.
- API path nên bắt đầu bằng `/api`.
- Không có lỗi CORS.
- Request lỗi cần có status code rõ ràng.

## Monitoring với CloudWatch

Mở CloudWatch Logs và kiểm tra log group của Elastic Beanstalk.

Cần kiểm tra:

- Log startup backend.
- Request log.
- Lỗi authentication.
- Lỗi kết nối database.
- Exception chưa được xử lý.

Các endpoint hữu ích:

```text
GET /api/health
POST /api/auth/login
GET /api/assets
GET /api/reports/summary
```

## Alarm đề xuất

Với môi trường demo, có thể tạo các CloudWatch alarm đơn giản:

| Alarm | Mục đích |
| --- | --- |
| EC2 high CPU | Phát hiện backend instance quá tải. |
| ALB unhealthy targets | Phát hiện lỗi health của backend. |
| RDS CPU hoặc storage | Phát hiện vấn đề capacity của database. |
| 5xx errors | Phát hiện lỗi application hoặc infrastructure. |

## Hướng dẫn xử lý lỗi

| Vấn đề | Nguyên nhân thường gặp | Cách xử lý |
| --- | --- | --- |
| `502 Bad Gateway` | Backend crash hoặc sai port | Kiểm tra `PORT=8080`, EB logs và target group health. |
| CORS error | `FRONTEND_ORIGIN` sai | Set đúng URL Amplify và redeploy backend. |
| Không kết nối được database | RDS endpoint hoặc security group sai | Kiểm tra `DATABASE_URL` và cho phép `3306` từ backend SG. |
| `/api/...` trả frontend HTML | Thứ tự Amplify rewrite sai | Đưa `/api/<*>` lên trên SPA fallback rule. |
| Login fail | Seed data hoặc JWT config có vấn đề | Kiểm tra seed data, `JWT_SECRET` và backend logs. |
| Upload không bền vững | Đang dùng local instance storage | Chuyển upload storage sang S3 cho production-ready deployment. |

## Checklist xác nhận

- [ ] Frontend mở được từ Amplify URL.
- [ ] `GET /api/health` trả success.
- [ ] Admin login hoạt động.
- [ ] Employee login hoạt động.
- [ ] Workflow CRUD chính hoạt động.
- [ ] Workflow bàn giao tài sản hoạt động.
- [ ] Workflow yêu cầu hỗ trợ hoạt động.
- [ ] CloudWatch Logs có log backend.
- [ ] Không có lỗi CORS trong browser DevTools.
