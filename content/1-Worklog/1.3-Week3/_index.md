---
title: "Week 3 Worklog"
date: 2026-05-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

## Week 3 Worklog

**Period:** 01/05/2026 - 07/05/2026

This week moved the frontend from static screens to API-connected flows. The main work covered login, token storage, current-user checks, and service layers for later admin modules.

### Week 3 Objectives:

- Connect the login form to the backend API.
- Handle tokens, protected routes, and frontend authentication state.
- Create service layers for the main API groups.

### Work planned and completed this week:

| Day | Work performed | Start date | End date | References |
| --- | --- | --- | --- | --- |
| Friday | - Connect the login form to the backend API and handle login responses.<br>- Learned about Amazon S3 and static website hosting.<br>&emsp; + Noted the main concepts for the report. | 01/05/2026 | 01/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Saturday | - Store login tokens and attach them to subsequent requests.<br>- Learned about Amazon RDS, DB instances, endpoints, backups, and engines.<br>&emsp; + Checked where it could be used in EAM Workspace. | 02/05/2026 | 02/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Sunday | - Create a current-user API flow and synchronize authentication state on the frontend.<br>- Learned about DynamoDB and NoSQL use cases.<br>&emsp; + Compared NoSQL storage with the relational data model used in the project. | 03/05/2026 | 03/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Monday | - Build protected routes based on authentication state and access rights.<br>- Learned about CloudWatch metrics, logs, and alarms.<br>&emsp; + Read the material and recorded steps useful for deployment. | 04/05/2026 | 04/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Tuesday | - Start creating separate frontend services for each API group.<br>- Learned about CloudFront and CDN for web applications.<br>&emsp; + Checked how a CDN can improve frontend loading speed. | 05/05/2026 | 05/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Wednesday | - Add loading and empty states for data lists.<br>- Learned about Route 53, DNS, hosted zones, and records.<br>&emsp; + Noted how domains can point to frontend or API endpoints. | 06/05/2026 | 06/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thursday | - Review login, token, and API call flows before building admin CRUD screens.<br>- Learned about AWS CLI and command-line service operations.<br>&emsp; + Practiced reading common CLI command formats for AWS services. | 07/05/2026 | 07/05/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Week 3 Achievements:

- The basic login flow could call the backend, store tokens, and reuse them in later requests.
- Protected routes limited access to authenticated screens.
- Loading and empty states were added so API-driven screens responded more clearly.

### Plan for Next Week

- Complete admin CRUD screens for categories, departments, employees, and assets.




