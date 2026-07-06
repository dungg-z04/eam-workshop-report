---
title: "Week 10 Worklog"
date: 2026-06-19
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

## Week 10 Worklog

**Period:** 19/06/2026 - 25/06/2026

This week shifted from feature development to AWS deployment. Backend, database, API Gateway, and frontend hosting were connected into a real public demo flow.

### Week 10 Objectives:

- Deploy the backend to Elastic Beanstalk and connect it to RDS MySQL.
- Configure API Gateway as the backend entry point.
- Deploy the frontend with Amplify and configure API/upload rewrites.

### Work planned and completed this week:

| Day | Work performed | Start date | End date | References |
| --- | --- | --- | --- | --- |
| Friday | - Prepare RDS MySQL, security groups, and `DATABASE_URL` for the production backend. | 19/06/2026 | 19/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Saturday | - Create the backend source bundle and verify the ZIP structure for Elastic Beanstalk Linux. | 20/06/2026 | 20/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Sunday | - Create/configure the Elastic Beanstalk environment and update environment properties. | 21/06/2026 | 21/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Monday | - Configure SES/SMTP, OTP, JWT, rate limit, and CORS origins for the backend. | 22/06/2026 | 22/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Tuesday | - Test the health endpoint directly through Elastic Beanstalk and resolve startup issues if needed. | 23/06/2026 | 23/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Wednesday | - Create the API Gateway HTTP API, proxy route, Elastic Beanstalk integration, and deployment stage. | 24/06/2026 | 24/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thursday | - Deploy the frontend with Amplify and configure build settings, `/api/*`, `/uploads/*` rewrites, and SPA fallback. | 25/06/2026 | 25/06/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Week 10 Achievements:

- The backend was packaged, configured with environment properties, and validated through the health endpoint.
- API Gateway forwarded requests to Elastic Beanstalk through a proxy route and integration.
- Amplify was configured with build settings, `/api/*`, `/uploads/*`, and SPA fallback rules for the production demo.

### Plan for Next Week

- Run production testing, fix upload/inactive-account issues, and complete workshop documentation.




