---
title: "Chuáº©n bá»‹"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Chuáº©n bá»‹

TrÆ°á»›c khi triá»ƒn khai, cáº§n chuáº©n bá»‹ AWS account, cÃ´ng cá»¥ local, source code vÃ  cÃ¡c biáº¿n mÃ´i trÆ°á»ng.

## AWS account

Sá»­ dá»¥ng má»™t AWS Region cá»‘ Ä‘á»‹nh cho toÃ n bá»™ tÃ i nguyÃªn trong workshop. IAM user hoáº·c role cáº§n cÃ³ quyá»n táº¡o vÃ  quáº£n lÃ½:

- AWS Amplify
- Amazon EC2 vÃ  Security Groups
- Elastic Load Balancing
- AWS Elastic Beanstalk
- Amazon RDS
- Amazon S3
- Amazon SES
- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- Amazon CloudWatch
- AWS CloudTrail


## CÃ´ng cá»¥ local

CÃ i Ä‘áº·t vÃ  kiá»ƒm tra cÃ¡c cÃ´ng cá»¥ sau:

| CÃ´ng cá»¥ | Má»¥c Ä‘Ã­ch |
| --- | --- |
| Node.js 20+ | Cháº¡y backend vÃ  frontend local. |
| npm | CÃ i dependency vÃ  cháº¡y build script. |
| Git | Quáº£n lÃ½ source code vÃ  káº¿t ná»‘i GitHub. |
| Hugo Extended | Build website workshop. |
| MySQL client hoáº·c database tool | TÃ¹y chá»n, há»¯u Ã­ch khi kiá»ƒm tra database. |
| Postman hoáº·c browser DevTools | Kiá»ƒm thá»­ API endpoint. |

Kiá»ƒm tra Node.js vÃ  npm:

```bash
node -v
npm -v
```

Kiá»ƒm tra Hugo:

```bash
hugo version
```

## Cáº¥u trÃºc source code

Project cÃ³ hai thÆ° má»¥c á»©ng dá»¥ng:

```text
quanlidoanhnghiep/
  backend/
  frontend/
```

Entry runtime cá»§a backend:

```text
backend/src/app/server.js
```

Output build cá»§a frontend:

```text
frontend/dist
```

## Biáº¿n mÃ´i trÆ°á»ng backend

Chuáº©n bá»‹ cÃ¡c giÃ¡ trá»‹ sau trÆ°á»›c khi táº¡o Elastic Beanstalk environment:

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

## Biáº¿n mÃ´i trÆ°á»ng frontend

Khi deploy báº±ng Amplify, dÃ¹ng API path tÆ°Æ¡ng Ä‘á»‘i:

```env
VITE_API_BASE_URL=/api
```

CÃ¡ch nÃ y giÃºp browser gá»i cÃ¹ng origin cá»§a Amplify, cÃ²n Amplify sáº½ rewrite `/api/<*>` Ä‘áº¿n backend load balancer.

## Checklist Ä‘Ã³ng gÃ³i backend

Khi Ä‘Ã³ng gÃ³i backend Ä‘á»ƒ deploy lÃªn Elastic Beanstalk, file ZIP nÃªn chá»©a cÃ¡c file vÃ  thÆ° má»¥c sau ngay á»Ÿ root cá»§a ZIP:

- `package.json`
- `package-lock.json`
- `src/`
- `prisma/`
- cÃ¡c file cáº¥u hÃ¬nh runtime cáº§n thiáº¿t cho backend

KhÃ´ng nÃªn Ä‘Æ°a vÃ o:

- `node_modules/`
- `.env`
- secret tháº­t
- file upload local khÃ´ng cáº§n thiáº¿t

## Checklist sáºµn sÃ ng

- [ ] ÄÃ£ chá»n AWS Region.
- [ ] AWS account cÃ³ quyá»n phÃ¹ há»£p.
- [ ] ÄÃ£ cÃ³ source code backend vÃ  frontend.
- [ ] ÄÃ£ chuáº©n bá»‹ biáº¿n mÃ´i trÆ°á»ng backend.
- [ ] ÄÃ£ chuáº©n bá»‹ `VITE_API_BASE_URL=/api` cho Amplify.
- [ ] Thá»‘ng nháº¥t dÃ¹ng hÆ°á»›ng demo khÃ´ng cÃ³ Route 53 hoáº·c custom domain.
