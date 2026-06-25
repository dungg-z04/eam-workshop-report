---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Prerequisites

Before starting the deployment, prepare the AWS account, local tools, source code, and environment variables.

## AWS account

Use one AWS Region for all resources in this workshop. The IAM user or role should be allowed to create and manage:

- AWS Amplify
- Amazon EC2 and Security Groups
- Elastic Load Balancing
- AWS Elastic Beanstalk
- Amazon RDS
- Amazon S3
- Amazon SES
- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- Amazon CloudWatch
- AWS CloudTrail


## Local tools

Install and verify these tools:

| Tool | Purpose |
| --- | --- |
| Node.js 20+ | Run backend and frontend locally. |
| npm | Install dependencies and run build scripts. |
| Git | Manage source code and connect to GitHub. |
| Hugo Extended | Build the workshop website. |
| MySQL client or database tool | Optional, useful for checking the database. |
| Postman or browser DevTools | Test API endpoints. |

Check Node.js and npm:

```bash
node -v
npm -v
```

Check Hugo:

```bash
hugo version
```

## Source code structure

The project contains two application folders:

```text
quanlidoanhnghiep/
  backend/
  frontend/
```

Backend runtime entry:

```text
backend/src/app/server.js
```

Frontend build output:

```text
frontend/dist
```

## Backend environment variables

Prepare these values before creating the Elastic Beanstalk environment:

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

## Frontend environment variable

For Amplify deployment, use a relative API path:

```env
VITE_API_BASE_URL=/api
```

This allows the browser to call the same Amplify origin, while Amplify rewrites `/api/<*>` to the backend load balancer.

## Backend package checklist

When packaging the backend for Elastic Beanstalk, the ZIP file should contain these files and folders at the root of the ZIP:

- `package.json`
- `package-lock.json`
- `src/`
- `prisma/`
- runtime configuration files required by the backend

Do not include:

- `node_modules/`
- `.env`
- real secrets
- unnecessary local uploads

## Readiness checklist

- [ ] AWS Region is selected.
- [ ] AWS account has required permissions.
- [ ] Backend and frontend source code are available.
- [ ] Backend environment variables are prepared.
- [ ] `VITE_API_BASE_URL=/api` is ready for Amplify.
- [ ] The deployment will use the demo path without Route 53 or custom domain.
