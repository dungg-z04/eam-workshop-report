---
title: "Kiểm thử, monitoring và xử lý lỗi"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Kiểm thử, monitoring và xử lý lỗi

Sau khi frontend, API Gateway và backend đã deploy, cần kiểm thử toàn bộ hệ thống và kiểm tra log vận hành.

## Test 1: Backend health

Kiểm tra theo từng lớp:

```text
http://<elastic-beanstalk-domain>/api/health
https://<api-gateway-endpoint>/api/health
https://<amplify-domain>/api/health
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

Nếu lỗi, kiểm tra theo thứ tự: Elastic Beanstalk logs, API Gateway route/integration/stage, rồi Amplify rewrite rule.

## Test 2: Admin login

Mở URL Amplify và đăng nhập bằng tài khoản admin từ seed data.

![Trang đăng nhập trên Amplify domain](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.1-login-page.png)

*Hình 5.6.1. Trang đăng nhập trên Amplify domain.*

Ứng dụng frontend cần mở được từ domain Amplify và form đăng nhập phải hiển thị đầy đủ. Đây là điểm bắt đầu để kiểm thử luồng người dùng.

Kết quả mong đợi:

- User được redirect đến `/admin/dashboard`.
- Dashboard metrics hiển thị.
- Sidebar và navigation hoạt động.
- API call trả `200` hoặc response nghiệp vụ mong đợi.

![Admin dashboard sau khi đăng nhập thành công](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.2-admin-dashboard.png)

*Hình 5.6.2. Admin dashboard sau khi đăng nhập thành công.*

Sau khi đăng nhập admin, dashboard cần hiển thị dữ liệu tổng quan. Điều này xác nhận authentication, API backend và database đang hoạt động cùng nhau.

## Test 3: Workflow admin chính

Kiểm thử ít nhất một workflow từ mỗi module admin lớn:

| Module | Hành động kiểm thử |
| --- | --- |
| Categories | Tạo hoặc tìm kiếm danh mục tài sản. |
| Assets | Tạo, cập nhật hoặc tìm kiếm tài sản. |
| Employees | Xem danh sách nhân viên và chi tiết nhân viên. |
| Departments | Xem hoặc cập nhật thông tin phòng ban. |
| Assignments | Bàn giao tài sản khả dụng cho nhân viên. |
| Maintenance | Tạo hoặc cập nhật yêu cầu hỗ trợ/bảo trì. |
| Inventory | Xem hoặc tạo phiên kiểm kê. |
| Reports | Mở báo cáo tổng quan hoặc báo cáo tài sản. |

![Màn hình quản lý tài sản](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.3-admin-assets.png)

*Hình 5.6.3. Màn hình quản lý tài sản.*

Danh sách tài sản cần hiển thị đúng, đồng thời các thao tác chính như xem, sửa, xóa hoặc nhập Excel phải xuất hiện theo đúng quyền admin.

![Workflow quản lý bàn giao tài sản](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.4-assignment-maintenance.png)

*Hình 5.6.4. Workflow quản lý bàn giao tài sản.*

Ở workflow bàn giao, cần kiểm tra trạng thái tài sản, nhân viên nhận tài sản và lịch sử bàn giao. Đây là luồng nghiệp vụ quan trọng của hệ thống EAM Workspace.

## Test 4: Workflow nhân viên

Đăng nhập bằng tài khoản nhân viên và kiểm tra:

- Employee dashboard.
- Trang tài sản được bàn giao.
- Trang chi tiết tài sản.
- Tạo yêu cầu hỗ trợ.
- Trang FAQ.
- Trang hồ sơ và lịch sử.

![Employee dashboard](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.5-employee-dashboard.png)

*Hình 5.6.5. Employee dashboard sau khi đăng nhập.*

Tại dashboard nhân viên, cần kiểm tra dữ liệu hiển thị theo đúng quyền của tài khoản nhân viên. Người dùng chỉ nên thấy tài sản, yêu cầu hỗ trợ và thông tin cá nhân liên quan đến mình.

## Test 5: Upload và trạng thái tài khoản

Kiểm tra thêm các case đã gặp trong quá trình deploy:

- Upload ảnh/avatar đi qua backend/API và ảnh trả `200`.
- Tài khoản inactive không thể đăng nhập.
- Response lỗi inactive trả đúng mã nghiệp vụ, ví dụ `AUTH_ACCOUNT_INACTIVE`.
- Browser DevTools không có lỗi CORS.

![DevTools Network hiển thị API request thành công](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.6-devtools-network.png)

*Hình 5.6.6. DevTools Network hiển thị các API request thành công.*

Tại tab Network, cần lọc các request `/api/...` và kiểm tra status trả về `200` hoặc mã nghiệp vụ mong đợi. Nếu xuất hiện lỗi CORS hoặc request trả HTML, cần kiểm tra lại Amplify rewrite và backend CORS.

![Tài khoản inactive bị chặn đăng nhập](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.7-inactive-account.png)

*Hình 5.6.7. Tài khoản inactive bị chặn đăng nhập.*

Khi đăng nhập bằng tài khoản inactive, hệ thống cần từ chối truy cập. Kết quả này xác nhận backend có kiểm tra trạng thái tài khoản trước khi cấp quyền vào hệ thống.

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
| Elastic Beanstalk health degraded | Phát hiện environment không ổn định. |
| RDS CPU hoặc storage | Phát hiện vấn đề capacity của database. |
| 5xx errors | Phát hiện lỗi application hoặc infrastructure. |

## Hướng dẫn xử lý lỗi

| Vấn đề | Nguyên nhân thường gặp | Cách xử lý |
| --- | --- | --- |
| `502` hoặc backend không phản hồi | Backend crash hoặc sai port | Kiểm tra `PORT=8080`, EB logs và health endpoint trực tiếp. |
| API Gateway trả `404` | Route, stage, integration hoặc path forwarding sai | Kiểm tra route proxy, endpoint integration, stage đã deploy và đảm bảo backend nhận đúng path `/api/...`. |
| CORS error | `FRONTEND_ORIGIN` hoặc `FRONTEND_ORIGINS` sai | Set đúng URL Amplify và redeploy backend. |
| Không kết nối được database | RDS endpoint hoặc security group sai | Kiểm tra `DATABASE_URL` và cho phép `3306` từ backend SG. |
| `/api/...` trả frontend HTML | Thứ tự Amplify rewrite sai | Đưa `/api/<*>` lên trên SPA fallback rule. |
| Ảnh/avatar upload trả `404` | Amplify chưa rewrite `/uploads/<*>` hoặc backend chưa phục vụ đúng thư mục upload | Thêm `/uploads/<*>` rewrite đến API Gateway, đặt trên SPA fallback và kiểm tra URL ảnh trực tiếp. |
| Static JS/CSS lỗi MIME type | Rewrite rule bắt nhầm static assets | Chỉ rewrite `/api/<*>` và `/uploads/<*>` đến API Gateway, để SPA fallback xử lý route frontend. |
| Login fail | Seed data hoặc JWT config có vấn đề | Kiểm tra seed data, `JWT_SECRET` và backend logs. |
| Upload không bền vững | Đang dùng local instance storage | Chuyển nơi lưu file upload sang S3 cho hướng triển khai sẵn sàng production. |

## Checklist xác nhận

- [ ] Frontend mở được từ Amplify URL.
- [ ] `GET /api/health` trả success qua Elastic Beanstalk.
- [ ] `GET /api/health` trả success qua API Gateway.
- [ ] `GET /api/health` trả success qua Amplify rewrite.
- [ ] Admin login hoạt động.
- [ ] Employee login hoạt động.
- [ ] Workflow CRUD chính hoạt động.
- [ ] Workflow bàn giao tài sản hoạt động.
- [ ] Workflow yêu cầu hỗ trợ hoạt động.
- [ ] Tài khoản inactive bị chặn đăng nhập.
- [ ] Không có lỗi CORS trong browser DevTools.
