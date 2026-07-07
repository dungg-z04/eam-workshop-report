---
title: "Test, monitor, and troubleshoot"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Test, Monitor, and Troubleshoot

After the frontend, API Gateway, and backend are deployed, validate the whole system and check operational logs.

## Test 1: Backend Health

Check each layer:

```text
http://<elastic-beanstalk-domain>/api/health
https://<api-gateway-endpoint>/api/health
https://<amplify-domain>/api/health
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

If it fails, check in this order: Elastic Beanstalk logs, API Gateway route/integration/stage, then the Amplify rewrite rule.

## Test 2: Admin Login

Open the Amplify URL and sign in with the seeded admin account.

![Login page on the Amplify domain](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.1-login-page.png)

*Figure 5.6.1. Login page on the Amplify domain.*

The frontend should open from the Amplify domain and the login form should display correctly. This is the starting point for user workflow testing.

Expected results:

- User is redirected to `/admin/dashboard`.
- Dashboard metrics are displayed.
- Sidebar and navigation work.
- API calls return `200` or the expected business response.

![Admin dashboard after successful login](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.2-admin-dashboard.png)

*Figure 5.6.2. Admin dashboard after successful login.*

After admin login, the dashboard should display summary data. This confirms that authentication, backend APIs, and the database are working together.

## Test 3: Main Admin Workflows

Test at least one workflow from each major admin module:

| Module | Test Action |
| --- | --- |
| Categories | Create or search asset categories. |
| Assets | Create, update, or search assets. |
| Employees | View the employee list and employee details. |
| Departments | View or update department information. |
| Assignments | Assign an available asset to an employee. |
| Maintenance | Create or update a support/maintenance request. |
| Inventory | View or create an inventory session. |
| Reports | Open summary or asset reports. |

![Asset management screen](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.3-admin-assets.png)

*Figure 5.6.3. Asset management screen.*

On the asset management screen, check that the asset list loads correctly and that core actions such as view, edit, delete, or Excel import appear according to admin permissions.

![Asset assignment workflow](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.4-assignment-maintenance.png)

*Figure 5.6.4. Asset assignment workflow.*

In the assignment workflow, verify asset status, assigned employee, and assignment history. This is a key business workflow in EAM Workspace.

## Test 4: Employee Workflows

Sign in with an employee account and check:

- Employee dashboard.
- Assigned assets page.
- Asset detail page.
- Support request creation.
- FAQ page.
- Profile and history pages.

![Employee dashboard](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.5-employee-dashboard.png)

*Figure 5.6.5. Employee dashboard after sign-in.*

On the employee dashboard, verify that data is displayed according to employee permissions. The user should only see assigned assets, support requests, and personal information related to their account.

## Test 5: Upload and Account Status

Also test the cases encountered during deployment:

- Image/avatar upload goes through backend/API and the image returns `200`.
- Inactive accounts cannot sign in.
- Inactive account errors return the expected business code, for example `AUTH_ACCOUNT_INACTIVE`.
- Browser DevTools shows no CORS errors.

![DevTools Network showing successful API requests](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.6-devtools-network.png)

*Figure 5.6.6. DevTools Network showing successful API requests.*

In the Network tab, filter `/api/...` requests and check that the status is `200` or an expected business response. If CORS errors or HTML responses appear, recheck Amplify rewrites and backend CORS settings.

![Inactive account blocked from signing in](/eam-workshop-report/images/5-Workshop/5.6-Test-Monitor/5.6.7-inactive-account.png)

*Figure 5.6.7. Inactive account blocked from signing in.*

When signing in with an inactive account, the system should deny access. This confirms that the backend checks account status before granting system access.

## Monitoring with CloudWatch

Open CloudWatch Logs and check the Elastic Beanstalk log group.

Check:

- Backend startup logs.
- Request logs.
- Authentication errors.
- Database connection errors.
- Unhandled exceptions.

Useful endpoints:

```text
GET /api/health
POST /api/auth/login
GET /api/assets
GET /api/reports/summary
```

## Suggested Alarms

For a demo environment, simple CloudWatch alarms can be created:

| Alarm | Purpose |
| --- | --- |
| EC2 high CPU | Detect backend instance overload. |
| Elastic Beanstalk health degraded | Detect unstable backend environments. |
| RDS CPU or storage | Detect database capacity issues. |
| 5xx errors | Detect application or infrastructure errors. |

## Troubleshooting Guide

| Issue | Common Cause | Fix |
| --- | --- | --- |
| `502` or backend not responding | Backend crash or wrong port | Check `PORT=8080`, EB logs, and direct health endpoint. |
| API Gateway returns `404` | Wrong route, stage, or integration | Check `ANY /{proxy+}`, integration endpoint, deployed stage, and path forwarding. |
| CORS error | Wrong `FRONTEND_ORIGIN` or `FRONTEND_ORIGINS` | Set the correct Amplify URL and redeploy backend. |
| Cannot connect to database | Wrong RDS endpoint or security group | Check `DATABASE_URL` and allow `3306` from backend SG. |
| `/api/...` returns frontend HTML | Amplify rewrite order is wrong | Move `/api/<*>` above the SPA fallback rule. |
| Static JS/CSS MIME type error | Rewrite rule captures static assets incorrectly | Rewrite only `/api/<*>` to API Gateway and let SPA fallback handle frontend routes. |
| Login fails | Seed data or JWT config issue | Check seed data, `JWT_SECRET`, and backend logs. |
| Upload is not durable | Local instance storage is being used | Move upload storage to S3 for production-ready deployment. |

## Validation Checklist

- Frontend opens from the Amplify URL.
- `GET /api/health` succeeds through Elastic Beanstalk.
- `GET /api/health` succeeds through API Gateway.
- `GET /api/health` succeeds through Amplify rewrite.
- Admin login works.
- Employee login works.
- Main CRUD workflows work.
- Asset assignment workflow works.
- Support request workflow works.
- Inactive accounts are blocked from signing in.
- Browser DevTools shows no CORS errors.
