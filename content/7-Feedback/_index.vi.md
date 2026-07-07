---
title: "Chia sẻ và góp ý"
date: 2026-07-06
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

## 1. Đánh giá chung

### 1.1. Môi trường thực tập

Chương trình tạo cho em một môi trường học tập khá chuyên nghiệp và có định hướng rõ ràng. Thay vì chỉ học lý thuyết về cloud, em được yêu cầu ghi lại worklog, đọc tài liệu AWS, tham gia event, tìm hiểu AWS Blog, triển khai project thật và trình bày lại quy trình theo dạng workshop.

Cách tổ chức này giúp em hiểu rằng khi làm việc với cloud, việc biết tên dịch vụ là chưa đủ. Người học cần hiểu dịch vụ đó giải quyết vấn đề gì, nằm ở đâu trong kiến trúc, cấu hình như thế nào và kiểm tra kết quả ra sao.

### 1.2. Sự hỗ trợ của mentor và team

Trong quá trình thực tập, em nhận được sự hỗ trợ cần thiết từ mentor và team admin. Mentor giúp em định hướng cách chia nội dung báo cáo, cách trình bày kiến trúc AWS, cách viết workshop, cách vẽ kiến trúc project sao cho hợp lý, giúp em và các bạn nhận ra các lỗi sai mà mình mắc phải.


### 1.3. Mức độ phù hợp với chuyên ngành

Chương trình phù hợp với chuyên ngành Công nghệ thông tin vì các nội dung thực tập gắn trực tiếp với phát triển và triển khai ứng dụng web. Thông qua project EAM Workspace, em được tiếp cận các phần như frontend, backend, cơ sở dữ liệu, xác thực, email OTP, API, cloud hosting và monitoring.

Trước đây, khi chạy project local, em chủ yếu quan tâm ứng dụng có chạy được trên máy hay không. Sau khi triển khai lên AWS, em hiểu thêm rằng một hệ thống hoàn chỉnh cần có nhiều lớp khác nhau: hạ tầng mạng, compute, database, API gateway, email service, monitoring, bảo mật và kiểm soát chi phí.

### 1.4. Cơ hội học hỏi và phát triển kỹ năng

Trong chương trình, em có cơ hội tìm hiểu và thực hành nhiều dịch vụ AWS quan trọng, bao gồm:

- **IAM** để hiểu về tài khoản, quyền truy cập và credential.
- **VPC, subnet và Security Group** để hiểu cách kiểm soát kết nối mạng.
- **Amazon RDS** để triển khai cơ sở dữ liệu MySQL cho backend.
- **Elastic Beanstalk** để triển khai backend Node.js.
- **API Gateway** để tạo lớp trung gian cho frontend gọi backend.
- **AWS Amplify Hosting** để triển khai frontend.
- **Amazon SES/SMTP** để gửi email OTP.
- **CloudWatch** để theo dõi trạng thái và hỗ trợ kiểm tra lỗi.
- **Billing and Cost Management** để theo dõi chi phí phát sinh.

Ngoài kỹ năng kỹ thuật, em cũng rèn luyện thêm kỹ năng viết tài liệu, trình bày quy trình, mô tả kiến trúc, chụp ảnh minh họa và giải thích kết quả thực hành. Đây là những kỹ năng quan trọng khi làm việc với project thật.

### 1.5. Văn hóa học tập và tinh thần cộng đồng

Một điểm em đánh giá cao là chương trình không chỉ yêu cầu làm project, mà còn khuyến khích sinh viên đọc blog, tham gia event và chia sẻ nội dung đã học. Việc tiếp cận AWS Blog và các buổi chia sẻ giúp em nhìn AWS ở phạm vi rộng hơn, không chỉ dừng lại ở việc deploy một web app.

Các chủ đề như Amazon EKS, Istio Ambient Mesh, security automation, AI và cloud operations giúp em hiểu rằng AWS là một hệ sinh thái lớn, được sử dụng trong nhiều bài toán thực tế khác nhau. Điều này tạo động lực để em tiếp tục học sâu hơn sau kỳ thực tập.

## 2. Một số cảm nhận cá nhân

### 2.1. Điều em hài lòng nhất

Điều em hài lòng nhất là sau chương trình, em có thể nhìn project theo góc độ triển khai thực tế hơn. EAM Workspace không chỉ là một ứng dụng web chạy local, mà đã được đưa lên AWS với mô hình:

**Amplify Hosting -> API Gateway -> Elastic Beanstalk -> Amazon RDS**

Kèm theo đó là **Amazon SES** cho email OTP và các bước kiểm tra health endpoint để xác nhận hệ thống hoạt động. Quá trình này giúp em hiểu rõ hơn vai trò của từng dịch vụ AWS trong một kiến trúc ứng dụng full-stack.

### 2.2. Điều em thấy còn khó khăn

Khó khăn lớn nhất của em là ban đầu có quá nhiều phần cần xử lý cùng lúc. Khi deploy lên AWS, lỗi có thể đến từ code, biến môi trường, security group, endpoint, rewrite rule, SES credential hoặc cấu hình database. Nếu chưa quen, rất dễ kiểm tra sai hướng.

Ngoài ra, việc viết báo cáo theo dạng workshop cũng mất nhiều thời gian hơn em nghĩ. Mỗi bước không chỉ cần làm được, mà còn phải chụp ảnh đúng, mô tả rõ mục đích, giải thích kết quả và đảm bảo người khác có thể đọc lại quy trình.

### 2.3. Có nên giới thiệu chương trình cho bạn bè không?

Em sẽ giới thiệu chương trình này cho các bạn muốn bắt đầu học AWS hoặc muốn hiểu cách triển khai một project web lên cloud. Chương trình phù hợp với những bạn đã có nền tảng lập trình cơ bản và muốn bước sang phần triển khai, vận hành, kiểm tra lỗi và viết tài liệu kỹ thuật.

Tuy nhiên, để học hiệu quả, người tham gia cần chủ động đọc tài liệu, tự thực hành và ghi chú lại lỗi gặp phải. AWS có nhiều dịch vụ và khái niệm mới, nên nếu chỉ làm theo từng bước mà không hiểu mục đích thì sẽ khó áp dụng lại cho project khác.

## 3. Mong muốn sau chương trình

Sau kỳ thực tập, em muốn tiếp tục học AWS theo hướng thực hành nhiều hơn. Một số chủ đề em muốn tìm hiểu tiếp gồm:

- Infrastructure as Code với AWS CDK, CloudFormation hoặc Terraform.
- VPC nâng cao, private subnet, NAT Gateway và VPC Endpoint.
- CloudWatch Logs, metrics, alarms và dashboard.
- S3, CloudFront, custom domain và HTTPS.
- IAM policy, Secrets Manager và best practices về bảo mật.
- Tối ưu chi phí AWS cho môi trường demo và production nhỏ.
- Container và Kubernetes trên AWS, đặc biệt là Amazon EKS.

Nhìn chung, First Cloud AI Journey là một chương trình hữu ích đối với sinh viên muốn bắt đầu với AWS. Chương trình giúp em hiểu rằng cloud không chỉ là nơi deploy ứng dụng, mà còn là nền tảng để thiết kế, vận hành, giám sát và cải thiện hệ thống một cách chuyên nghiệp hơn.
