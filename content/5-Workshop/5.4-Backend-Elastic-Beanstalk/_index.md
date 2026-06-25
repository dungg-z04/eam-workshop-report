---
title: "Deploy backend with Elastic Beanstalk"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Deploy backend with Elastic Beanstalk

In this step, you will package the Node.js/Express backend and deploy it to AWS Elastic Beanstalk behind an Application Load Balancer.

## Step 1: Check backend locally

From the backend folder, install dependencies and verify that the backend can start:

```bash
cd backend
npm ci
npm start
```

The backend entry point is:

```text
src/app/server.js
```

The application should read the port from the `PORT` environment variable.

## Step 2: Create a backend source bundle

Create a ZIP file from the contents inside the `backend/` folder. The ZIP root must contain `package.json` directly.

Correct ZIP structure:

```text
backend-eb-source.zip
  package.json
  package-lock.json
  src/
  prisma/
  jest.config.cjs
  eslint.config.js
```

Incorrect ZIP structure:

```text
backend-eb-source.zip
  backend/
    package.json
```


## Step 3: Create Elastic Beanstalk application

Open the Elastic Beanstalk console:

1. Choose **Create application**.
2. Application name: `eam-backend`.
3. Platform: **Node.js**.
4. Application code: upload the backend ZIP file.
5. Environment type: use a load-balanced environment if you want the ALB to be created and managed with Elastic Beanstalk.
6. Select the target VPC.
7. Select private subnets for backend instances if your network design supports it.
8. Attach the backend security group.

## Step 4: Configure environment properties

In Elastic Beanstalk environment properties, set:

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

The `FRONTEND_ORIGIN` value can be updated after Amplify creates the frontend URL.

## Step 5: Deploy and wait for health

Upload and deploy the backend source bundle. Wait until the environment health is green.

If the environment is unhealthy, check:

- The backend is listening on `PORT=8080`.
- `DATABASE_URL` is correct.
- The backend security group can reach RDS on port `3306`.
- Required mail and JWT environment variables are present.
- Elastic Beanstalk logs show no startup error.

## Step 6: Run Prisma migration

After the backend can reach RDS, run migrations from a machine that can connect to the database:

```bash
cd backend
npx prisma generate
npx prisma migrate deploy
```

For a demo database, you may seed sample data:

```bash
npx prisma db seed
```


## Step 7: Test backend health

Open the backend health endpoint:

```text
http://<alb-dns-name>/api/health
```

Expected result:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

## Output of this step

Record these values:

- Elastic Beanstalk environment name
- Application Load Balancer DNS name
- Backend security group
- RDS endpoint
- Backend health check result
