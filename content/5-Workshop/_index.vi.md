---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Triển khai EAM Workspace trên AWS

#### Tổng quan

Workshop này hướng dẫn triển khai **EAM Workspace**, hệ thống quản lý tài sản doanh nghiệp, lên AWS theo mô hình demo full-stack. Ứng dụng gồm giao diện React/Vite, backend Node.js/Express, Prisma ORM và database MySQL.

Luồng triển khai được thiết kế để phù hợp với project đã thực hiện trong kỳ thực tập: frontend chạy trên AWS Amplify Hosting, API public đi qua Amazon API Gateway, backend chạy trên AWS Elastic Beanstalk và dữ liệu lưu trong Amazon RDS for MySQL.

Các dịch vụ chính:

- **AWS Amplify Hosting** cho frontend React.
- **Amazon API Gateway HTTP API** cho route `/api/*`.
- **AWS Elastic Beanstalk** cho backend Node.js/Express.
- **Amazon RDS for MySQL** cho dữ liệu ứng dụng.
- **Amazon S3** cho hướng lưu trữ file sẵn sàng production.
- **Amazon SES** cho OTP và email flow.
- **Amazon CloudWatch** cho log và kiểm tra lỗi.

Workshop này dùng hướng demo: không dùng Route 53, không dùng custom domain và không dùng Amazon Cognito. Xác thực được backend xử lý bằng JWT.

#### Kiến trúc

{{< mermaid >}}
graph LR
    User["Trình duyệt người dùng"] --> Amplify["AWS Amplify Hosting\nReact Frontend"]
    Amplify --> Rewrite["Rewrite /api/*"]
    Rewrite --> APIGW["Amazon API Gateway\nHTTP API"]
    APIGW --> EB["AWS Elastic Beanstalk\nNode.js Backend"]
    EB --> RDS["Amazon RDS MySQL"]
    EB --> S3["Amazon S3\nProduction-ready File Storage"]
    EB --> SES["Amazon SES"]
    EB --> CW["CloudWatch Logs"]
{{< /mermaid >}}

#### Nội dung

1. [Tổng quan workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequisites/)
3. [Chuẩn bị network và RDS](5.3-Network-RDS/)
4. [Triển khai backend bằng Elastic Beanstalk](5.4-Backend-Elastic-Beanstalk/)
5. [Kết nối API Gateway và Amplify Hosting](5.5-Frontend-Amplify/)
6. [Kiểm thử, monitoring và xử lý lỗi](5.6-Test-Monitor/)
7. [Dọn dẹp tài nguyên](5.7-Cleanup/)
