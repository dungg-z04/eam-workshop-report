---
title: "Triển khai frontend bằng Amplify Hosting"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Triển khai frontend bằng Amplify Hosting

Ở bước này, chúng ta sẽ deploy frontend React lên AWS Amplify Hosting và kết nối frontend với backend thông qua Amplify rewrite rule.

## Bước 1: Kiểm tra frontend build local

Từ thư mục frontend:

```bash
cd frontend
npm ci
npm run build
```

Output build production sẽ là:

```text
dist/
```

## Bước 2: Kiểm tra Amplify build settings

Repository có file `amplify.yml` cho cấu trúc monorepo:

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

## Bước 3: Tạo Amplify app

Mở AWS Amplify console:

1. Chọn **New app** hoặc **Host web app**.
2. Kết nối GitHub repository.
3. Chọn branch cần deploy, thường là `main`.
4. Đặt app root là `frontend` nếu Amplify hỏi monorepo app root.
5. Kiểm tra build command:

```bash
npm ci && npm run build
```

6. Kiểm tra output directory:

```text
dist
```

## Bước 4: Đặt biến môi trường frontend

Đặt biến môi trường sau trong Amplify:

```env
VITE_API_BASE_URL=/api
```

Biến này giúp browser gọi API qua cùng Amplify domain:

```text
https://<amplify-domain>/api/...
```

## Bước 5: Cấu hình API rewrite

Sau khi app được tạo, mở **Rewrites and redirects**.

Thêm rule này ở phía trên SPA fallback rule:

| Source address | Target address | Type |
| --- | --- | --- |
| `/api/<*>` | `http://<alb-dns-name>/api/<*>` | `200 (Rewrite)` |

Sau đó giữ SPA fallback rule cho React Router:

| Source address | Target address | Type |
| --- | --- | --- |
| `/<*>` | `/index.html` | `404 (Rewrite)` hoặc `404-200` |

{{% notice warning %}}
Rule `/api/<*>` phải nằm trên SPA fallback rule. Nếu không, API request có thể bị xử lý nhầm như frontend route.
{{% /notice %}}

## Bước 6: Cập nhật backend CORS origin

Sau khi Amplify deploy xong, copy URL mặc định của Amplify, ví dụ:

```text
https://main.xxxxx.amplifyapp.com
```

Cập nhật biến môi trường backend:

```env
FRONTEND_ORIGIN=https://main.xxxxx.amplifyapp.com
```

Redeploy hoặc restart Elastic Beanstalk environment sau khi cập nhật giá trị này.

## Bước 7: Mở ứng dụng

Mở URL Amplify trên trình duyệt và kiểm tra:

- Trang login hiển thị.
- Static assets tải đúng.
- Refresh `/login`, `/admin/dashboard` hoặc `/employee/dashboard` không bị 404.
- Browser DevTools cho thấy API request đi đến `/api/...` trên Amplify domain.

## Kết quả của bước này

Ghi lại:

- Amplify app URL
- ALB DNS name dùng trong rewrite rule
- Giá trị `FRONTEND_ORIGIN`
- Trạng thái frontend build
