---
title: "Worklog Week 12"
date: 2026-07-03
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

## Worklog Week 12

**Time:** 03/07/2026 - 10/07/2026

Week 12 focused on final testing, AWS resource review, cleanup, and project wrap-up.

### Week 12 goals:

- Recheck the main EAM Workspace flows after production deployment.
- Review created AWS resources, monitor cost, and identify resources that need cleanup.
- Record technical issues, test results, and items to resolve during the week.

### Tasks completed this week:

| Day | Work performed | Start date | End date | References |
| --- | --- | --- | --- | --- |
| Friday | - Retested login, the admin dashboard, asset lists, and the employee portal in production.<br>- Checked the API health endpoint through API Gateway to confirm that the backend still responded correctly. | 03/07/2026 | 03/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Saturday | - Reviewed Amplify rewrite rules for `/api/*`, `/uploads/*`, and SPA fallback.<br>- Rechecked frontend environment variables to avoid calling the wrong backend endpoint. | 04/07/2026 | 04/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Sunday | - Monitored Elastic Beanstalk status, API responses, and possible errors when the app ran publicly.<br>- Rechecked SES/SMTP configuration to ensure the email flow did not use incorrect credentials. | 05/07/2026 | 05/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Monday | - Reviewed RDS, security groups, and `DATABASE_URL` to ensure the backend connected to the correct database environment.<br>- Checked demo data and main business flows after seeding the database. | 06/07/2026 | 06/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Tuesday | - Monitored Billing and Cost Management for costs from RDS, Elastic Beanstalk, API Gateway, and Amplify.<br>- Identified resources that should be stopped or removed after the demo was complete. | 07/07/2026 | 07/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Wednesday | - Reviewed created AWS resources, including the Elastic Beanstalk environment, API Gateway, RDS, SES identity, and Amplify app.<br>- Checked the cleanup order to avoid removing resources that still needed final verification. | 08/07/2026 | 08/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Thursday | - Reviewed completed work from week 12 and identified remaining issues.<br>- Finalized the important production configuration points for the project summary. | 09/07/2026 | 09/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |
| Friday | - Summarized the internship period, checked the repository, and confirmed that the project content was ready for handover. | 10/07/2026 | 10/07/2026 | Project source code, team discussion, <https://cloudjourney.awsstudygroup.com/> |

### Week 12 results:

- Completed final testing for the main EAM Workspace flows in production.
- Identified AWS resources that required cleanup and cost-related points to monitor.
- Added technical notes for testing and upcoming deployment work.
