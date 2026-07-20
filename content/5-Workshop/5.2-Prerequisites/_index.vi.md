---
title: "Chuẩn bị"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Chuẩn bị

Trước khi triển khai, cần chuẩn bị AWS account, công cụ local, source code và các biến môi trường cần dùng cho backend/frontend.

## AWS account

Sử dụng một AWS Region cố định cho toàn bộ tài nguyên trong workshop. IAM user hoặc role cần có quyền tạo và quản lý:

- AWS Amplify Hosting
- Amazon API Gateway
- Amazon EC2 và Security Groups
- AWS Elastic Beanstalk
- Amazon RDS
- Amazon S3
- Amazon SES
- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- Amazon CloudWatch
- AWS CloudTrail

Sau khi chọn Region, kiểm tra lại góc phải trên của AWS Console để đảm bảo toàn bộ thao tác được thực hiện trong cùng một Region.

![Region AWS được sử dụng cho workshop](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.1-aws-region.png)

*Hình 5.2.1. Region AWS được sử dụng cho workshop.*

Region đang chọn phải là Region được dùng xuyên suốt workshop. Việc thống nhất Region giúp tránh lỗi kết nối giữa Elastic Beanstalk, API Gateway, RDS và SES.

## Kiểm tra branch triển khai

Trước khi kết nối AWS Amplify, cần xác định branch GitHub được dùng để triển khai frontend.

![GitHub branch dùng để triển khai frontend bằng Amplify](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.2-github-branch.png)

*Hình 5.2.2. GitHub branch dùng để triển khai frontend bằng Amplify.*

Cần ghi lại đúng branch deploy, ví dụ `aws-architecture`, vì Amplify sẽ lấy source code từ branch này để build và deploy frontend.

## Công cụ local

Cài đặt và kiểm tra các công cụ sau:

| Công cụ | Mục đích |
| --- | --- |
| Node.js 20+ | Chạy backend và frontend local. |
| npm | Cài dependency và chạy build script. |
| Git | Quản lý source code và kết nối GitHub. |
| MySQL client hoặc database tool | Tùy chọn, hữu ích khi kiểm tra database. |
| Postman hoặc browser DevTools | Kiểm thử API endpoint. |

Kiểm tra Node.js và npm:

```bash
node -v
npm -v
```

Kết quả cần hiển thị phiên bản Node.js và npm trên máy local.

![Kiểm tra Node.js và npm trên máy local](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.3-local-tools.png)

*Hình 5.2.3. Kiểm tra Node.js và npm trên máy local.*

Nếu hai lệnh trên trả về version hợp lệ, môi trường local đã sẵn sàng để cài dependency, build frontend và kiểm tra backend trước khi đóng gói triển khai lên AWS.

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

Chuẩn bị các giá trị sau trước khi tạo hoặc cập nhật Elastic Beanstalk environment:

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

## Chuẩn bị SES/SMTP

Backend sử dụng email để gửi OTP hoặc thông báo, vì vậy cần chuẩn bị thông tin SMTP trước khi cấu hình Elastic Beanstalk. Trong môi trường demo, có thể xác thực một email identity thay vì xác thực domain riêng.

Các bước chuẩn bị:

1. Mở **Amazon SES** trong cùng Region đang dùng cho workshop.
2. Vào **Verified identities** và tạo identity loại **Email address**.
3. Nhập email gửi, ví dụ email cá nhân hoặc email dùng cho demo.
4. Mở hộp thư và bấm link xác thực do Amazon SES gửi đến.
5. Sau khi email ở trạng thái **Verified**, tạo **SMTP credentials** trong SES.
6. Lưu lại SMTP username và SMTP password để điền vào Elastic Beanstalk.

Các biến môi trường tương ứng:

```env
MAIL_HOST=email-smtp.<region>.amazonaws.com
MAIL_PORT=587
MAIL_SECURE=false
MAIL_USER=<ses-smtp-username>
MAIL_PASSWORD=<ses-smtp-password>
MAIL_FROM=<verified-email-address>
```

Nếu SES vẫn ở sandbox mode, email chỉ gửi được đến các địa chỉ đã verified. Với workshop demo, điều này vẫn đủ để kiểm thử OTP hoặc email thông báo.

## Biến môi trường frontend

Khi deploy bằng Amplify, dùng API path tương đối:

```env
VITE_API_BASE_URL=/api
```

Cách này giúp browser gọi cùng origin của Amplify, còn Amplify sẽ rewrite `/api/*` đến endpoint Amazon API Gateway.

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

- Đã chọn AWS Region.
- AWS account có quyền phù hợp.
- Đã có source code backend và frontend.
- Đã chuẩn bị biến môi trường backend.
- Đã chuẩn bị `VITE_API_BASE_URL=/api` cho Amplify.
- Đã xác định endpoint RDS hoặc kế hoạch tạo RDS.
- Thống nhất dùng hướng demo không có Route 53 hoặc custom domain.

