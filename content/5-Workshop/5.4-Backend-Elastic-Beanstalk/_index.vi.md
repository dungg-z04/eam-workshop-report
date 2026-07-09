---
title: "Triển khai backend bằng Elastic Beanstalk"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Triển khai backend bằng Elastic Beanstalk

Bước này đóng gói backend Node.js/Express và deploy lên AWS Elastic Beanstalk. Backend sẽ nhận request từ API Gateway và kết nối đến Amazon RDS for MySQL.

## Bước 1: Kiểm tra backend local

Từ thư mục backend, cài dependency và kiểm tra backend có thể start:

```bash
cd backend
npm ci
npm start
```

Entry point của backend:

```text
src/app/server.js
```

Ứng dụng cần đọc port từ biến môi trường `PORT`. Khi deploy lên Elastic Beanstalk, dùng:

```env
PORT=8080
```

## Bước 2: Tạo backend source bundle

Tạo file ZIP từ nội dung bên trong thư mục `backend/`. Root của file ZIP phải chứa trực tiếp `package.json`.

Cấu trúc ZIP đúng:

```text
backend-eb-source.zip
  package.json
  package-lock.json
  src/
  prisma/
```

Cấu trúc ZIP sai:

```text
backend-eb-source.zip
  backend/
    package.json
```

Không đưa `.env`, `node_modules` hoặc secret thật vào file ZIP.

![Backend source bundle đúng cấu trúc để deploy lên Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.1-source-bundle.png)

*Hình 5.4.1. Backend source bundle đúng cấu trúc để deploy lên Elastic Beanstalk.*

File ZIP cần có `package.json`, `package-lock.json`, `src/` và `prisma/` nằm trực tiếp ở root. Nếu ZIP chứa thêm thư mục `backend/` bên ngoài, Elastic Beanstalk có thể không start được ứng dụng.

## Bước 3: Tạo Elastic Beanstalk application

Mở Elastic Beanstalk console:

1. Chọn **Create application**.
2. Application name: `eam-backend`.
3. Platform: **Node.js**.
4. Application code: upload file ZIP của backend.
5. Environment name: ví dụ `eam-backend-prod`.
6. Chọn VPC và subnet phù hợp.
7. Gắn backend security group.
8. Tạo environment và chờ quá trình provision hoàn tất.

Nếu environment cũ bị kẹt ở trạng thái `Severe`, `No Data`, `CREATE_FAILED` hoặc `DELETE_FAILED`, có thể tạo environment mới và trỏ về cùng RDS để giảm thời gian xử lý.

![Trang tạo Elastic Beanstalk environment cho backend](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.2-create-eb-environment.png)

*Hình 5.4.2. Trang tạo Elastic Beanstalk environment cho backend.*

Phần tạo environment cần thể hiện đúng application name, environment name, platform Node.js và file source bundle đã upload. Đây là cấu hình nền tảng để backend chạy trên Elastic Beanstalk.

## Bước 4: Cấu hình environment properties

Trong Elastic Beanstalk environment properties, đặt:

```env
NODE_ENV=production
PORT=8080
DATABASE_URL=mysql://<db_user>:<db_password>@<rds-endpoint>:3306/enterprise_asset_management
JWT_SECRET=<long-random-secret>
JWT_EXPIRES_IN=1h
DEFAULT_USER_PASSWORD=<default-demo-password>
OTP_EXPIRES_SECONDS=60
OTP_MAX_ATTEMPTS=3
RATE_LIMIT_BUCKET_CAPACITY=60
RATE_LIMIT_REFILL_TOKENS_PER_SECOND=1
RATE_LIMIT_TOKENS_PER_REQUEST=1
MAIL_HOST=<smtp-host>
MAIL_PORT=<smtp-port>
MAIL_SECURE=false
MAIL_USER=<mail-user>
MAIL_PASSWORD=<mail-password>
MAIL_FROM=<mail-from-address>
FRONTEND_ORIGIN=https://<amplify-domain>
FRONTEND_ORIGINS=https://<amplify-domain>
```

`FRONTEND_ORIGIN` và `FRONTEND_ORIGINS` có thể cập nhật sau khi Amplify tạo URL frontend.

![Environment properties của Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.3-eb-env-properties.png)

*Hình 5.4.3. Environment properties của Elastic Beanstalk sau khi che thông tin nhạy cảm.*

Các biến quan trọng cần được kiểm tra gồm `DATABASE_URL`, `JWT_SECRET`, `MAIL_HOST`, `MAIL_USER`, `MAIL_PASSWORD`, `FRONTEND_ORIGIN` và `PORT=8080`. 

## Bước 5: Deploy và kiểm tra health

Sau khi deploy, kiểm tra endpoint trực tiếp của backend:

```text
http://<elastic-beanstalk-domain>/api/health
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

![Elastic Beanstalk environment ở trạng thái OK](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.4-eb-health-ok.png)

*Hình 5.4.4. Elastic Beanstalk environment ở trạng thái OK.*

Màn hình này cần hiển thị environment health ở trạng thái OK. Đây là dấu hiệu Elastic Beanstalk đã provision tài nguyên và backend không gặp lỗi startup nghiêm trọng.

![Health endpoint của backend trên Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.5-eb-health-endpoint.png)

*Hình 5.4.5. Health endpoint của backend trên Elastic Beanstalk trả kết quả thành công.*

Kết quả `/api/health` cần trả `success: true` và `status: ok`. Nếu endpoint này hoạt động, có thể tiếp tục đưa backend ra ngoài thông qua API Gateway.

Nếu health check lỗi, kiểm tra:

- Backend có listen đúng `PORT=8080`.
- `DATABASE_URL` đúng.
- Backend security group có thể kết nối RDS port `3306`.
- `JWT_SECRET` đủ dài và không rỗng.
- Biến môi trường mail/OTP/rate limit đã được cấu hình.
- Elastic Beanstalk logs không có startup error.

## Bước 6: Chạy Prisma migration và seed

Sau khi backend có thể kết nối RDS, chạy migration từ môi trường có quyền truy cập database. Trước khi chạy lệnh, cần kiểm tra file `.env` hoặc biến môi trường local đang trỏ đến đúng RDS endpoint, không phải `localhost:3306`.

```bash
cd backend
npx prisma generate
npx prisma migrate deploy
```

Nếu máy local không truy cập được RDS do security group, network hoặc VPN, không nên chạy migration trực tiếp từ local. Khi đó cần chạy lệnh từ một môi trường có quyền truy cập database, ví dụ EC2/bastion trong cùng VPC, môi trường CI/CD đã được cấp quyền, hoặc tạm thời cấu hình network phù hợp cho quá trình migration.

Với database demo, có thể seed dữ liệu mẫu sau khi migration chạy thành công:

```bash
npx prisma db seed
```

Nếu lệnh Prisma báo lỗi không kết nối được `localhost:3306`, nguyên nhân thường là `DATABASE_URL` vẫn đang dùng cấu hình local. Cần cập nhật lại `DATABASE_URL` theo dạng:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

## Kết quả của bước này

Ghi lại các giá trị:

- Tên Elastic Beanstalk application.
- Tên Elastic Beanstalk environment.
- Backend endpoint/domain.
- Backend security group.
- RDS endpoint.
- Kết quả health check `/api/health`.
