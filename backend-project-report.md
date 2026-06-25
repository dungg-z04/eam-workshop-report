# Báo cáo tổng quan Backend - EAM Workspace

## 1. Mục đích tài liệu

Tài liệu này mô tả chi tiết phần Backend của dự án **EAM Workspace** - hệ thống quản lý tài sản doanh nghiệp. Nội dung được viết theo hướng có thể đưa trực tiếp vào báo cáo thực tập, thuyết minh kỹ thuật, hoặc làm căn cứ để thiết kế slide/thuyết trình.

Tài liệu tập trung vào:

- Mục tiêu và vai trò của Backend trong toàn bộ hệ thống.
- Công nghệ, kiến trúc, luồng xử lý và các module nghiệp vụ.
- Cấu trúc API, xác thực, phân quyền, lưu trữ dữ liệu và triển khai AWS.
- Checklist test Backend khi demo.

Lưu ý: không đưa mật khẩu, token, secret thật vào báo cáo. Các biến môi trường trong tài liệu này chỉ nên dùng dưới dạng placeholder.

## 2. Tổng quan hệ thống

**EAM Workspace** là một ứng dụng quản lý tài sản doanh nghiệp, hỗ trợ doanh nghiệp theo dõi tài sản, nhân viên, phòng ban, bàn giao, bảo trì, kiểm kê, báo cáo và các công việc liên quan đến vòng đời tài sản.

Backend đóng vai trò là lớp xử lý trung tâm của hệ thống:

- Tiếp nhận request từ Frontend.
- Xác thực người dùng và kiểm tra quyền truy cập.
- Xử lý logic nghiệp vụ quản lý tài sản.
- Đọc/ghi dữ liệu vào MySQL thông qua Prisma ORM.
- Trả về dữ liệu đã chuẩn hóa cho giao diện React.
- Phục vụ file upload nội bộ như ảnh đại diện, ảnh tài sản, file đính kèm.
- Gửi email/OTP khi cần.
- Cung cấp health check để kiểm tra trạng thái hệ thống khi deploy lên AWS.

## 3. Vai trò Backend trong kiến trúc tổng thể

Kiến trúc demo/deployment có thể mô tả như sau:

```text
User Browser
    |
    v
AWS Amplify Hosting - React Frontend
    |
    | /api/*
    v
Amazon API Gateway - HTTP API proxy
    |
    v
AWS Elastic Beanstalk - Node.js/Express Backend
    |
    v
Amazon RDS MySQL - enterprise_asset_management
```

Nếu chạy local:

```text
React Vite Frontend - localhost:5173
    |
    v
Express Backend - localhost:5000
    |
    v
Local MySQL/XAMPP hoac RDS MySQL
```

Backend được thiết kế để chạy được cả local và production thông qua biến môi trường.

## 4. Công nghệ sử dụng

| Thành phần | Công nghệ | Vai trò |
| --- | --- | --- |
| Runtime | Node.js | Môi trường chạy Backend |
| Framework | Express.js | Xây dựng REST API |
| Database | MySQL | Lưu trữ dữ liệu nghiệp vụ |
| ORM | Prisma | Quản lý schema, query và migration |
| Authentication | JWT | Đăng nhập và bảo vệ API |
| Password hashing | bcrypt | Băm mật khẩu người dùng |
| Validation | Middleware/request validation pattern | Kiểm tra dữ liệu đầu vào |
| Logging | pino/pino-http | Ghi log request và lỗi hệ thống |
| Security middleware | helmet, cors, rate limit | Tăng an toàn API |
| File upload | multer/static file serving | Xử lý ảnh/file đính kèm |
| Excel import | xlsx | Import nhân viên/tài sản từ file Excel |
| Email | nodemailer | Gửi OTP/email thông báo |
| Deployment | AWS Elastic Beanstalk | Chạy Backend trên AWS |
| Database production | Amazon RDS MySQL | Database cloud |
| API proxy | Amazon API Gateway | Làm HTTPS endpoint và proxy về Backend |

## 5. Cấu trúc thư mục Backend

Cấu trúc Backend được chia theo hướng tách rõ cấu hình, app, routes, controllers/services và Prisma:

```text
backend/
  package.json
  prisma/
    schema.prisma
    seed.js
    migrations/
  src/
    app/
      server.js
      app.js
    config/
      env.js
      database.js
      logger.js
    middleware/
      authenticate.js
      authorize.js
      errorHandler.js
      requestLogger.js
      validation.js
    routes/
      auth.routes.js
      departments.routes.js
      employees.routes.js
      categories.routes.js
      assets.routes.js
      assignments.routes.js
      maintenance.routes.js
      inventory.routes.js
      reports.routes.js
      locations.routes.js
      notifications.routes.js
      faq.routes.js
      feedback.routes.js
      attendance.routes.js
      supportChat.routes.js
    modules/
      auth/
      employees/
      assets/
      assignments/
      maintenance/
      inventory/
      reports/
      settings/
    uploads/
```

Ý nghĩa thiết kế:

- `src/app`: khởi tạo Express app và start server.
- `src/config`: đọc biến môi trường, kết nối database, cấu hình logger.
- `src/middleware`: middleware dùng chung cho xác thực, phân quyền, validate và bắt lỗi.
- `src/routes`: đăng ký endpoint theo từng module.
- `src/modules`: nơi chứa logic nghiệp vụ, service/controller tùy theo cách tổ chức.
- `prisma`: quản lý schema, migration và seed data.

## 6. Luồng khởi động Backend

Khi chạy Backend, server thực hiện các bước chính:

1. Đọc biến môi trường từ `.env` hoặc environment properties trên AWS.
2. Validate các biến bắt buộc như `PORT`, `DATABASE_URL`, `JWT_SECRET`.
3. Khởi tạo Prisma Client.
4. Kiểm tra kết nối MySQL/RDS.
5. Tạo Express app.
6. Gần middleware bảo mật, CORS, JSON parser, static upload, logger.
7. Đăng ký routes API.
8. Gần middleware xử lý 404 và error handler.
9. Listen trên port cấu hình.

Local thuong dùng:

```powershell
cd backend
npm install
npx prisma generate
npx prisma db push
npx prisma db seed
npm run dev
```

Production trên Elastic Beanstalk thuong dùng port:

```env
PORT=8080
NODE_ENV=production
```

## 7. Chuẩn API

Backend sử dùng REST API theo prefix:

```text
/api
```

Dạng response chung:

```json
{
  "success": true,
  "message": "OK",
  "data": {}
}
```

Dạng response lỗi:

```json
{
  "success": false,
  "message": "Internal server error",
  "errorCode": "INTERNAL_SERVER_ERROR",
  "requestId": "uuid"
}
```

Một số đặc điểm:

- Mỗi request có `requestId` để truy vết lỗi.
- API lỗi 401 khi chưa đăng nhập.
- API lỗi 403 khi không đủ quyền hoặc tài khoản bị khóa.
- API lỗi 404 khi không tìm thấy resource.
- API lỗi 500 khi có lỗi hệ thống/database.

## 8. Xác thực và phân quyền

### 8.1 Đăng nhập

Người dùng đăng nhập bảng email và password:

```http
POST /api/auth/login
```

Backend kiểm tra:

1. Email có tồn tại không.
2. Mật khẩu có khớp hash không.
3. Tài khoản có đang active không.
4. Nhân viên liên kết với tài khoản có bị ngừng hoạt động không.
5. Role của người dùng là gì.
6. Có cần đổi mật khẩu lan đầu không.

Nếu hợp lệ, Backend trả về JWT access token và thông tin user.

### 8.2 JWT

JWT được dùng để bảo vệ API. Frontend gửi token trong header:

```http
Authorization: Bearer <access_token>
```

Token gồm các thông tin cần thiết:

- `userId`
- `email`
- `role`
- thời gian hết hạn

### 8.3 Middleware authenticate

Middleware `authenticate` có nhiệm vụ:

- Đọc token từ request header.
- Verify token bằng `JWT_SECRET`.
- Gắn thông tin user vào `req.user`.
- Từ chối request nếu token thiếu, sai hoặc hết hạn.

### 8.4 Middleware authorize

Middleware `authorize` kiểm tra role của user:

```text
ADMIN: quản lý hệ thống trong phạm vi doanh nghiệp
USER: nhân viên sử dụng tài sản
```

Hướng mở rộng trong báo cáo có thể nêu:

```text
SYSTEM_ADMIN: quản lý nền tảng SaaS
ORGANIZATION_OWNER: chủ workspace doanh nghiệp
ADMIN: quản trị nhân sự và tài sản trong doanh nghiệp
USER: nhân viên sử dụng tài sản
```

Trong MVP hiện tại, dự án tập trung vào `ADMIN` và `USER` để đảm bảo demo chạy trọn vẹn.

### 8.5 Tài khoản ngừng hoạt động

Tài khoản/nhân viên ngừng hoạt động không được phép đăng nhập. Khi login, Backend nên trả về:

```json
{
  "success": false,
  "message": "Account is inactive",
  "errorCode": "AUTH_ACCOUNT_INACTIVE"
}
```

Đây là lượng quản trong khi demo tính năng quản trị nhân viên.

## 9. Các module nghiệp vụ chính

### 9.1 Auth module

Chuc nang:

- Đăng nhập.
- Lấy thông tin user hiện tại.
- Đời mật khẩu.
- Yêu cầu đời mật khẩu lan đầu.
- Kiểm tra trạng thái tài khoản.

Endpoint tiêu biểu:

```http
POST /api/auth/login
GET /api/auth/me
POST /api/auth/change-password
```

### 9.2 Departments module

Chuc nang:

- Tạo phòng ban.
- Cập nhật phòng ban.
- Xóa/khóa phòng ban nếu hợp lệ.
- Tìm kiếm theo tên/mô tả.
- Quản lý người phụ trách phòng ban.

Endpoint tiêu biểu:

```http
GET /api/departments
POST /api/departments
PUT /api/departments/:id
DELETE /api/departments/:id
```

### 9.3 Employees module

Chuc nang:

- Quản lý hồ sơ nhân viên.
- Gần phòng ban, chức vụ, trạng thái.
- Tạo tài khoản user cho nhân viên.
- Khóa/ngừng hoạt động nhân viên.
- Cập nhật ảnh đại diện.
- Quản lý tài liệu định kèm.
- Import nhân viên từ Excel.

Endpoint tiêu biểu:

```http
GET /api/employees
GET /api/employees/:id
POST /api/employees
PUT /api/employees/:id
PATCH /api/employees/:id/status
POST /api/employees/import
POST /api/employees/:id/avatar
```

### 9.4 Categories module

Chuc nang:

- Quản lý danh mục tài sản.
- Tìm kiếm danh mục.
- Theo dõi số lượng tài sản theo danh mục.

Endpoint tiêu biểu:

```http
GET /api/categories
POST /api/categories
PUT /api/categories/:id
DELETE /api/categories/:id
```

### 9.5 Assets module

Chuc nang:

- Tạo tài sản.
- Cập nhật thông tin tài sản.
- Gắn danh mục, serial number, giá trị, vị trí.
- Gần ảnh tài sản.
- Lọc theo trạng thái, danh mục, phòng ban, người sử dụng.
- Import tài sản từ Excel.
- Quản lý tọa độ hiển thị trên sơ đồ mặt bằng.

Trạng thái tài sản có thể gồm:

```text
AVAILABLE
ASSIGNED
MAINTENANCE
BROKEN
RETIRED
LOST
```

Endpoint tiêu biểu:

```http
GET /api/assets
GET /api/assets/:id
POST /api/assets
PUT /api/assets/:id
PATCH /api/assets/:id/status
POST /api/assets/import
POST /api/assets/:id/image
```

### 9.6 Assignment module

Chuc nang:

- Bàn giao tài sản cho nhân viên.
- Thử hồi tài sản.
- Chuyển tài sản từ nhân viên này sang nhân viên khác.
- Lưu lịch sử bàn giao.
- Nhân viên xác nhận đã nhân/trả tài sản.
- Lưu chữ ký xác nhận nếu có.

Endpoint tiêu biểu:

```http
GET /api/assignments/history
GET /api/assignments/my
GET /api/assignments/history/my
POST /api/assignments/assign
POST /api/assignments/:id/return
POST /api/assignments/:id/transfer
POST /api/assignments/:id/confirm
```

### 9.7 Maintenance và support module

Chuc nang:

- Nhân viên báo hỏng tài sản.
- Admin tiếp nhận yêu cầu bảo trì.
- Cập nhật trạng thái xử lý.
- Lưu lịch sử sự kiện của yêu cầu.
- Gần độ ưu tiên, người phụ trách, ghi chú.

Endpoint tiêu biểu:

```http
GET /api/maintenance-requests
POST /api/maintenance-requests
PUT /api/maintenance-requests/:id
GET /api/support-requests
POST /api/support-requests
```

### 9.8 Inventory module

Chuc nang:

- Tạo phiên kiểm kê.
- Gán danh sách tài sản cần kiểm kê.
- Cập nhật kết quả kiểm kê.
- Theo dõi tài sản khớp, lệch, thiếu, hỏng.
- Tổng hợp báo cáo sau kiểm kê.

Endpoint tiêu biểu:

```http
GET /api/inventory-sessions
POST /api/inventory-sessions
GET /api/inventory-sessions/:id
PUT /api/inventory-sessions/:id
POST /api/inventory-sessions/:id/items
```

### 9.9 Reports module

Chuc nang:

- Báo cáo tổng quan tài sản.
- Báo cáo tài sản theo phòng ban.
- Báo cáo chất lượng dữ liệu.
- Báo cáo trạng thái tài sản.
- Báo cáo bảo trì/kiểm kê.
- Xuat dữ liệu cho dashboard.

Endpoint tiêu biểu:

```http
GET /api/reports/summary
GET /api/reports/assets
GET /api/reports/assets-by-department
GET /api/reports/data-quality
```

### 9.10 Locations và floor map module

Chuc nang:

- Quản lý vị trí/văn phòng.
- Lưu tọa độ tài sản trên sơ đồ mặt bằng.
- Hỗ trợ Frontend hiển thị bản đồ vị trí tài sản trong văn phòng.

Endpoint tiêu biểu:

```http
GET /api/locations
POST /api/locations
PUT /api/locations/:id
```

### 9.11 FAQ, feedback và settings module

Chuc nang:

- Quản lý FAQ/cẩm nang tự phục vụ.
- Nhân góp ý và phản hồi từ nhân viên.
- Hỗ trợ file đính kèm feedback.
- Admin thấy đời trạng thái xử lý.

Endpoint tiêu biểu:

```http
GET /api/faqs
POST /api/faqs
PUT /api/faqs/:id
PATCH /api/faqs/:id/status
GET /api/feedbacks
POST /api/feedbacks
PUT /api/feedbacks/:id
```

### 9.12 Attendance và login history

Chuc nang:

- Ghi nhân check-in/check-out.
- Lưu lịch sử chấm công.
- Lưu lịch sử đăng nhập.
- Admin xem và tìm kiếm lịch sử.

Endpoint tiêu biểu:

```http
GET /api/attendance/status
POST /api/attendance/check-in
POST /api/attendance/check-out
GET /api/attendance/my-history
GET /api/login-histories
```

### 9.13 Notifications module

Chuc nang:

- Tạo thông báo khi có sử kiến mới.
- Đếm số thông báo chưa đọc.
- Đánh dấu đã đọc.

Endpoint tiêu biểu:

```http
GET /api/notifications
GET /api/notifications/unread-count
PATCH /api/notifications/:id/read
```

### 9.14 Support chất module

Chuc nang:

- Nhân viên tạo phiên chat hỗ trợ.
- Admin xem danh sách phiên chat.
- Gửi/nhân tin nhắn.
- Lưu lịch sử trao đời.

Endpoint tiêu biểu:

```http
GET /api/support-chat/admin/sessions
GET /api/support-chat/sessions/:id/messages
POST /api/support-chat/sessions/:id/messages
```

## 10. Mô hình dữ liệu chính

| Bảng/Model | Vai trò |
| --- | --- |
| `users` | Tài khoản đăng nhập, email, password hash, role, trạng thái |
| `employees` | Hồ sơ nhân viên, phòng ban, chức vụ, thông tin cá nhân |
| `departments` | Phòng ban trong doanh nghiệp |
| `asset_categories` | Danh mục tài sản |
| `assets` | Tài sản, serial, giá trị, trạng thái, hình ảnh, vị trí |
| `asset_assignments` | Lịch sử bàn giao/thu hồi/chuyển giao tài sản |
| `maintenance_requests` | Yêu cầu bảo trì/sửa chữa |
| `support_request_events` | Lịch sử xử lý yêu cầu hỗ trợ/bảo trì |
| `inventory_sessions` | Phiên kiểm kê |
| `inventory_items` | Kết quả kiểm kê từng tài sản |
| `locations` | Vị trí/văn phòng/tọa độ sơ đồ |
| `notifications` | Thông báo trong hệ thống |
| `faqs` | Câu hỏi thường gặp/cẩm nang tự phục vụ |
| `feedbacks` | Góp ý và phản hồi của nhân viên |
| `login_histories` | Lịch sử đăng nhập |
| `time_attendances` | Dữ liệu chấm công |
| `user_tasks` | Công việc cần làm của nhân viên |
| `chat_sessions` | Phiên chat hỗ trợ |
| `chat_messages` | Tin nhắn trong chat |
| `employee_attachments` | File đính kèm hồ sơ nhân viên |
| `employee_profile_logs` | Lịch sử cập nhật hồ sơ |
| `department_asset_quotas` | Hạn mức tài sản theo phòng ban |
| `department_audit_logs` | Nhật ký thay đổi phòng ban |
| `password_reset_otps` | OTP đặt lại mật khẩu |

## 11. Biến môi trường Backend

Không nên đưa giá trị thật vào báo cáo. Nên viết theo dạng:

```env
NODE_ENV=production
PORT=8080

DATABASE_URL=mysql://<db_user>:<db_password>@<rds-endpoint>:3306/enterprise_asset_management

JWT_SECRET=<long-random-secret>
JWT_EXPIRES_IN=1h
DEFAULT_USER_PASSWORD=<default-password-for-demo>

FRONTEND_ORIGIN=https://<amplify-domain>
FRONTEND_ORIGINS=https://<amplify-domain>

MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_SECURE=false
MAIL_USER=<mail-user>
MAIL_PASSWORD=<mail-app-password>
MAIL_FROM=<mail-from-address>

OTP_EXPIRES_SECONDS=60
OTP_MAX_ATTEMPTS=3

RATE_LIMIT_BUCKET_CAPACITY=60
RATE_LIMIT_REFILL_TOKENS_PER_SECOND=1
RATE_LIMIT_TOKENS_PER_REQUEST=1
```

Ý nghĩa quan trọng:

- `DATABASE_URL`: chuỗi kết nối MySQL/RDS.
- `JWT_SECRET`: khóa ký token, phải là chuỗi dài random.
- `FRONTEND_ORIGIN(S)`: domain Frontend được phép gọi API.
- `PORT`: trên Elastic Beanstalk nên dùng `8080`.
- `MAIL_*`: cấu hình SMTP để gửi email.

## 12. Bảo mật

Backend có các lớp bảo vệ chính:

- Hash password bằng bcrypt.
- Xác thực request bằng JWT.
- Phân quyền bằng role.
- Kiểm tra account/employee inactive khi đăng nhập.
- CORS chỉ cho phép domain Frontend hợp lệ.
- Helmet để them security headers.
- Rate limit để giảm spam/brute force.
- Không lưu secret vào source code.
- Không public log chứa password/token.
- Validate file upload và giới hạn loại file.

## 13. Import Excel

Backend hỗ trợ import dữ liệu từ file Excel cho:

- Nhân viên.
- Tài sản.

Luồng xử lý import:

1. Frontend upload file `.xlsx`.
2. Backend đọc workbook bằng thư viện Excel.
3. Kiểm tra sheet và cột bắt buộc.
4. Parse từng dòng thành object.
5. Validate dữ liệu: email, mã nhân viên, tên, phòng ban, serial number...
6. Tạo bản ghi mới hoặc báo lỗi dòng sai.
7. Trả về kết quả: tổng dòng thành công, dòng lỗi, lý do lỗi.

Đây là tính năng ghi điểm khi demo vì giải quyết được bài toán nhập liệu số lượng lớn.

## 14. File upload

Backend phục vụ file upload cho:

- Ảnh đại diện nhân viên.
- Ảnh tài sản.
- File đính kèm feedback.
- Tài liệu hồ sơ nhân viên.

Trong demo hiện tại có thể dùng local file storage trên Elastic Beanstalk instance. Khi lên production thật, nên cần nhac chuyển sáng Amazon S3 để:

- Không mất file khi instance bị thấy thế.
- Để scale nhiều instance.
- Có URL ổn định hon.
- Quản lý quyền truy cập tot hon.

## 15. Health check

Endpoint health check:

```http
GET /api/health
```

Response thành công:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

Endpoint này được dùng để:

- Kiểm tra Backend local.
- Kiểm tra Elastic Beanstalk health.
- Kiểm tra API Gateway proxy.
- Kiểm tra Amplify rewrite `/api`.

## 16. Seed data

Seed data giup demo nhanh mã không cần nhập tay:

- Admin account.
- Employee account active.
- Employee first-login account.
- Employee inactive account.
- Phòng ban.
- Nhân viên.
- Danh mục tài sản.
- Tài sản.
- Bàn giao.
- Bảo trì.
- Kiểm kê.
- FAQ.
- Feedback.
- Locations.

Lenh:

```powershell
cd backend
npx prisma db seed
```

Tài khoản demo nên được ghi riêng trong phụ lục báo cáo hoặc script demo, không đưa mật khẩu production thật.

## 17. Deployment Backend trên AWS

Thành phần dùng trong deployment:

- **Elastic Beanstalk**: chạy Node.js Express Backend.
- **RDS MySQL**: lưu database production/demo.
- **API Gateway HTTP API**: tạo HTTPS endpoint và proxy request `/api`.
- **Security Group**: cho phép EB instance kết nối RDS port 3306.
- **CloudWatch/EB logs**: theo dõi lỗi và health.

Lượng deploy tom tất:

1. Tạo RDS MySQL.
2. Chạy migration/db push vào RDS.
3. Seed dữ liệu demo.
4. Tạo source bundle Backend `.zip`.
5. Tạo Elastic Beanstalk environment Node.js.
6. Them environment properties.
7. Kiểm tra `GET /api/health`.
8. Tạo API Gateway proxy về EB.
9. Kiểm tra HTTPS API Gateway.
10. Cấu hình Amplify rewrite `/api/*`.

## 18. Checklist test Backend

### 18.1 Test health

```powershell
Invoke-RestMethod "http://localhost:5000/api/health"
Invoke-RestMethod "https://<api-gateway-domain>/api/health"
```

### 18.2 Test login admin

```powershell
Invoke-RestMethod `
  -Uri "https://<frontend-domain>/api/auth/login" `
  -Method Post `
  -ContentType "application/json" `
  -Headers @{ Origin = "https://<frontend-domain>" } `
  -Body '{"email":"admin@company.local","password":"Admin123"}'
```

### 18.3 Test inactive account

Kết quả dùng là API phải trả về `AUTH_ACCOUNT_INACTIVE`.

```powershell
Invoke-RestMethod `
  -Uri "https://<frontend-domain>/api/auth/login" `
  -Method Post `
  -ContentType "application/json" `
  -Headers @{ Origin = "https://<frontend-domain>" } `
  -Body '{"email":"inactive.employee@company.local","password":"Inactive123"}'
```

### 18.4 Test CRUD core

- Tạo phòng ban.
- Sửa phòng ban.
- Tạo nhân viên.
- Khóa nhân viên.
- Tạo danh mục.
- Tạo tài sản.
- Gần tài sản cho nhân viên.
- Thử hồi tài sản.

### 18.5 Test module nang cáo

- Import Excel nhân viên.
- Import Excel tài sản.
- Báo hỏng tài sản.
- Tạo phiên kiểm kê.
- Xem báo cáo.
- Gửi feedback có file đính kèm.
- Cập nhật avatar.

## 19. Điểm nội bắt Backend để đưa vào báo cáo

- Backend không chỉ làm CRUD đơn gìản mã xử lý được vòng đời tài sản.
- Có phân quyền rõ gìữa admin và nhân viên.
- Có xác thực JWT và bảo vệ API.
- Có kết nối Prisma/MySQL, có seed data để demo.
- Có workflow bàn giao, bảo trì, kiểm kê và báo cáo.
- Có import Excel, upload file, notification, FAQ, feedback, login history.
- Có khả năng deploy lên AWS với RDS, Elastic Beanstalk, API Gateway và Amplify.
- Có health check và requestId giup debug khi triển khai.

## 20. Đoạn mô tả ngắn có thể đưa vào báo cáo

Backend của EAM Workspace được xây dựng bảng Node.js và Express.js, sử dùng Prisma ORM để giao tiếp với MySQL. Hệ thống cung cấp các REST API cho toàn bộ nghiệp vụ quản lý tài sản doanh nghiệp, báo gồm quản lý nhân viên, phòng ban, danh mục, tài sản, bàn giao, bảo trì, kiểm kê, báo cáo, FAQ, feedback và thông báo. Backend áp dụng JWT authentication, role-based authorization, password hashing, CORS, rate limiting và centralized error handling để đảm bảo tính án toàn và khả năng bảo trì. Trong mới trường demo, Backend được deploy lên AWS Elastic Beanstalk, kết nối Amazon RDS MySQL và được public thông qua API Gateway để Frontend trên AWS Amplify có thể truy cập bảng HTTPS.
