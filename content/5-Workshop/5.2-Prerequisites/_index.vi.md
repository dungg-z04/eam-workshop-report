---
title: "Chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Chuẩn bị

Trước khi triển khai, cần chuẩn bị AWS account, công cụ local, source code và các biến môi trường.

## AWS account

Sử dụng một AWS Region cố định cho toàn bộ tài nguyên trong workshop. IAM user hoặc role cần có quyền tạo và quản lý:

- AWS Amplify
- Amazon EC2 và Security Groups
- Elastic Load Balancing
- AWS Elastic Beanstalk
- Amazon RDS
- Amazon S3
- Amazon SES
- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- Amazon CloudWatch
- AWS CloudTrail

{{% notice warning %}}
Không nên dùng root account cho công việc triển khai hằng ngày. Hãy dùng IAM user hoặc IAM role với đúng các quyền cần thiết cho workshop.
{{% /notice %}}

## Công cụ local

Cài đặt và kiểm tra các công cụ sau:

| Công cụ | Mục đích |
| --- | --- |
| Node.js 20+ | Chạy backend và frontend local. |
| npm | Cài dependency và chạy build script. |
| Git | Quản lý source code và kết nối GitHub. |
| Hugo Extended | Build website workshop. |
| MySQL client hoặc database tool | Tùy chọn, hữu ích khi kiểm tra database. |
| Postman hoặc browser DevTools | Kiểm thử API endpoint. |

Kiểm tra Node.js và npm:

```bash
node -v
npm -v
```

Kiểm tra Hugo:

```bash
hugo version
```

## Cấu trúc source code

Project có hai thư mục ứng dụng:

```text
quanlidoanhnghiep/
  backend/
  frontend/
```

Entry runtime của backend:

```text
backend/src/app/server.js
```

Output build của frontend:

```text
frontend/dist
```

## Biến môi trường backend

Chuẩn bị các giá trị sau trước khi tạo Elastic Beanstalk environment:

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

## Biến môi trường frontend

Khi deploy bằng Amplify, dùng API path tương đối:

```env
VITE_API_BASE_URL=/api
```

Cách này giúp browser gọi cùng origin của Amplify, còn Amplify sẽ rewrite `/api/<*>` đến backend load balancer.

## Checklist đóng gói backend

Khi đóng gói backend để deploy lên Elastic Beanstalk, file ZIP nên chứa các file và thư mục sau ngay ở root của ZIP:

- `package.json`
- `package-lock.json`
- `src/`
- `prisma/`
- các file cấu hình runtime cần thiết cho backend

Không nên đưa vào:

- `node_modules/`
- `.env`
- secret thật
- file upload local không cần thiết

## Checklist sẵn sàng

- [ ] Đã chọn AWS Region.
- [ ] AWS account có quyền phù hợp.
- [ ] Đã có source code backend và frontend.
- [ ] Đã chuẩn bị biến môi trường backend.
- [ ] Đã chuẩn bị `VITE_API_BASE_URL=/api` cho Amplify.
- [ ] Thống nhất dùng hướng demo không có Route 53 hoặc custom domain.
