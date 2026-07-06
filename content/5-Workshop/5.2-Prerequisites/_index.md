---
title: "Prerequisites"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

## Prerequisites

Before deployment, prepare the AWS account, local tools, source code, and environment variables required by the backend and frontend.

## AWS Account

Use one AWS Region for all workshop resources. The IAM user or role should be able to create and manage:

- AWS Amplify Hosting
- Amazon API Gateway
- Amazon EC2 and Security Groups
- AWS Elastic Beanstalk
- Amazon RDS
- Amazon S3
- Amazon SES
- AWS Secrets Manager
- AWS Systems Manager Parameter Store
- Amazon CloudWatch
- AWS CloudTrail

After selecting the Region, check the top-right corner of the AWS Console to ensure all actions are performed in the same Region.

![AWS Region used for the workshop](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.1-aws-region.png)

*Figure 5.2.1. AWS Region used for the workshop.*

The selected Region should be the Region used throughout the workshop. Keeping one Region helps avoid connectivity issues between Elastic Beanstalk, API Gateway, RDS, and SES.

## Local Tools

Install and verify the following tools:

| Tool | Purpose |
| --- | --- |
| Node.js 20+ | Run the backend and frontend locally. |
| npm | Install dependencies and run build scripts. |
| Git | Manage source code and connect to GitHub. |
| MySQL client or database tool | Optional, useful for checking the database. |
| Postman or browser DevTools | Test API endpoints. |

Check Node.js and npm:

```bash
node -v
npm -v
```

The result should show the installed Node.js and npm versions on the local machine.

![Checking Node.js and npm on the local machine](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.3-local-tools.png)

*Figure 5.2.3. Checking Node.js and npm on the local machine.*

If both commands return valid versions, the local environment is ready for installing dependencies, building the frontend, and checking the backend before AWS deployment.

## Source Code Structure

The project has two application folders:

```text
quanlidoanhnghiep/
  backend/
  frontend/
```

Backend runtime entry:

```text
backend/src/app/server.js
```

Frontend production output:

```text
frontend/dist
```

## Check the Deployment Branch

Before connecting AWS Amplify, identify the GitHub branch used for frontend deployment.

![GitHub branch used for Amplify frontend deployment](/eam-workshop-report/images/5-Workshop/5.2-Prerequisites/5.2.2-github-branch.png)

*Figure 5.2.2. GitHub branch used for Amplify frontend deployment.*

Record the correct deployment branch, for example `aws-architecture`, because Amplify will build and deploy the frontend from this branch.

## Backend Environment Variables

Prepare these values before creating or updating the Elastic Beanstalk environment:

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

## Prepare SES/SMTP

The backend uses email for OTP or notification messages, so SMTP information should be prepared before configuring Elastic Beanstalk. For the demo environment, an email identity can be verified instead of a custom sending domain.

Preparation steps:

1. Open **Amazon SES** in the same Region used for the workshop.
2. Go to **Verified identities** and create an **Email address** identity.
3. Enter the sender email address used for the demo.
4. Open the mailbox and confirm the verification link sent by Amazon SES.
5. After the email address becomes **Verified**, create **SMTP credentials** in SES.
6. Store the SMTP username and SMTP password for the Elastic Beanstalk environment variables.

Related environment variables:

```env
MAIL_HOST=email-smtp.<region>.amazonaws.com
MAIL_PORT=587
MAIL_SECURE=false
MAIL_USER=<ses-smtp-username>
MAIL_PASSWORD=<ses-smtp-password>
MAIL_FROM=<verified-email-address>
```

If SES is still in sandbox mode, emails can only be sent to verified recipient addresses. This is still enough for a demo workshop to test OTP or notification email behavior.

## Frontend Environment Variable

When deploying with Amplify, use a relative API path:

```env
VITE_API_BASE_URL=/api
```

This allows the browser to call the same Amplify origin, while Amplify rewrites `/api/*` to the Amazon API Gateway endpoint.

## Backend Packaging Checklist

When packaging the backend for Elastic Beanstalk, the ZIP file should contain these files and folders at the root:

- `package.json`
- `package-lock.json`
- `src/`
- `prisma/`
- runtime configuration files required by the backend

Do not include:

- `node_modules/`
- `.env`
- real secrets
- unnecessary local upload files

## Readiness Checklist

- [ ] AWS Region selected.
- [ ] AWS account has the required permissions.
- [ ] Backend and frontend source code are available.
- [ ] Backend environment variables are prepared.
- [ ] `VITE_API_BASE_URL=/api` is prepared for Amplify.
- [ ] RDS endpoint or RDS creation plan is ready.
- [ ] Demo path without Route 53 or custom domain is confirmed.
