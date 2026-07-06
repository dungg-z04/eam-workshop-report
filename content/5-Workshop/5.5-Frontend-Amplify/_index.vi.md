---
title: "Kết nối API Gateway và Amplify Hosting"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Kết nối API Gateway và Amplify Hosting

Bước này tạo Amazon API Gateway HTTP API cho backend, sau đó deploy frontend React lên AWS Amplify Hosting và cấu hình rewrite `/api/*`.

## Bước 1: Tạo API Gateway HTTP API

Mở Amazon API Gateway console:

1. Chọn **Create API**.
2. Chọn **HTTP API**.
3. Đặt tên, ví dụ `eam-backend-api`.
4. Tạo integration trỏ đến backend Elastic Beanstalk endpoint.
5. Tạo route proxy để nhận request được Amplify chuyển đến:

```text
ANY /{proxy+}
```

Route này cho phép API Gateway nhận các path như `/api/health`, `/api/auth/login`, `/uploads/...` và chuyển tiếp nguyên path đến backend.

6. Tạo stage, ví dụ `$default` hoặc `prod`.
7. Deploy API.

Endpoint API Gateway sẽ có dạng:

```text
https://<api-id>.execute-api.<region>.amazonaws.com
```

![Tổng quan HTTP API trong Amazon API Gateway](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.1-api-gateway-overview.png)

*Hình 5.5.1. Tổng quan HTTP API trong Amazon API Gateway.*

API cần được tạo đúng tên và có endpoint public. Endpoint này sẽ được dùng trong Amplify rewrite để chuyển tiếp các request `/api/*` và `/uploads/*`.

![Route proxy của API Gateway](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.2-api-gateway-route.png)

*Hình 5.5.2. Route `ANY /{proxy+}` của API Gateway.*

Tại phần Routes, cần đảm bảo route `ANY /{proxy+}` đã được tạo. Route này giúp API Gateway nhận mọi path cần chuyển đến backend, bao gồm `/api/health`, `/api/assets` và `/uploads/...`.

![Integration của API Gateway trỏ đến Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.3-api-gateway-integration.png)

*Hình 5.5.3. Integration của API Gateway trỏ đến Elastic Beanstalk backend.*

Tại phần Integration, cần kiểm tra URI đang trỏ đến domain Elastic Beanstalk và có giữ biến `{proxy}`. Nếu integration không giữ path, backend có thể nhận sai endpoint và trả lỗi `404`.

## Bước 2: Kiểm tra API Gateway

Mở health endpoint qua API Gateway:

```text
https://<api-gateway-endpoint>/api/health
```

Nếu trả 404, kiểm tra lại:

- Route `ANY /{proxy+}`.
- Integration target đến đúng backend Elastic Beanstalk endpoint.
- Stage đã deploy.
- Parameter mapping hoặc path forwarding không làm mất prefix `/api`.
- Backend phải nhận đúng đường dẫn gốc như `/api/health`, `/api/auth/login` hoặc `/api/assets`.
- Integration URI có thể dùng `http://<elastic-beanstalk-domain>/{proxy}` khi route có biến `{proxy+}`.

![Health endpoint qua API Gateway](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.4-api-gateway-health.png)

*Hình 5.5.4. Health endpoint qua API Gateway trả kết quả thành công.*

Khi gọi `/api/health` qua API Gateway, response cần trả `success: true` và `status: ok`. Kết quả này xác nhận route, integration và stage của API Gateway hoạt động đúng.

## Bước 3: Kiểm tra frontend build local

Từ thư mục frontend:

```bash
cd frontend
npm ci
npm run build
```

Output build production:

```text
dist/
```

## Bước 4: Kiểm tra Amplify build settings

Repository có thể dùng file `amplify.yml` cho cấu trúc monorepo:

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

![Build settings của Amplify](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.6-amplify-build-settings.png)

*Hình 5.5.6. Build settings của Amplify với app root và output directory.*

Build settings cần khớp với cấu trúc project: `appRoot` là `frontend`, build command là `npm ci && npm run build` và output directory là `dist`.

## Bước 5: Tạo Amplify app

Mở AWS Amplify console:

1. Chọn **New app** hoặc **Host web app**.
2. Kết nối GitHub repository.
3. Chọn branch triển khai, ví dụ `aws-architecture`.
4. Đặt monorepo root là `frontend` nếu Amplify yêu cầu.
5. Kiểm tra build command:

```bash
npm ci && npm run build
```

6. Kiểm tra output directory:

```text
dist
```

![Amplify app kết nối branch aws-architecture](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.5-amplify-branch.png)

*Hình 5.5.5. Amplify app kết nối đúng branch triển khai.*

Branch deploy phải là branch chứa source frontend mới nhất. Sau khi kết nối, Amplify sẽ tự động build và publish frontend theo cấu hình đã chọn.

![Amplify deployment thành công](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.8-amplify-build-success.png)

*Hình 5.5.8. Amplify deployment thành công.*

Khi deployment ở trạng thái `Deployed`, frontend đã được build và xuất bản thành công trên Amplify domain. Đây là điều kiện trước khi kiểm thử giao diện và rewrite API.

## Bước 6: Đặt biến môi trường frontend

Trong Amplify, đặt:

```env
VITE_API_BASE_URL=/api
```

Biến này giúp browser gọi API qua cùng Amplify domain:

```text
https://<amplify-domain>/api/...
```

## Bước 7: Cấu hình Amplify rewrite

Sau khi app được tạo, mở **Rewrites and redirects**.

Thêm rule này ở phía trên SPA fallback rule:

| Source address | Target address | Type |
| --- | --- | --- |
| `/api/<*>` | `https://<api-gateway-endpoint>/api/<*>` | `200 (Rewrite)` |
| `/uploads/<*>` | `https://<api-gateway-endpoint>/uploads/<*>` | `200 (Rewrite)` |

Sau đó giữ SPA fallback rule cho React Router:

| Source address | Target address | Type |
| --- | --- | --- |
| `/<*>` | `/index.html` | `404 (Rewrite)` hoặc `404-200` |

Nếu rule `/api/<*>` hoặc `/uploads/<*>` đặt sai thứ tự, request API hoặc ảnh upload có thể bị trả về HTML của frontend, gây lỗi `404`, lỗi ảnh không hiển thị hoặc static assets bị lỗi MIME type.

![Rewrite rules của Amplify](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.7-amplify-rewrite-rules.png)

*Hình 5.5.7. Rewrite rules của Amplify chuyển tiếp `/api/<*>` và `/uploads/<*>` đến API Gateway.*

Hai rule `/api/<*>` và `/uploads/<*>` phải nằm phía trên rule fallback `/index.html`. Thứ tự này đảm bảo request API và file upload đi đến API Gateway thay vì bị React Router xử lý như route frontend.

## Bước 8: Cập nhật backend CORS origin

Sau khi Amplify deploy xong, copy URL mặc định của Amplify:

```text
https://main.xxxxx.amplifyapp.com
```

Nếu deploy từ branch khác, hãy dùng đúng domain của branch đó, ví dụ:

```text
https://aws-architecture.xxxxx.amplifyapp.com
```

Cập nhật biến môi trường backend:

```env
FRONTEND_ORIGIN=https://main.xxxxx.amplifyapp.com
FRONTEND_ORIGINS=https://main.xxxxx.amplifyapp.com
```

Redeploy hoặc restart Elastic Beanstalk environment sau khi cập nhật giá trị này.

## Kết quả của bước này

Ghi lại:

- API Gateway endpoint.
- Amplify app URL.
- Giá trị `FRONTEND_ORIGIN`.
- Trạng thái frontend build.
- Kết quả test `https://<amplify-domain>/api/health`.

![Health endpoint qua Amplify domain](/eam-workshop-report/images/5-Workshop/5.5-Frontend-Amplify/5.5.9-amplify-health.png)

*Hình 5.5.9. Health endpoint qua Amplify domain trả kết quả thành công.*

Tại bước kiểm thử cuối, gọi `https://<amplify-domain>/api/health`. Request sẽ đi qua Amplify rewrite, API Gateway và Elastic Beanstalk trước khi trả về response thành công.
