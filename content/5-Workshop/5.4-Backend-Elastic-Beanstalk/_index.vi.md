---
title: "Triá»ƒn khai backend báº±ng Elastic Beanstalk"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Triá»ƒn khai backend báº±ng Elastic Beanstalk

á»ž bÆ°á»›c nÃ y, chÃºng ta sáº½ Ä‘Ã³ng gÃ³i backend Node.js/Express vÃ  deploy lÃªn AWS Elastic Beanstalk phÃ­a sau Application Load Balancer.

## BÆ°á»›c 1: Kiá»ƒm tra backend local

Tá»« thÆ° má»¥c backend, cÃ i dependency vÃ  kiá»ƒm tra backend cÃ³ thá»ƒ start:

```bash
cd backend
npm ci
npm start
```

Entry point cá»§a backend lÃ :

```text
src/app/server.js
```

á»¨ng dá»¥ng cáº§n Ä‘á»c port tá»« biáº¿n mÃ´i trÆ°á»ng `PORT`.

## BÆ°á»›c 2: Táº¡o backend source bundle

Táº¡o file ZIP tá»« ná»™i dung bÃªn trong thÆ° má»¥c `backend/`. Root cá»§a file ZIP pháº£i chá»©a trá»±c tiáº¿p `package.json`.

Cáº¥u trÃºc ZIP Ä‘Ãºng:

```text
backend-eb-source.zip
  package.json
  package-lock.json
  src/
  prisma/
  jest.config.cjs
  eslint.config.js
```

Cáº¥u trÃºc ZIP sai:

```text
backend-eb-source.zip
  backend/
    package.json
```


## BÆ°á»›c 3: Táº¡o Elastic Beanstalk application

Má»Ÿ Elastic Beanstalk console:

1. Chá»n **Create application**.
2. Application name: `eam-backend`.
3. Platform: **Node.js**.
4. Application code: upload file ZIP cá»§a backend.
5. Environment type: dÃ¹ng load-balanced environment náº¿u muá»‘n ALB Ä‘Æ°á»£c táº¡o vÃ  quáº£n lÃ½ cÃ¹ng Elastic Beanstalk.
6. Chá»n VPC má»¥c tiÃªu.
7. Chá»n private subnet cho backend instance náº¿u network design há»— trá»£.
8. Gáº¯n backend security group.

## BÆ°á»›c 4: Cáº¥u hÃ¬nh environment properties

Trong Elastic Beanstalk environment properties, Ä‘áº·t:

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

GiÃ¡ trá»‹ `FRONTEND_ORIGIN` cÃ³ thá»ƒ cáº­p nháº­t sau khi Amplify táº¡o URL frontend.

## BÆ°á»›c 5: Deploy vÃ  chá» health

Upload vÃ  deploy backend source bundle. Chá» environment health chuyá»ƒn xanh.

Náº¿u environment unhealthy, kiá»ƒm tra:

- Backend cÃ³ listen Ä‘Ãºng `PORT=8080`.
- `DATABASE_URL` Ä‘Ãºng.
- Backend security group cÃ³ thá»ƒ káº¿t ná»‘i RDS port `3306`.
- CÃ¡c biáº¿n mÃ´i trÆ°á»ng mail vÃ  JWT Ä‘Ã£ Ä‘á»§.
- Elastic Beanstalk logs khÃ´ng cÃ³ startup error.

## BÆ°á»›c 6: Cháº¡y Prisma migration

Sau khi backend cÃ³ thá»ƒ káº¿t ná»‘i RDS, cháº¡y migration tá»« mÃ¡y cÃ³ thá»ƒ káº¿t ná»‘i Ä‘áº¿n database:

```bash
cd backend
npx prisma generate
npx prisma migrate deploy
```

Vá»›i database demo, cÃ³ thá»ƒ seed dá»¯ liá»‡u máº«u:

```bash
npx prisma db seed
```


## BÆ°á»›c 7: Kiá»ƒm tra backend health

Má»Ÿ backend health endpoint:

```text
http://<alb-dns-name>/api/health
```

Káº¿t quáº£ mong Ä‘á»£i:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

## Káº¿t quáº£ cá»§a bÆ°á»›c nÃ y

Ghi láº¡i cÃ¡c giÃ¡ trá»‹:

- TÃªn Elastic Beanstalk environment
- DNS name cá»§a Application Load Balancer
- Backend security group
- RDS endpoint
- Káº¿t quáº£ health check cá»§a backend
