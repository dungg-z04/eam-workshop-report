---
title: "Triá»ƒn khai frontend báº±ng Amplify Hosting"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Triá»ƒn khai frontend báº±ng Amplify Hosting

á»ž bÆ°á»›c nÃ y, chÃºng ta sáº½ deploy frontend React lÃªn AWS Amplify Hosting vÃ  káº¿t ná»‘i frontend vá»›i backend thÃ´ng qua Amplify rewrite rule.

## BÆ°á»›c 1: Kiá»ƒm tra frontend build local

Tá»« thÆ° má»¥c frontend:

```bash
cd frontend
npm ci
npm run build
```

Output build production sáº½ lÃ :

```text
dist/
```

## BÆ°á»›c 2: Kiá»ƒm tra Amplify build settings

Repository cÃ³ file `amplify.yml` cho cáº¥u trÃºc monorepo:

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

## BÆ°á»›c 3: Táº¡o Amplify app

Má»Ÿ AWS Amplify console:

1. Chá»n **New app** hoáº·c **Host web app**.
2. Káº¿t ná»‘i GitHub repository.
3. Chá»n branch cáº§n deploy, thÆ°á»ng lÃ  `main`.
4. Äáº·t app root lÃ  `frontend` náº¿u Amplify há»i monorepo app root.
5. Kiá»ƒm tra build command:

```bash
npm ci && npm run build
```

6. Kiá»ƒm tra output directory:

```text
dist
```

## BÆ°á»›c 4: Äáº·t biáº¿n mÃ´i trÆ°á»ng frontend

Äáº·t biáº¿n mÃ´i trÆ°á»ng sau trong Amplify:

```env
VITE_API_BASE_URL=/api
```

Biáº¿n nÃ y giÃºp browser gá»i API qua cÃ¹ng Amplify domain:

```text
https://<amplify-domain>/api/...
```

## BÆ°á»›c 5: Cáº¥u hÃ¬nh API rewrite

Sau khi app Ä‘Æ°á»£c táº¡o, má»Ÿ **Rewrites and redirects**.

ThÃªm rule nÃ y á»Ÿ phÃ­a trÃªn SPA fallback rule:

| Source address | Target address | Type |
| --- | --- | --- |
| `/api/<*>` | `http://<alb-dns-name>/api/<*>` | `200 (Rewrite)` |

Sau Ä‘Ã³ giá»¯ SPA fallback rule cho React Router:

| Source address | Target address | Type |
| --- | --- | --- |
| `/<*>` | `/index.html` | `404 (Rewrite)` hoáº·c `404-200` |


## BÆ°á»›c 6: Cáº­p nháº­t backend CORS origin

Sau khi Amplify deploy xong, copy URL máº·c Ä‘á»‹nh cá»§a Amplify, vÃ­ dá»¥:

```text
https://main.xxxxx.amplifyapp.com
```

Cáº­p nháº­t biáº¿n mÃ´i trÆ°á»ng backend:

```env
FRONTEND_ORIGIN=https://main.xxxxx.amplifyapp.com
```

Redeploy hoáº·c restart Elastic Beanstalk environment sau khi cáº­p nháº­t giÃ¡ trá»‹ nÃ y.

## BÆ°á»›c 7: Má»Ÿ á»©ng dá»¥ng

Má»Ÿ URL Amplify trÃªn trÃ¬nh duyá»‡t vÃ  kiá»ƒm tra:

- Trang login hiá»ƒn thá»‹.
- Static assets táº£i Ä‘Ãºng.
- Refresh `/login`, `/admin/dashboard` hoáº·c `/employee/dashboard` khÃ´ng bá»‹ 404.
- Browser DevTools cho tháº¥y API request Ä‘i Ä‘áº¿n `/api/...` trÃªn Amplify domain.

## Káº¿t quáº£ cá»§a bÆ°á»›c nÃ y

Ghi láº¡i:

- Amplify app URL
- ALB DNS name dÃ¹ng trong rewrite rule
- GiÃ¡ trá»‹ `FRONTEND_ORIGIN`
- Tráº¡ng thÃ¡i frontend build
