---
title: "Deploy frontend with Amplify Hosting"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Deploy frontend with Amplify Hosting

In this step, you will deploy the React frontend to AWS Amplify Hosting and connect it to the backend through an Amplify rewrite rule.

## Step 1: Check frontend build locally

From the frontend folder:

```bash
cd frontend
npm ci
npm run build
```

The production build output should be:

```text
dist/
```

## Step 2: Confirm Amplify build settings

The repository contains an `amplify.yml` file for a monorepo structure:

```yaml
version: 1
applications:
  - appRoot: frontend
    frontend:
      phases:
        preBuild:
          commands:
            - npm ci
        build:
          commands:
            - npm run build
      artifacts:
        baseDirectory: dist
        files:
          - '**/*'
```

## Step 3: Create Amplify app

Open the AWS Amplify console:

1. Choose **New app** or **Host web app**.
2. Connect the GitHub repository.
3. Select the target branch, usually `main`.
4. Set app root to `frontend` if Amplify asks for the monorepo app root.
5. Confirm build command:

```bash
npm ci && npm run build
```

6. Confirm output directory:

```text
dist
```

## Step 4: Set frontend environment variable

Set this environment variable in Amplify:

```env
VITE_API_BASE_URL=/api
```

This makes the browser call API endpoints through the same Amplify domain:

```text
https://<amplify-domain>/api/...
```

## Step 5: Configure API rewrite

After the app is created, open **Rewrites and redirects**.

Add this rule above the SPA fallback rule:

| Source address | Target address | Type |
| --- | --- | --- |
| `/api/<*>` | `http://<alb-dns-name>/api/<*>` | `200 (Rewrite)` |

Then keep a SPA fallback rule for React Router:

| Source address | Target address | Type |
| --- | --- | --- |
| `/<*>` | `/index.html` | `404 (Rewrite)` or `404-200` |

{{% notice warning %}}
The `/api/<*>` rule must be above the SPA fallback rule. Otherwise API requests may be treated as frontend routes.
{{% /notice %}}

## Step 6: Update backend CORS origin

After Amplify deployment finishes, copy the Amplify default URL, for example:

```text
https://main.xxxxx.amplifyapp.com
```

Update the backend environment variable:

```env
FRONTEND_ORIGIN=https://main.xxxxx.amplifyapp.com
```

Redeploy or restart the Elastic Beanstalk environment after updating this value.

## Step 7: Open the application

Open the Amplify URL in a browser and check:

- The login page loads.
- Static assets load correctly.
- Refreshing `/login`, `/admin/dashboard`, or `/employee/dashboard` does not cause a 404.
- Browser DevTools shows API requests going to `/api/...` on the Amplify domain.

## Output of this step

Record:

- Amplify app URL
- ALB DNS name used in rewrite rule
- `FRONTEND_ORIGIN` value
- Frontend build status
