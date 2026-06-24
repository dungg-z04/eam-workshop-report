# Bao cao tong quan Backend - EAM Workspace

## 1. Muc dich tai lieu

Tai lieu nay mo ta chi tiet phan Backend cua du an **EAM Workspace** - he thong quan ly tai san doanh nghiep. Noi dung duoc viet theo huong co the dua truc tiep vao bao cao thuc tap, thuyet minh ky thuat, hoac lam can cu de thiet ke slide/thuyet trinh.

Tai lieu tap trung vao:

- Muc tieu va vai tro cua Backend trong toan bo he thong.
- Cong nghe, kien truc, luong xu ly va cac module nghiep vu.
- Cau truc API, xac thuc, phan quyen, luu tru du lieu va trien khai AWS.
- Checklist test Backend khi demo.

Luu y: khong dua mat khau, token, secret that vao bao cao. Cac bien moi truong trong tai lieu nay chi nen dung duoi dang placeholder.

## 2. Tong quan he thong

**EAM Workspace** la mot ung dung quan ly tai san doanh nghiep, ho tro doanh nghiep theo doi tai san, nhan vien, phong ban, ban giao, bao tri, kiem ke, bao cao va cac cong viec lien quan den vong doi tai san.

Backend dong vai tro la lop xu ly trung tam cua he thong:

- Tiep nhan request tu Frontend.
- Xac thuc nguoi dung va kiem tra quyen truy cap.
- Xu ly logic nghiep vu quan ly tai san.
- Doc/ghi du lieu vao MySQL thong qua Prisma ORM.
- Tra ve du lieu da chuan hoa cho giao dien React.
- Phuc vu file upload noi bo nhu anh dai dien, anh tai san, file dinh kem.
- Gui email/OTP khi can.
- Cung cap health check de kiem tra trang thai he thong khi deploy len AWS.

## 3. Vai tro Backend trong kien truc tong the

Kien truc demo/deployment co the mo ta nhu sau:

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

Neu chay local:

```text
React Vite Frontend - localhost:5173
    |
    v
Express Backend - localhost:5000
    |
    v
Local MySQL/XAMPP hoac RDS MySQL
```

Backend duoc thiet ke de chay duoc ca local va production thong qua bien moi truong.

## 4. Cong nghe su dung

| Thanh phan | Cong nghe | Vai tro |
| --- | --- | --- |
| Runtime | Node.js | Moi truong chay Backend |
| Framework | Express.js | Xay dung REST API |
| Database | MySQL | Luu tru du lieu nghiep vu |
| ORM | Prisma | Quan ly schema, query va migration |
| Authentication | JWT | Dang nhap va bao ve API |
| Password hashing | bcrypt | Bam mat khau nguoi dung |
| Validation | Middleware/request validation pattern | Kiem tra du lieu dau vao |
| Logging | pino/pino-http | Ghi log request va loi he thong |
| Security middleware | helmet, cors, rate limit | Tang an toan API |
| File upload | multer/static file serving | Xu ly anh/file dinh kem |
| Excel import | xlsx | Import nhan vien/tai san tu file Excel |
| Email | nodemailer | Gui OTP/email thong bao |
| Deployment | AWS Elastic Beanstalk | Chay Backend tren AWS |
| Database production | Amazon RDS MySQL | Database cloud |
| API proxy | Amazon API Gateway | Lam HTTPS endpoint va proxy ve Backend |

## 5. Cau truc thu muc Backend

Cau truc Backend duoc chia theo huong tach ro cau hinh, app, routes, controllers/services va Prisma:

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

Y nghia thiet ke:

- `src/app`: khoi tao Express app va start server.
- `src/config`: doc bien moi truong, ket noi database, cau hinh logger.
- `src/middleware`: middleware dung chung cho xac thuc, phan quyen, validate va bat loi.
- `src/routes`: dang ky endpoint theo tung module.
- `src/modules`: noi chua logic nghiep vu, service/controller tuy theo cach to chuc.
- `prisma`: quan ly schema, migration va seed data.

## 6. Luong khoi dong Backend

Khi chay Backend, server thuc hien cac buoc chinh:

1. Doc bien moi truong tu `.env` hoac environment properties tren AWS.
2. Validate cac bien bat buoc nhu `PORT`, `DATABASE_URL`, `JWT_SECRET`.
3. Khoi tao Prisma Client.
4. Kiem tra ket noi MySQL/RDS.
5. Tao Express app.
6. Gan middleware bao mat, CORS, JSON parser, static upload, logger.
7. Dang ky routes API.
8. Gan middleware xu ly 404 va error handler.
9. Listen tren port cau hinh.

Local thuong dung:

```powershell
cd backend
npm install
npx prisma generate
npx prisma db push
npx prisma db seed
npm run dev
```

Production tren Elastic Beanstalk thuong dung port:

```env
PORT=8080
NODE_ENV=production
```

## 7. Chuan API

Backend su dung REST API theo prefix:

```text
/api
```

Dang response chung:

```json
{
  "success": true,
  "message": "OK",
  "data": {}
}
```

Dang response loi:

```json
{
  "success": false,
  "message": "Internal server error",
  "errorCode": "INTERNAL_SERVER_ERROR",
  "requestId": "uuid"
}
```

Mot so dac diem:

- Moi request co `requestId` de truy vet loi.
- API loi 401 khi chua dang nhap.
- API loi 403 khi khong du quyen hoac tai khoan bi khoa.
- API loi 404 khi khong tim thay resource.
- API loi 500 khi co loi he thong/database.

## 8. Xac thuc va phan quyen

### 8.1 Dang nhap

Nguoi dung dang nhap bang email va password:

```http
POST /api/auth/login
```

Backend kiem tra:

1. Email co ton tai khong.
2. Mat khau co khop hash khong.
3. Tai khoan co dang active khong.
4. Nhan vien lien ket voi tai khoan co bi ngung hoat dong khong.
5. Role cua nguoi dung la gi.
6. Co can doi mat khau lan dau khong.

Neu hop le, Backend tra ve JWT access token va thong tin user.

### 8.2 JWT

JWT duoc dung de bao ve API. Frontend gui token trong header:

```http
Authorization: Bearer <access_token>
```

Token gom cac thong tin can thiet:

- `userId`
- `email`
- `role`
- thoi gian het han

### 8.3 Middleware authenticate

Middleware `authenticate` co nhiem vu:

- Doc token tu request header.
- Verify token bang `JWT_SECRET`.
- Gan thong tin user vao `req.user`.
- Tu choi request neu token thieu, sai hoac het han.

### 8.4 Middleware authorize

Middleware `authorize` kiem tra role cua user:

```text
ADMIN: quan ly he thong trong pham vi doanh nghiep
USER: nhan vien su dung tai san
```

Huong mo rong trong bao cao co the neu:

```text
SYSTEM_ADMIN: quan ly nen tang SaaS
ORGANIZATION_OWNER: chu workspace doanh nghiep
ADMIN: quan tri nhan su va tai san trong doanh nghiep
USER: nhan vien su dung tai san
```

Trong MVP hien tai, du an tap trung vao `ADMIN` va `USER` de dam bao demo chay tron ven.

### 8.5 Tai khoan ngung hoat dong

Tai khoan/nhan vien ngung hoat dong khong duoc phep dang nhap. Khi login, Backend nen tra ve:

```json
{
  "success": false,
  "message": "Account is inactive",
  "errorCode": "AUTH_ACCOUNT_INACTIVE"
}
```

Day la luong quan trong khi demo tinh nang quan tri nhan vien.

## 9. Cac module nghiep vu chinh

### 9.1 Auth module

Chuc nang:

- Dang nhap.
- Lay thong tin user hien tai.
- Doi mat khau.
- Yeu cau doi mat khau lan dau.
- Kiem tra trang thai tai khoan.

Endpoint tieu bieu:

```http
POST /api/auth/login
GET /api/auth/me
POST /api/auth/change-password
```

### 9.2 Departments module

Chuc nang:

- Tao phong ban.
- Cap nhat phong ban.
- Xoa/khoa phong ban neu hop le.
- Tim kiem theo ten/mo ta.
- Quan ly nguoi phu trach phong ban.

Endpoint tieu bieu:

```http
GET /api/departments
POST /api/departments
PUT /api/departments/:id
DELETE /api/departments/:id
```

### 9.3 Employees module

Chuc nang:

- Quan ly ho so nhan vien.
- Gan phong ban, chuc vu, trang thai.
- Tao tai khoan user cho nhan vien.
- Khoa/ngung hoat dong nhan vien.
- Cap nhat anh dai dien.
- Quan ly tai lieu dinh kem.
- Import nhan vien tu Excel.

Endpoint tieu bieu:

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

- Quan ly danh muc tai san.
- Tim kiem danh muc.
- Theo doi so luong tai san theo danh muc.

Endpoint tieu bieu:

```http
GET /api/categories
POST /api/categories
PUT /api/categories/:id
DELETE /api/categories/:id
```

### 9.5 Assets module

Chuc nang:

- Tao tai san.
- Cap nhat thong tin tai san.
- Gan danh muc, serial number, gia tri, vi tri.
- Gan anh tai san.
- Loc theo trang thai, danh muc, phong ban, nguoi su dung.
- Import tai san tu Excel.
- Quan ly toa do hien thi tren so do mat bang.

Trang thai tai san co the gom:

```text
AVAILABLE
ASSIGNED
MAINTENANCE
BROKEN
RETIRED
LOST
```

Endpoint tieu bieu:

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

- Ban giao tai san cho nhan vien.
- Thu hoi tai san.
- Chuyen tai san tu nhan vien nay sang nhan vien khac.
- Luu lich su ban giao.
- Nhan vien xac nhan da nhan/tra tai san.
- Luu chu ky xac nhan neu co.

Endpoint tieu bieu:

```http
GET /api/assignments/history
GET /api/assignments/my
GET /api/assignments/history/my
POST /api/assignments/assign
POST /api/assignments/:id/return
POST /api/assignments/:id/transfer
POST /api/assignments/:id/confirm
```

### 9.7 Maintenance va support module

Chuc nang:

- Nhan vien bao hong tai san.
- Admin tiep nhan yeu cau bao tri.
- Cap nhat trang thai xu ly.
- Luu lich su su kien cua yeu cau.
- Gan do uu tien, nguoi phu trach, ghi chu.

Endpoint tieu bieu:

```http
GET /api/maintenance-requests
POST /api/maintenance-requests
PUT /api/maintenance-requests/:id
GET /api/support-requests
POST /api/support-requests
```

### 9.8 Inventory module

Chuc nang:

- Tao phien kiem ke.
- Gan danh sach tai san can kiem ke.
- Cap nhat ket qua kiem ke.
- Theo doi tai san khop, lech, thieu, hong.
- Tong hop bao cao sau kiem ke.

Endpoint tieu bieu:

```http
GET /api/inventory-sessions
POST /api/inventory-sessions
GET /api/inventory-sessions/:id
PUT /api/inventory-sessions/:id
POST /api/inventory-sessions/:id/items
```

### 9.9 Reports module

Chuc nang:

- Bao cao tong quan tai san.
- Bao cao tai san theo phong ban.
- Bao cao chat luong du lieu.
- Bao cao trang thai tai san.
- Bao cao bao tri/kiem ke.
- Xuat du lieu cho dashboard.

Endpoint tieu bieu:

```http
GET /api/reports/summary
GET /api/reports/assets
GET /api/reports/assets-by-department
GET /api/reports/data-quality
```

### 9.10 Locations va floor map module

Chuc nang:

- Quan ly vi tri/van phong.
- Luu toa do tai san tren so do mat bang.
- Ho tro Frontend hien thi ban do vi tri tai san trong van phong.

Endpoint tieu bieu:

```http
GET /api/locations
POST /api/locations
PUT /api/locations/:id
```

### 9.11 FAQ, feedback va settings module

Chuc nang:

- Quan ly FAQ/cam nang tu phuc vu.
- Nhan gop y va phan hoi tu nhan vien.
- Ho tro file dinh kem feedback.
- Admin thay doi trang thai xu ly.

Endpoint tieu bieu:

```http
GET /api/faqs
POST /api/faqs
PUT /api/faqs/:id
PATCH /api/faqs/:id/status
GET /api/feedbacks
POST /api/feedbacks
PUT /api/feedbacks/:id
```

### 9.12 Attendance va login history

Chuc nang:

- Ghi nhan check-in/check-out.
- Luu lich su cham cong.
- Luu lich su dang nhap.
- Admin xem va tim kiem lich su.

Endpoint tieu bieu:

```http
GET /api/attendance/status
POST /api/attendance/check-in
POST /api/attendance/check-out
GET /api/attendance/my-history
GET /api/login-histories
```

### 9.13 Notifications module

Chuc nang:

- Tao thong bao khi co su kien moi.
- Dem so thong bao chua doc.
- Danh dau da doc.

Endpoint tieu bieu:

```http
GET /api/notifications
GET /api/notifications/unread-count
PATCH /api/notifications/:id/read
```

### 9.14 Support chat module

Chuc nang:

- Nhan vien tao phien chat ho tro.
- Admin xem danh sach phien chat.
- Gui/nhan tin nhan.
- Luu lich su trao doi.

Endpoint tieu bieu:

```http
GET /api/support-chat/admin/sessions
GET /api/support-chat/sessions/:id/messages
POST /api/support-chat/sessions/:id/messages
```

## 10. Mo hinh du lieu chinh

| Bang/Model | Vai tro |
| --- | --- |
| `users` | Tai khoan dang nhap, email, password hash, role, trang thai |
| `employees` | Ho so nhan vien, phong ban, chuc vu, thong tin ca nhan |
| `departments` | Phong ban trong doanh nghiep |
| `asset_categories` | Danh muc tai san |
| `assets` | Tai san, serial, gia tri, trang thai, hinh anh, vi tri |
| `asset_assignments` | Lich su ban giao/thu hoi/chuyen giao tai san |
| `maintenance_requests` | Yeu cau bao tri/sua chua |
| `support_request_events` | Lich su xu ly yeu cau ho tro/bao tri |
| `inventory_sessions` | Phien kiem ke |
| `inventory_items` | Ket qua kiem ke tung tai san |
| `locations` | Vi tri/van phong/toa do so do |
| `notifications` | Thong bao trong he thong |
| `faqs` | Cau hoi thuong gap/cam nang tu phuc vu |
| `feedbacks` | Gop y va phan hoi cua nhan vien |
| `login_histories` | Lich su dang nhap |
| `time_attendances` | Du lieu cham cong |
| `user_tasks` | Cong viec can lam cua nhan vien |
| `chat_sessions` | Phien chat ho tro |
| `chat_messages` | Tin nhan trong chat |
| `employee_attachments` | File dinh kem ho so nhan vien |
| `employee_profile_logs` | Lich su cap nhat ho so |
| `department_asset_quotas` | Han muc tai san theo phong ban |
| `department_audit_logs` | Nhat ky thay doi phong ban |
| `password_reset_otps` | OTP dat lai mat khau |

## 11. Bien moi truong Backend

Khong nen dua gia tri that vao bao cao. Nen viet theo dang:

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

Y nghia quan trong:

- `DATABASE_URL`: chuoi ket noi MySQL/RDS.
- `JWT_SECRET`: khoa ky token, phai la chuoi dai random.
- `FRONTEND_ORIGIN(S)`: domain Frontend duoc phep goi API.
- `PORT`: tren Elastic Beanstalk nen dung `8080`.
- `MAIL_*`: cau hinh SMTP de gui email.

## 12. Bao mat

Backend co cac lop bao ve chinh:

- Hash password bang bcrypt.
- Xac thuc request bang JWT.
- Phan quyen bang role.
- Kiem tra account/employee inactive khi dang nhap.
- CORS chi cho phep domain Frontend hop le.
- Helmet de them security headers.
- Rate limit de giam spam/brute force.
- Khong luu secret vao source code.
- Khong public log chua password/token.
- Validate file upload va gioi han loai file.

## 13. Import Excel

Backend ho tro import du lieu tu file Excel cho:

- Nhan vien.
- Tai san.

Luong xu ly import:

1. Frontend upload file `.xlsx`.
2. Backend doc workbook bang thu vien Excel.
3. Kiem tra sheet va cot bat buoc.
4. Parse tung dong thanh object.
5. Validate du lieu: email, ma nhan vien, ten, phong ban, serial number...
6. Tao ban ghi moi hoac bao loi dong sai.
7. Tra ve ket qua: tong dong thanh cong, dong loi, ly do loi.

Day la tinh nang ghi diem khi demo vi giai quyet duoc bai toan nhap lieu so luong lon.

## 14. File upload

Backend phuc vu file upload cho:

- Anh dai dien nhan vien.
- Anh tai san.
- File dinh kem feedback.
- Tai lieu ho so nhan vien.

Trong demo hien tai co the dung local file storage tren Elastic Beanstalk instance. Khi len production that, nen can nhac chuyen sang Amazon S3 de:

- Khong mat file khi instance bi thay the.
- De scale nhieu instance.
- Co URL on dinh hon.
- Quan ly quyen truy cap tot hon.

## 15. Health check

Endpoint health check:

```http
GET /api/health
```

Response thanh cong:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

Endpoint nay duoc dung de:

- Kiem tra Backend local.
- Kiem tra Elastic Beanstalk health.
- Kiem tra API Gateway proxy.
- Kiem tra Amplify rewrite `/api`.

## 16. Seed data

Seed data giup demo nhanh ma khong can nhap tay:

- Admin account.
- Employee account active.
- Employee first-login account.
- Employee inactive account.
- Phong ban.
- Nhan vien.
- Danh muc tai san.
- Tai san.
- Ban giao.
- Bao tri.
- Kiem ke.
- FAQ.
- Feedback.
- Locations.

Lenh:

```powershell
cd backend
npx prisma db seed
```

Tai khoan demo nen duoc ghi rieng trong phu luc bao cao hoac script demo, khong dua mat khau production that.

## 17. Deployment Backend tren AWS

Thanh phan dung trong deployment:

- **Elastic Beanstalk**: chay Node.js Express Backend.
- **RDS MySQL**: luu database production/demo.
- **API Gateway HTTP API**: tao HTTPS endpoint va proxy request `/api`.
- **Security Group**: cho phep EB instance ket noi RDS port 3306.
- **CloudWatch/EB logs**: theo doi loi va health.

Luong deploy tom tat:

1. Tao RDS MySQL.
2. Chay migration/db push vao RDS.
3. Seed du lieu demo.
4. Tao source bundle Backend `.zip`.
5. Tao Elastic Beanstalk environment Node.js.
6. Them environment properties.
7. Kiem tra `GET /api/health`.
8. Tao API Gateway proxy ve EB.
9. Kiem tra HTTPS API Gateway.
10. Cau hinh Amplify rewrite `/api/*`.

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

Ket qua dung la API phai tra ve `AUTH_ACCOUNT_INACTIVE`.

```powershell
Invoke-RestMethod `
  -Uri "https://<frontend-domain>/api/auth/login" `
  -Method Post `
  -ContentType "application/json" `
  -Headers @{ Origin = "https://<frontend-domain>" } `
  -Body '{"email":"inactive.employee@company.local","password":"Inactive123"}'
```

### 18.4 Test CRUD core

- Tao phong ban.
- Sua phong ban.
- Tao nhan vien.
- Khoa nhan vien.
- Tao danh muc.
- Tao tai san.
- Gan tai san cho nhan vien.
- Thu hoi tai san.

### 18.5 Test module nang cao

- Import Excel nhan vien.
- Import Excel tai san.
- Bao hong tai san.
- Tao phien kiem ke.
- Xem bao cao.
- Gui feedback co file dinh kem.
- Cap nhat avatar.

## 19. Diem noi bat Backend de dua vao bao cao

- Backend khong chi lam CRUD don gian ma xu ly duoc vong doi tai san.
- Co phan quyen ro giua admin va nhan vien.
- Co xac thuc JWT va bao ve API.
- Co ket noi Prisma/MySQL, co seed data de demo.
- Co workflow ban giao, bao tri, kiem ke va bao cao.
- Co import Excel, upload file, notification, FAQ, feedback, login history.
- Co kha nang deploy len AWS voi RDS, Elastic Beanstalk, API Gateway va Amplify.
- Co health check va requestId giup debug khi trien khai.

## 20. Doan mo ta ngan co the dua vao bao cao

Backend cua EAM Workspace duoc xay dung bang Node.js va Express.js, su dung Prisma ORM de giao tiep voi MySQL. He thong cung cap cac REST API cho toan bo nghiep vu quan ly tai san doanh nghiep, bao gom quan ly nhan vien, phong ban, danh muc, tai san, ban giao, bao tri, kiem ke, bao cao, FAQ, feedback va thong bao. Backend ap dung JWT authentication, role-based authorization, password hashing, CORS, rate limiting va centralized error handling de dam bao tinh an toan va kha nang bao tri. Trong moi truong demo, Backend duoc deploy len AWS Elastic Beanstalk, ket noi Amazon RDS MySQL va duoc public thong qua API Gateway de Frontend tren AWS Amplify co the truy cap bang HTTPS.
