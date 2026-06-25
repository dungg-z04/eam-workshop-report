---
title: "Test, monitor, and troubleshoot"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

## Test, monitor, and troubleshoot

After the frontend and backend are deployed, validate the full system and check operational logs.

## Test 1: Backend health

Open:

```text
https://<amplify-domain>/api/health
```

or:

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

If this fails, check the ALB target health and Elastic Beanstalk logs.

## Test 2: Admin login

Open the Amplify URL and log in with an admin account from seed data.

Expected result:

- User is redirected to `/admin/dashboard`.
- Dashboard metrics are displayed.
- Sidebar and navigation work.
- API calls return `200` or expected business responses.

## Test 3: Core admin workflow

Validate at least one workflow from each major admin module:

| Module | Test action |
| --- | --- |
| Categories | Create or search an asset category. |
| Assets | Create, update, or search an asset. |
| Employees | View employee list and employee detail. |
| Departments | View or update department information. |
| Assignments | Assign an available asset to an employee. |
| Maintenance | Create or update a support/maintenance request. |
| Inventory | View or create an inventory session. |
| Reports | Open summary or asset reports. |

## Test 4: Employee workflow

Log in with an employee account and check:

- Employee dashboard.
- My assets page.
- Asset detail page.
- Support request creation.
- FAQ page.
- Profile and history pages.

## Test 5: Browser DevTools

Open DevTools and check the Network tab:

- API requests should use the Amplify domain.
- API paths should start with `/api`.
- No CORS error should appear.
- Failed requests should include a clear status code.

## Monitoring with CloudWatch

Open CloudWatch Logs and check the Elastic Beanstalk log groups.

Look for:

- Backend startup logs.
- Request logs.
- Authentication errors.
- Database connection errors.
- Unhandled exceptions.

Useful checks:

```text
GET /api/health
POST /api/auth/login
GET /api/assets
GET /api/reports/summary
```

## Recommended alarms

For a demo environment, create simple CloudWatch alarms:

| Alarm | Purpose |
| --- | --- |
| EC2 high CPU | Detect overloaded backend instance. |
| ALB unhealthy targets | Detect backend health issues. |
| RDS CPU or storage | Detect database capacity issues. |
| 5xx errors | Detect application or infrastructure errors. |

## Troubleshooting guide

| Problem | Likely cause | Fix |
| --- | --- | --- |
| `502 Bad Gateway` | Backend crashed or wrong port | Check `PORT=8080`, EB logs, and target group health. |
| CORS error | `FRONTEND_ORIGIN` is wrong | Set it to the exact Amplify URL and redeploy backend. |
| Cannot connect to database | RDS endpoint or security group is wrong | Check `DATABASE_URL` and allow `3306` from backend SG. |
| `/api/...` returns frontend HTML | Amplify rewrite order is wrong | Move `/api/<*>` above the SPA fallback rule. |
| Login fails | Seed data or JWT config issue | Check seed data, `JWT_SECRET`, and backend logs. |
| Upload does not persist | Local instance storage is used | Move upload storage to S3 for production-ready deployment. |

## Validation checklist

- [ ] Frontend opens from Amplify URL.
- [ ] `GET /api/health` returns success.
- [ ] Admin login works.
- [ ] Employee login works.
- [ ] Core CRUD workflow works.
- [ ] Asset assignment workflow works.
- [ ] Support request workflow works.
- [ ] CloudWatch Logs show backend activity.
- [ ] No CORS errors in browser DevTools.
