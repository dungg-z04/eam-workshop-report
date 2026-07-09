---
title: "Dọn dẹp tài nguyên"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---


Sau khi hoàn thành workshop triển khai **EAM Workspace** trên AWS, cần dọn dẹp các tài nguyên không còn sử dụng để tránh phát sinh chi phí ngoài dự kiến. Ở workshop này, các tài nguyên chính đã sử dụng gồm **AWS Amplify Hosting**, **Amazon API Gateway**, **AWS Elastic Beanstalk**, **Amazon RDS for MySQL**, **Amazon SES**, security group và một số log/metric liên quan.

Trước khi xóa tài nguyên, cần chụp lại các màn hình quan trọng để đưa vào báo cáo. Các ảnh này giúp chứng minh project đã được triển khai, kiểm thử và có kế hoạch cleanup rõ ràng.

### Tổng kết nội dung đã thực hiện

Trong workshop này, hệ thống EAM Workspace đã được triển khai theo mô hình web full-stack trên AWS:

- Frontend React/Vite được build và host bằng **AWS Amplify Hosting**.
- Request `/api/*` từ frontend được chuyển đến **Amazon API Gateway**.
- API Gateway chuyển tiếp request đến backend chạy trên **AWS Elastic Beanstalk**.
- Backend kết nối đến **Amazon RDS for MySQL** để lưu dữ liệu nghiệp vụ.
- Chức năng gửi email/OTP sử dụng **Amazon SES** thông qua SMTP credential.
- Kết quả triển khai được kiểm tra bằng health endpoint, giao diện đăng nhập, dashboard và các màn hình nghiệp vụ chính.

Sau khi đã hoàn tất phần kiểm thử và ghi nhận ảnh minh họa, các tài nguyên demo có thể được xóa theo thứ tự bên dưới.

## Bước 1: Ghi lại danh sách tài nguyên cần dọn dẹp

Trước khi xóa, nên ghi lại tên các tài nguyên đã tạo trong workshop:

| Nhóm tài nguyên | Tên hoặc nội dung cần kiểm tra |
| --- | --- |
| Amplify app | App frontend `quanlidoanhnghiep` hoặc branch deploy `aws-architecture` |
| API Gateway | HTTP API `eam-backend-http-api` |
| Elastic Beanstalk | Environment backend, ví dụ `eam-backend-prod-v8` |
| RDS | MySQL database dùng cho EAM Workspace |
| SES | Email identity và SMTP credential dùng để gửi email |
| CloudWatch | Log/metric liên quan đến Elastic Beanstalk hoặc API |
| EC2/Security Group | Security group của Elastic Beanstalk và RDS |

Việc ghi lại danh sách này giúp tránh xóa nhầm tài nguyên không thuộc workshop.

## Bước 2: Xóa hoặc disconnect AWS Amplify app

AWS Amplify Hosting đang dùng để build và public frontend. Nếu không còn cần demo giao diện, có thể xóa app hoặc disconnect branch deploy.

Các bước thực hiện:

1. Mở **AWS Amplify** console.
2. Chọn app frontend của project, ví dụ `quanlidoanhnghiep`.
3. Chọn branch deploy đang dùng, ví dụ `aws-architecture`.
4. Chọn **App settings** hoặc **General settings** và thực hiện xóa app.


![Amplify app cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.1-amplify-cleanup.png)

*Hình 5.7.1. AWS Amplify app `quanlidoanhnghiep` và branch `aws-architecture`.*


## Bước 3: Xóa Amazon API Gateway

API Gateway là lớp public endpoint để frontend gọi backend. Nếu API không còn dùng, nên xóa để tránh endpoint vẫn tiếp tục nhận request.

Các bước thực hiện:

1. Mở **Amazon API Gateway** console.
2. Chọn HTTP API của project, ví dụ `eam-backend-http-api`.
3. Kiểm tra route `ANY /{proxy+}` và integration đang trỏ đến Elastic Beanstalk backend.
4. Chọn **Delete** để xóa API nếu không còn cần sử dụng.
5. Kiểm tra lại danh sách API để xác nhận API đã được xóa.

Sau khi xóa API Gateway, các URL dạng `https://...execute-api.ap-southeast-1.amazonaws.com/...` sẽ không còn hoạt động.

![API Gateway cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.2-api-gateway-cleanup.png)

*Hình 5.7.2. HTTP API `eam-backend-http-api` trong Amazon API Gateway trước khi xóa.*


## Bước 4: Terminate Elastic Beanstalk environment

Elastic Beanstalk quản lý môi trường chạy backend Node.js/Express. Đây là tài nguyên có thể tạo EC2 instance, load balancer, Auto Scaling resource và security group liên quan, vì vậy cần terminate khi không còn sử dụng.

Các bước thực hiện:

1. Mở **Elastic Beanstalk** console.
2. Chọn environment backend, ví dụ `eam-backend-prod-v8`.
3. Chọn **Actions** -> **Terminate environment**.
4. Nhập tên environment để xác nhận nếu AWS yêu cầu.
5. Chờ đến khi environment chuyển sang trạng thái terminated.
6. Kiểm tra EC2 console để bảo đảm instance do Elastic Beanstalk tạo đã được dừng/xóa.

Nếu Elastic Beanstalk chưa terminate được do dependency, cần kiểm tra thêm security group, load balancer hoặc EC2 resource liên quan.

![Elastic Beanstalk cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.3-eb-cleanup.png)

*Hình 5.7.3. Elastic Beanstalk environment `eam-backend-prod-v8` trước khi terminate. Ảnh thể hiện environment backend đang ở trạng thái hoạt động ổn định, có domain riêng và là tài nguyên có thể phát sinh chi phí nếu tiếp tục chạy.*



## Bước 5: Xóa hoặc tạm dừng Amazon RDS for MySQL

Amazon RDS là tài nguyên quan trọng vì có thể phát sinh chi phí khi database instance vẫn chạy. Trước khi xóa, cần xác định có cần giữ dữ liệu demo hay không.

Các bước thực hiện:

1. Mở **Amazon RDS** console.
2. Chọn database MySQL của project EAM Workspace.
3. Nếu cần giữ dữ liệu, tạo snapshot trước khi xóa.
4. Chọn database database `eam-mysql` -> **Actions** -> **Delete**.
5. Xác nhận database đã chuyển sang trạng thái deleting/deleted.
6. Sau khi RDS bị xóa, kiểm tra lại security group liên quan vì có thể không còn dependency và có thể xóa tiếp.


![RDS cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.4-rds-cleanup.png)

*Hình 5.7.4. Amazon RDS database `eam-mysql` được kiểm tra trước khi cleanup. Đây là tài nguyên cần chú ý vì database instance vẫn có thể phát sinh chi phí khi còn ở trạng thái available.*

## Bước 6: Kiểm tra Amazon SES

Amazon SES trong workshop được dùng để xác thực email identity và tạo SMTP credential cho backend gửi email/OTP. SES thường không phát sinh chi phí lớn nếu không gửi email nhiều, nhưng vẫn nên kiểm tra lại cấu hình.

Các bước thực hiện:

1. Mở **Amazon SES** console.
2. Kiểm tra email identity đã xác thực.
3. Kiểm tra SMTP credential/IAM user đã tạo cho SES.
4. Nếu không còn sử dụng, xóa IAM user hoặc credential liên quan đến SMTP.


![SES cleanup](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.5-ses-cleanup.png)

*Hình 5.7.5. Amazon SES email identity đã được xác thực tại region Singapore.*


## Bước 7: Xóa security group và tài nguyên phụ thuộc

Sau khi Elastic Beanstalk và RDS đã được xóa, kiểm tra lại các security group không còn sử dụng.

Các bước thực hiện:

1. Mở **EC2** console.
2. Vào **Security Groups**.
3. Tìm các security group liên quan đến Elastic Beanstalk backend và RDS.
4. Chỉ xóa security group khi không còn resource nào phụ thuộc.
5. Nếu AWS báo lỗi dependency, kiểm tra lại EC2 instance, load balancer, RDS hoặc network interface.

Không nên xóa default security group hoặc security group không liên quan.

## Bước 8: Kiểm tra CloudWatch và Billing

Sau khi dọn các tài nguyên chính, cần kiểm tra lại log và chi phí.

Các bước thực hiện:

1. Mở **CloudWatch** console.
2. Kiểm tra log groups liên quan đến Elastic Beanstalk hoặc backend.
3. Xóa log group không còn cần sử dụng hoặc giảm retention nếu muốn giữ log.
4. Mở **Billing and Cost Management**.
5. Kiểm tra Cost Explorer hoặc Bills để xác nhận không còn tài nguyên phát sinh chi phí bất thường.

Các tài nguyên cần chú ý nhất về chi phí gồm RDS database, EC2/Elastic Beanstalk, Load Balancer, NAT Gateway, Elastic IP và CloudWatch Logs.

![Billing check](/eam-workshop-report/images/5-Workshop/5.7-Cleanup/5.7.6-billing-check.png)

*Hình 5.7.6. Billing and Cost Management được dùng để theo dõi chi phí sau quá trình triển khai AWS.*

Sau khi cleanup các tài nguyên chính, cần kiểm tra chi phí:

1. Mở **Billing and Cost Management**.
2. Kiểm tra **Cost summary** để xem chi phí tháng hiện tại và dự báo cuối tháng.
3. Xem **Cost breakdown** theo service để phát hiện dịch vụ nào vẫn còn phát sinh chi phí.
4. Các service cần chú ý gồm Amazon RDS, EC2, Elastic Load Balancing, VPC, API Gateway, Amplify và CloudWatch.
5. Nếu vẫn thấy chi phí tăng bất thường sau khi cleanup, quay lại từng service để kiểm tra tài nguyên còn sót.

## Checklist dọn dẹp cuối cùng

- Đã ghi lại danh sách tài nguyên được tạo trong workshop.
- Đã chụp ảnh Amplify app/branch trước khi xóa hoặc disconnect.
- Đã xóa API Gateway không còn sử dụng.
- Đã terminate Elastic Beanstalk environment.
- Đã xóa hoặc tạm dừng RDS database theo nhu cầu demo.
- Đã kiểm tra SES identity và SMTP credential.
- Đã xóa security group không còn dependency.
- Đã kiểm tra CloudWatch log groups.
- Đã kiểm tra Billing/Cost Explorer sau cleanup.
