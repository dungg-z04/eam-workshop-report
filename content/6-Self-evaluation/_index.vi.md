---
title: "Tự đánh giá"
date: 2026-07-05
weight: 6
chapter: false
pre: " <b> 6. </b> "
---


Trong thời gian thực tập từ **17/04/2026 đến 10/07/2026** tại **Công ty TNHH Amazon Web Services Việt Nam** trong chương trình **Workforce Bootcamp - First Cloud AI Journey**, em có cơ hội tiếp cận AWS theo hướng thực tế hơn thông qua việc tự học, tham gia event, đọc AWS Blog, thực hành triển khai project và viết workshop báo cáo.

Project được sử dụng trong báo cáo là **EAM Workspace - Hệ thống quản lý tài sản doanh nghiệp**. Dù em có tham gia vào phần frontend của project, trọng tâm quan trọng nhất trong kỳ thực tập là cách đưa một ứng dụng web full-stack lên môi trường AWS, hiểu vai trò của từng dịch vụ trong kiến trúc triển khai và ghi lại quy trình đó thành tài liệu có thể theo dõi được.

## 1. Kết quả đạt được

### 1.1. Kiến thức nền tảng AWS

Trong giai đoạn đầu, em bắt đầu từ các khái niệm cơ bản như **Cloud Computing**, **AWS Global Infrastructure**, **AWS Management Console**, **AWS Free Tier**, **AWS Budgets** và cách kiểm soát chi phí khi sử dụng tài khoản AWS.

Sau đó, em tiếp tục tìm hiểu các nhóm dịch vụ chính:

- **IAM**: user, group, role, policy và nguyên tắc phân quyền tối thiểu.
- **Networking**: VPC, subnet, route table, Internet Gateway, NAT Gateway, Security Group và Network ACL.
- **Compute**: EC2, AMI, instance type, Elastic IP và cách compute được sử dụng khi chạy backend.
- **Database**: Amazon RDS for MySQL, endpoint, backup, database engine và kết nối từ backend.
- **Storage**: Amazon S3, object storage, upload file và hướng mở rộng cho lưu trữ ảnh/tài liệu.
- **Deployment**: AWS Amplify Hosting, Elastic Beanstalk, API Gateway và các bước đưa ứng dụng lên môi trường cloud.
- **Monitoring/Security**: CloudWatch, CloudTrail, WAF, KMS, Secrets Manager và các khái niệm bảo vệ hệ thống.

Nhờ quá trình này, em hiểu rõ hơn rằng AWS không chỉ là nơi thuê máy chủ, mà là một hệ sinh thái dịch vụ giúp xây dựng, triển khai, giám sát và bảo vệ ứng dụng.

### 1.2. Áp dụng AWS vào project EAM Workspace

Phần triển khai AWS là nội dung giúp em học được nhiều nhất. Thay vì chỉ đọc tài liệu, em có cơ hội nhìn thấy từng dịch vụ AWS tham gia vào kiến trúc của project:

- **AWS Amplify Hosting** dùng để build và host frontend React/Vite.
- **Amazon API Gateway** dùng để tạo endpoint public và chuyển request `/api/*` đến backend.
- **AWS Elastic Beanstalk** dùng để triển khai backend Node.js/Express.
- **Amazon RDS for MySQL** dùng để lưu dữ liệu nghiệp vụ của hệ thống.
- **Amazon SES** dùng cho luồng gửi email/OTP thông qua SMTP credential.
- **CloudWatch** dùng để theo dõi trạng thái, log và hỗ trợ kiểm tra lỗi khi triển khai.

Qua quá trình này, em hiểu hơn mối liên hệ giữa frontend, backend, database và các dịch vụ AWS. Một ứng dụng chạy được ở local chưa đủ để gọi là hoàn chỉnh; khi triển khai lên AWS cần quan tâm thêm đến biến môi trường, endpoint, quyền truy cập, network, database connection, build settings, rewrite rule và trạng thái health của backend.

### 1.3. Kỹ năng triển khai và xử lý lỗi

Trong quá trình triển khai, em gặp và tìm hiểu nhiều vấn đề thực tế như:

- Cách cấu hình environment variables cho Elastic Beanstalk.
- Cách dùng SMTP username/password của Amazon SES.
- Cách kiểm tra backend health endpoint qua API Gateway.
- Cách cấu hình Amplify rewrite để frontend gọi được API.
- Cách xác định lỗi nằm ở frontend, API Gateway, backend hay database.
- Cách ghi lại các bước triển khai bằng hình ảnh và mô tả rõ ràng trong workshop.

Những phần này giúp em rèn luyện tư duy kiểm tra theo từng lớp. Khi một chức năng không chạy, em không chỉ nhìn vào code mà còn phải kiểm tra cấu hình AWS, endpoint, network, credential và trạng thái deploy.

### 1.4. Kỹ năng đọc tài liệu AWS và tổng hợp kiến thức

Trong kỳ thực tập, em đọc và tổng hợp các bài AWS Blog liên quan đến EKS, Istio Ambient Mesh, EKS Control Plane Egress và AWS Continuum. Việc đọc blog kỹ thuật giúp em làm quen hơn với cách AWS trình bày giải pháp, kiến trúc và vấn đề vận hành trong môi trường thực tế.

Ngoài ra, các event đã tham gia cũng giúp em mở rộng góc nhìn về AWS trong nhiều mảng khác nhau như security, AI, container, tuyển dụng, tự động hóa quy trình và cách doanh nghiệp áp dụng cloud vào hoạt động vận hành.

Từ đó, em nhận ra việc học AWS không chỉ nằm ở thao tác trên console, mà còn cần biết đọc tài liệu, chọn lọc ý chính, hiểu use case và liên hệ lại với project đang làm.

### 1.5. Kỹ năng viết workshop và báo cáo

Một điểm em cải thiện rõ là khả năng viết lại quy trình kỹ thuật thành tài liệu. Khi làm workshop triển khai EAM Workspace lên AWS, em phải trình bày từng bước theo thứ tự dễ theo dõi:

- Mục tiêu của bước triển khai.
- Dịch vụ AWS được sử dụng.
- Cấu hình cần chuẩn bị.
- Ảnh minh họa cần chụp.
- Kết quả mong đợi sau mỗi bước.
- Lỗi thường gặp và cách kiểm tra.

Quá trình này giúp em hiểu rằng tài liệu kỹ thuật tốt không chỉ ghi “đã làm gì”, mà còn cần giải thích “vì sao làm”, “làm ở đâu”, “kiểm tra bằng cách nào” và “kết quả đúng trông như thế nào”.

## 2. Bảng tự đánh giá

| STT | Tiêu chí | Mô tả | Mức tự đánh giá |
| --- | --- | --- | --- |
| 1 | Kiến thức AWS nền tảng | Hiểu các khái niệm cơ bản về IAM, VPC, EC2, RDS, S3, CloudWatch và chi phí AWS | Khá |
| 2 | Triển khai AWS | Có thể triển khai demo frontend, backend, API Gateway, RDS và SES ở mức project thực tập | Khá |
| 3 | Hiểu kiến trúc cloud | Nắm được luồng người dùng từ Amplify đến API Gateway, Elastic Beanstalk và RDS | Khá |
| 4 | Xử lý lỗi triển khai | Biết kiểm tra endpoint, biến môi trường, health check, rewrite rule và kết nối database | Khá |
| 5 | Đọc tài liệu AWS | Có thể đọc AWS Blog/tài liệu kỹ thuật và viết lại nội dung theo hướng dễ hiểu hơn | Tốt |
| 6 | Viết workshop | Biết mô tả bước triển khai, thêm ảnh minh họa và ghi chú kết quả kiểm tra | Tốt |
| 7 | Tự học cloud | Chủ động tìm hiểu thêm dịch vụ AWS theo nhu cầu của project | Tốt |
| 8 | Làm việc nhóm | Phối hợp với nhóm để hiểu frontend, backend, database và nội dung triển khai | Khá |
| 9 | Quản lý tiến độ | Duy trì worklog, proposal, blog, event, workshop và self-evaluation theo từng giai đoạn | Khá |
| 10 | Tổng thể | Hoàn thành được báo cáo cá nhân gắn với project và quá trình học AWS | Tốt |

## 3. Điểm mạnh

- Em có tinh thần chủ động khi tìm hiểu dịch vụ AWS phục vụ cho project.
- Em biết liên hệ kiến thức AWS đã học với kiến trúc triển khai EAM Workspace.
- Em có khả năng đọc tài liệu, blog kỹ thuật và viết lại thành nội dung báo cáo dễ theo dõi.
- Em hiểu được luồng triển khai full-stack cơ bản trên AWS gồm frontend, API, backend và database.
- Em cải thiện kỹ năng viết workshop, mô tả ảnh minh họa và trình bày kết quả kiểm thử.

## 4. Điểm cần cải thiện

- Em cần thực hành sâu hơn với AWS CLI và Infrastructure as Code để giảm phụ thuộc vào thao tác thủ công trên console.
- Em cần luyện thêm cách đọc CloudWatch Logs và debug lỗi backend trên môi trường cloud.
- Em cần hiểu rõ hơn về network nâng cao như private subnet, NAT Gateway, VPC Endpoint và security best practices.
- Em cần học thêm về bảo mật secrets, phân quyền IAM chi tiết và cách tách môi trường dev/staging/production.
- Em cần rèn luyện thêm khả năng tối ưu chi phí AWS khi thiết kế kiến trúc triển khai.

## 5. Bài học rút ra

Qua kỳ thực tập, em nhận ra AWS không chỉ là công cụ triển khai ứng dụng, mà còn là cách tiếp cận để xây dựng hệ thống có khả năng vận hành tốt hơn. Khi đưa project lên AWS, em phải suy nghĩ nhiều hơn về kiến trúc, quyền truy cập, database, endpoint, monitoring và khả năng mở rộng.

Em cũng nhận ra rằng học cloud cần đi kèm thực hành. Nếu chỉ đọc tài liệu, các dịch vụ như Amplify, API Gateway, Elastic Beanstalk, RDS hay SES khá rời rạc. Nhưng khi đặt chúng vào một project cụ thể, vai trò của từng dịch vụ trở nên rõ ràng hơn.

Quan trọng hơn, quá trình viết workshop giúp em biết cách biến kinh nghiệm triển khai thành tài liệu. Đây là kỹ năng rất cần thiết khi làm việc trong môi trường cloud, vì mỗi bước cấu hình đều cần được ghi lại rõ ràng để người khác có thể kiểm tra, lặp lại hoặc cải thiện.

## 6. Định hướng sau thực tập

Sau kỳ thực tập, em mong muốn tiếp tục học sâu hơn về AWS theo các hướng:

- Thực hành triển khai hạ tầng bằng AWS CDK hoặc Terraform.
- Tìm hiểu kỹ hơn về VPC, private subnet, load balancer, security group và IAM policy.
- Bổ sung CloudWatch Logs, metrics và alarm cho backend.
- Tìm hiểu S3 upload, CloudFront, custom domain và HTTPS.
- Thực hành backup/restore database và tối ưu chi phí AWS cho môi trường demo.
- Tiếp tục hoàn thiện EAM Workspace theo hướng gần với production-ready hơn.

Nhìn chung, kỳ thực tập tại AWS giúp em có cái nhìn thực tế hơn về cloud computing. Em không chỉ học thêm dịch vụ AWS, mà còn hiểu cách kết hợp các dịch vụ đó để triển khai một hệ thống web hoàn chỉnh, có thể kiểm thử và có tài liệu hướng dẫn rõ ràng.
