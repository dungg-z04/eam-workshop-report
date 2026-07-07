---
title: "Chuẩn bị network và RDS"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

## Chuẩn bị network và RDS

Bước này chuẩn bị database MySQL cho backend. Với môi trường demo, có thể dùng VPC mặc định hoặc VPC đã có sẵn, miễn là Elastic Beanstalk backend có thể kết nối đến Amazon RDS qua port `3306`.

## Mô hình kết nối mục tiêu

{{< mermaid >}}
graph LR
    APIGW["Amazon API Gateway"] --> EB["Elastic Beanstalk Backend"]
    EB --> SGBackend["Backend Security Group"]
    SGBackend --> RDS["Amazon RDS MySQL"]
    RDS --> SGRDS["RDS Security Group"]
{{< /mermaid >}}

## Bước 1: Chọn VPC

Dùng một VPC cố định cho Elastic Beanstalk và RDS. VPC nên có:

- Subnet cho Elastic Beanstalk environment.
- Subnet group cho RDS.
- Route Internet phù hợp để backend có thể nhận request public qua Elastic Beanstalk.
- Security group tách riêng cho backend và database.

Nếu workshop chỉ phục vụ demo ngắn hạn, có thể dùng cấu hình đơn giản hơn so với kiến trúc production nhiều subnet.

![VPC được sử dụng cho Elastic Beanstalk và RDS](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.1-vpc-subnets.png)

*Hình 5.3.1. VPC được sử dụng cho Elastic Beanstalk và RDS.*

VPC và CIDR trong ảnh cần khớp với môi trường dùng cho backend và database. Backend Elastic Beanstalk và RDS cần nằm trong cùng VPC hoặc có định tuyến phù hợp để kết nối an toàn.

## Bước 2: Tạo security group

Tạo hoặc kiểm tra các security group sau:

| Security group | Inbound rule | Mục đích |
| --- | --- | --- |
| `eam-backend-sg` | HTTP từ Internet hoặc từ cấu hình Elastic Beanstalk được chọn | Cho phép API Gateway gọi backend endpoint. |
| `eam-rds-sg` | MySQL `3306` từ `eam-backend-sg` | Chỉ cho backend kết nối database. |

Điểm quan trọng nhất là RDS không nên mở `3306` cho toàn bộ Internet. Chỉ cho phép backend security group truy cập database.

![Security group của backend Elastic Beanstalk](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.2-backend-security-group.png)

*Hình 5.3.2. Security group của backend Elastic Beanstalk.*

Security group ID của backend cần được ghi lại để dùng làm source cho rule inbound của RDS.

![Security group của RDS cho phép backend truy cập MySQL](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.3-rds-security-group.png)

*Hình 5.3.3. Security group của RDS cho phép backend truy cập port 3306.*

Rule inbound MySQL/Aurora `3306` của RDS chỉ nên cho phép source là security group của backend, không mở `0.0.0.0/0`.

## Bước 3: Tạo Amazon RDS for MySQL

Mở Amazon RDS console và tạo database:

1. Chọn **Create database**.
2. Chọn **Standard create**.
3. Chọn engine **MySQL**.
4. Chọn template **Dev/Test** hoặc cấu hình chi phí thấp.
5. Đặt DB instance identifier, ví dụ `eam-mysql-demo`.
6. Đặt master username, ví dụ `asset_app`.
7. Đặt mật khẩu mạnh và lưu ở nơi an toàn.
8. Chọn instance class nhỏ cho môi trường demo.
9. Chọn dung lượng storage phù hợp để test.
10. Trong **Connectivity**, chọn VPC mục tiêu.
11. Chọn DB subnet group phù hợp.
12. Nếu có thể, đặt **Public access** là **No**.
13. Gắn `eam-rds-sg`.
14. Bật storage encryption nếu cần.
15. Đặt initial database name:

```text
enterprise_asset_management
```

Chờ database chuyển sang trạng thái **Available**.

![RDS database ở trạng thái Available](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.4-rds-available.png)

*Hình 5.3.4. RDS database ở trạng thái Available.*

Khi trạng thái database là `Available`, RDS đã sẵn sàng nhận kết nối. Chỉ nên tiếp tục cấu hình backend sau khi trạng thái này hiển thị ổn định.

## Bước 4: Ghi lại thông tin kết nối

Sau khi RDS available, ghi lại:

- RDS endpoint
- Port, thường là `3306`
- Database name
- Username
- Password

Tạo backend `DATABASE_URL`:

```env
DATABASE_URL=mysql://asset_app:<password>@<rds-endpoint>:3306/enterprise_asset_management
```

![Thông tin kết nối và security của RDS](/eam-workshop-report/images/5-Workshop/5.3-Network-RDS/5.3.5-rds-connectivity.png)

*Hình 5.3.5. Thông tin kết nối và security của RDS.*

Tại phần Connectivity & security, cần lấy đúng endpoint, port, VPC và security group. Các giá trị này được dùng để tạo `DATABASE_URL` cho Elastic Beanstalk.

## Bước 5: Kiểm tra bảo mật

Trước khi tiếp tục, kiểm tra:

- RDS không mở database port cho toàn bộ Internet.
- Inbound rule của RDS chỉ cho `3306` từ backend security group.
- Backend và RDS nằm trong cùng VPC hoặc có route phù hợp.
- Username/password database đã được lưu an toàn và không commit vào source code.

## Kết quả mong đợi

Kết thúc bước này, project có một MySQL database sẵn sàng để backend Elastic Beanstalk kết nối thông qua `DATABASE_URL`.
