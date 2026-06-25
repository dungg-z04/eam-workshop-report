---
title: "Triển khai backend bằng Elastic Beanstalk"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Triển khai backend bằng Elastic Beanstalk

Ở bước này, chúng ta sẽ đóng gói backend Node.js/Express và deploy lên AWS Elastic Beanstalk phía sau Application Load Balancer.

## Bước 1: Kiểm tra backend local

Từ thư mục backend, cài dependency và kiểm tra backend có thể start:

```bash
cd backend
npm ci
npm start
```

Entry point của backend là:

```text
src/app/server.js
```

Ứng dụng cần đọc port từ biến môi trường `PORT`.

## Bước 2: Tạo backend source bundle

Tạo file ZIP từ nội dung bên trong thư mục `backend/`. Root của file ZIP phải chứa trực tiếp `package.json`.

Cấu trúc ZIP đúng:

```text
backend-eb-source.zip
  package.json
  package-lock.json
  src/
  prisma/
  jest.config.cjs
  eslint.config.js
```

Cấu trúc ZIP sai:

```text
backend-eb-source.zip
  backend/
    package.json
```

{{% notice warning %}}
Không đưa `.env`, `node_modules` hoặc secret thật vào source bundle.
{{% /notice %}}

## Bước 3: Tạo Elastic Beanstalk application

Mở Elastic Beanstalk console:

1. Chọn **Create application**.
2. Application name: `eam-backend`.
3. Platform: **Node.js**.
4. Application code: upload file ZIP của backend.
5. Environment type: dùng load-balanced environment nếu muốn ALB được tạo và quản lý cùng Elastic Beanstalk.
6. Chọn VPC mục tiêu.
7. Chọn private subnet cho backend instance nếu network design hỗ trợ.
8. Gắn backend security group.

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
```

Giá trị `FRONTEND_ORIGIN` có thể cập nhật sau khi Amplify tạo URL frontend.

## Bước 5: Deploy và chờ health

Upload và deploy backend source bundle. Chờ environment health chuyển xanh.

Nếu environment unhealthy, kiểm tra:

- Backend có listen đúng `PORT=8080`.
- `DATABASE_URL` đúng.
- Backend security group có thể kết nối RDS port `3306`.
- Các biến môi trường mail và JWT đã đủ.
- Elastic Beanstalk logs không có startup error.

## Bước 6: Chạy Prisma migration

Sau khi backend có thể kết nối RDS, chạy migration từ máy có thể kết nối đến database:

```bash
cd backend
npx prisma generate
npx prisma migrate deploy
```

Với database demo, có thể seed dữ liệu mẫu:

```bash
npx prisma db seed
```

{{% notice warning %}}
Chỉ chạy seed trên database demo hoặc staging còn trống. Không seed production database nếu chưa kiểm tra kỹ.
{{% /notice %}}

## Bước 7: Kiểm tra backend health

Mở backend health endpoint:

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

## Kết quả của bước này

Ghi lại các giá trị:

- Tên Elastic Beanstalk environment
- DNS name của Application Load Balancer
- Backend security group
- RDS endpoint
- Kết quả health check của backend
