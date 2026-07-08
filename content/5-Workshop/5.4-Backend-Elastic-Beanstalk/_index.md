---
title: "Deploy backend with Elastic Beanstalk"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 5.4. </b> "
---

## Deploy Backend with Elastic Beanstalk

This step packages the Node.js/Express backend and deploys it to AWS Elastic Beanstalk. The backend will receive requests from API Gateway and connect to Amazon RDS for MySQL.

## Step 1: Check the Backend Locally

From the backend folder, install dependencies and verify that the backend can start:

```bash
cd backend
npm ci
npm start
```

Backend entry point:

```text
src/app/server.js
```

The application must read the port from the `PORT` environment variable. On Elastic Beanstalk, use:

```env
PORT=8080
```

## Step 2: Create the Backend Source Bundle

Create a ZIP file from the contents inside the `backend/` folder. The ZIP root must contain `package.json` directly.

Correct ZIP structure:

```text
backend-eb-source.zip
  package.json
  package-lock.json
  src/
  prisma/
```

Incorrect ZIP structure:

```text
backend-eb-source.zip
  backend/
    package.json
```

Do not include `.env`, `node_modules`, or real secrets in the ZIP file.

![Backend source bundle with the correct Elastic Beanstalk deployment structure](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.1-source-bundle.png)

*Figure 5.4.1. Backend source bundle with the correct Elastic Beanstalk deployment structure.*

The ZIP should contain `package.json`, `package-lock.json`, `src/`, and `prisma/` directly at the root. If the ZIP contains an extra outer `backend/` folder, Elastic Beanstalk may fail to start the application.

## Step 3: Create the Elastic Beanstalk Application

Open the Elastic Beanstalk console:

1. Choose **Create application**.
2. Application name: `eam-backend`.
3. Platform: **Node.js**.
4. Application code: upload the backend ZIP file.
5. Environment name: for example `eam-backend-prod`.
6. Select the appropriate VPC and subnet.
7. Attach the backend security group.
8. Create the environment and wait for provisioning to finish.

If an old environment is stuck in `Severe`, `No Data`, `CREATE_FAILED`, or `DELETE_FAILED`, creating a new environment and pointing it to the same RDS database can save time.

![Elastic Beanstalk environment creation page for the backend](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.2-create-eb-environment.png)

*Figure 5.4.2. Elastic Beanstalk environment creation page for the backend.*

On the environment creation screen, verify the application name, environment name, Node.js platform, and uploaded source bundle. This is the foundation for running the backend on Elastic Beanstalk.

## Step 4: Configure Environment Properties

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
FRONTEND_ORIGINS=https://<amplify-domain>
```

`FRONTEND_ORIGIN` and `FRONTEND_ORIGINS` can be updated after Amplify creates the frontend URL.

![Elastic Beanstalk environment properties](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.3-eb-env-properties.png)

*Figure 5.4.3. Elastic Beanstalk environment properties with sensitive values hidden.*

Important variables to verify include `DATABASE_URL`, `JWT_SECRET`, `MAIL_HOST`, `MAIL_USER`, `MAIL_PASSWORD`, `FRONTEND_ORIGIN`, and `PORT=8080`. Hide secrets before including the screenshot in the report.

## Step 5: Deploy and Check Health

After deployment, check the backend endpoint directly:

```text
http://<elastic-beanstalk-domain>/api/health
```

Expected response:

```json
{
  "success": true,
  "message": "OK",
  "data": {
    "status": "ok"
  }
}
```

![Elastic Beanstalk environment in OK status](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.4-eb-health-ok.png)

*Figure 5.4.4. Elastic Beanstalk environment in OK status.*

This screen should show the environment health as OK. It indicates that Elastic Beanstalk has provisioned the resources and the backend has no critical startup failure.

![Backend health endpoint on Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.4-Backend-Elastic-Beanstalk/5.4.5-eb-health-endpoint.png)

*Figure 5.4.5. Backend health endpoint on Elastic Beanstalk returning a successful response.*

The `/api/health` result should return `success: true` and `status: ok`. If this endpoint works, the backend is ready to be exposed through API Gateway.

If the health check fails, check:

- The backend listens on `PORT=8080`.
- `DATABASE_URL` is correct.
- The backend security group can connect to RDS port `3306`.
- `JWT_SECRET` is long enough and not empty.
- Mail/OTP/rate limit variables are configured.
- Elastic Beanstalk logs do not show startup errors.

## Step 6: Run Prisma Migration and Seed

After the backend can connect to RDS, run migration from an environment that can access the database. Before running the commands, check that the local `.env` file or environment variables point to the correct RDS endpoint, not `localhost:3306`.

```bash
cd backend
npx prisma generate
npx prisma migrate deploy
```

If the local machine cannot reach RDS because of security group, network, or VPN restrictions, do not run the migration directly from local. Instead, run it from an environment that can access the database, such as an EC2/bastion instance in the same VPC, an authorized CI/CD environment, or a temporarily configured network path for migration.

For a demo database, seed sample data after migration succeeds:

```bash
npx prisma db seed
```

If Prisma reports that it cannot connect to `localhost:3306`, the `DATABASE_URL` is usually still using the local database configuration. Update it to the RDS format:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

## Result of This Step

Record these values:

- Elastic Beanstalk application name.
- Elastic Beanstalk environment name.
- Backend endpoint/domain.
- Backend security group.
- RDS endpoint.
- `/api/health` health check result.
