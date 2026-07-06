---
title: "Connect API Gateway and Amplify Hosting"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Connect API Gateway and Amplify Hosting

This step creates an Amazon API Gateway HTTP API for the backend, then deploys the React frontend to AWS Amplify Hosting and configures the `/api/*` and `/uploads/*` rewrites.

## Step 1: Create an API Gateway HTTP API

Open the Amazon API Gateway console:

1. Choose **Create API**.
2. Choose **HTTP API**.
3. Set a name, for example `eam-backend-api`.
4. Create an integration that points to the Elastic Beanstalk backend endpoint.
5. Create a proxy route for requests forwarded by Amplify:

```text
ANY /{proxy+}
```

This route allows API Gateway to receive paths such as `/api/health`, `/api/auth/login`, `/uploads/...` and forward the original path to the backend.

6. Create a stage, for example `$default` or `prod`.
7. Deploy the API.

The API Gateway endpoint will look like:

```text
https://<api-id>.execute-api.<region>.amazonaws.com
```

![Amazon API Gateway HTTP API overview](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.1-api-gateway-overview.png)

*Figure 5.5.1. Amazon API Gateway HTTP API overview.*

The API should have the correct name and a public endpoint. This endpoint will be used by Amplify rewrite rules for `/api/*` and `/uploads/*`.

![API Gateway proxy route](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.2-api-gateway-route.png)

*Figure 5.5.2. API Gateway `ANY /{proxy+}` route.*

In the Routes section, confirm that `ANY /{proxy+}` exists. This route allows API Gateway to receive paths such as `/api/health`, `/api/assets`, and `/uploads/...`.

![API Gateway integration pointing to Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.3-api-gateway-integration.png)

*Figure 5.5.3. API Gateway integration pointing to the Elastic Beanstalk backend.*

In the Integration section, confirm that the URI points to the Elastic Beanstalk domain and preserves the `{proxy}` variable. If the path is not preserved, the backend may receive the wrong endpoint and return `404`.

## Step 2: Test API Gateway

Open the health endpoint through API Gateway:

```text
https://<api-gateway-endpoint>/api/health
```

If it returns 404, check:

- Route `ANY /{proxy+}`.
- Integration target points to the correct Elastic Beanstalk backend endpoint.
- Stage is deployed.
- Parameter mapping or path forwarding does not remove the `/api` prefix.
- The integration URI can use `http://<elastic-beanstalk-domain>/{proxy}` when the route has the `{proxy+}` path variable.

![Health endpoint through API Gateway](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.4-api-gateway-health.png)

*Figure 5.5.4. Health endpoint through API Gateway returning a successful response.*

When calling `/api/health` through API Gateway, the response should return `success: true` and `status: ok`. This confirms that the route, integration, and stage are working correctly.

## Step 3: Check the Frontend Build Locally

From the frontend folder:

```bash
cd frontend
npm ci
npm run build
```

Production build output:

```text
dist/
```

## Step 4: Check Amplify Build Settings

The repository can use an `amplify.yml` file for the monorepo structure:

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

![Amplify build settings](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.6-amplify-build-settings.png)

*Figure 5.5.6. Amplify build settings with app root and output directory.*

On the build settings screen, verify that `appRoot` is `frontend`, the build command is `npm ci && npm run build`, and the output directory is `dist`.

## Step 5: Create the Amplify App

Open the AWS Amplify console:

1. Choose **New app** or **Host web app**.
2. Connect the GitHub repository.
3. Select the deployment branch, for example `aws-architecture`.
4. Set the monorepo root to `frontend` if Amplify asks for it.
5. Check the build command:

```bash
npm ci && npm run build
```

6. Check the output directory:

```text
dist
```

![Amplify app connected to the aws-architecture branch](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.5-amplify-branch.png)

*Figure 5.5.5. Amplify app connected to the deployment branch.*

On the Amplify app screen, verify that the deployment branch is the branch that contains the latest frontend source. Amplify will automatically build and publish the frontend from this branch.

![Successful Amplify deployment](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.8-amplify-build-success.png)

*Figure 5.5.8. Successful Amplify deployment.*

When the deployment status is `Deployed`, the frontend has been built and published successfully on the Amplify domain. This is required before testing the UI and API rewrite.

## Step 6: Set the Frontend Environment Variable

In Amplify, set:

```env
VITE_API_BASE_URL=/api
```

This allows the browser to call APIs through the same Amplify domain:

```text
https://<amplify-domain>/api/...
```

## Step 7: Configure the Amplify Rewrite

After the app is created, open **Rewrites and redirects**.

Add this rule above the SPA fallback rule:

| Source address | Target address | Type |
| --- | --- | --- |
| `/api/<*>` | `https://<api-gateway-endpoint>/api/<*>` | `200 (Rewrite)` |
| `/uploads/<*>` | `https://<api-gateway-endpoint>/uploads/<*>` | `200 (Rewrite)` |

Then keep the SPA fallback rule for React Router:

| Source address | Target address | Type |
| --- | --- | --- |
| `/<*>` | `/index.html` | `404 (Rewrite)` or `404-200` |

If the `/api/<*>` or `/uploads/<*>` rule is in the wrong order, API and upload requests may return frontend HTML or static assets may fail with MIME type errors.

![Amplify rewrite rules](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.7-amplify-rewrite-rules.png)

*Figure 5.5.7. Amplify rewrite rules forwarding `/api/<*>` and `/uploads/<*>` to API Gateway.*

The `/api/<*>` and `/uploads/<*>` rules should stay above the `/index.html` fallback. This order ensures API and upload requests go to API Gateway instead of being handled as frontend routes.

## Step 8: Update Backend CORS Origin

After Amplify is deployed, copy the default Amplify URL:

```text
https://main.xxxxx.amplifyapp.com
```

Update backend environment variables:

```env
FRONTEND_ORIGIN=https://main.xxxxx.amplifyapp.com
FRONTEND_ORIGINS=https://main.xxxxx.amplifyapp.com
```

Redeploy or restart the Elastic Beanstalk environment after updating these values.

## Result of This Step

Record:

- API Gateway endpoint.
- Amplify app URL.
- `FRONTEND_ORIGIN` value.
- Frontend build status.
- Result of `https://<amplify-domain>/api/health`.

![Health endpoint through the Amplify domain](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.9-amplify-health.png)

*Figure 5.5.9. Health endpoint through the Amplify domain returning a successful response.*

For the final validation, call `https://<amplify-domain>/api/health`. The request passes through Amplify rewrite, API Gateway, and Elastic Beanstalk before returning a successful response.
