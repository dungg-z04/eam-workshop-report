---
title: "Chia sẻ và góp ý"
date: 2026-07-05
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

# Chia sẻ và góp ý

Sau thời gian tham gia chương trình **Workforce Bootcamp - First Cloud AI Journey** tại AWS, em có cơ hội tiếp cận cloud theo cách thực tế hơn. Trước đây, em chủ yếu biết AWS qua khái niệm hoặc tài liệu rời rạc; sau chương trình, em hiểu rõ hơn cách các dịch vụ AWS có thể kết hợp với nhau để triển khai một ứng dụng web hoàn chỉnh.

Điểm em đánh giá cao nhất là chương trình không chỉ yêu cầu học lý thuyết, mà còn gắn việc học AWS với project, blog, event, workshop và báo cáo cá nhân. Nhờ vậy, quá trình học có mục tiêu rõ ràng hơn: học dịch vụ nào, dùng trong phần nào của project, kiểm tra kết quả ra sao và ghi lại quy trình như thế nào.

## 1. Đánh giá chung về chương trình

Chương trình First Cloud AI Journey giúp em có một lộ trình làm quen AWS khá đầy đủ, bắt đầu từ các kiến thức nền tảng như AWS account, IAM, networking, compute, database, storage, monitoring và chi phí. Sau đó, các kiến thức này được áp dụng vào project EAM Workspace thông qua quá trình triển khai frontend, backend, API Gateway, database và email service.

Điểm nổi bật của chương trình là cách học không tách rời thực tế. Khi triển khai project, em phải hiểu:

- Vì sao frontend cần được host bằng AWS Amplify.
- Vì sao backend cần môi trường chạy ổn định như Elastic Beanstalk.
- Vì sao API Gateway cần đứng giữa frontend và backend.
- Vì sao database cần được quản lý bằng Amazon RDS.
- Vì sao email OTP cần SES/SMTP và credential riêng.
- Vì sao CloudWatch/logging cần thiết khi kiểm tra lỗi triển khai.

Nhờ đó, em không chỉ nhớ tên dịch vụ AWS, mà còn hiểu vai trò của từng dịch vụ trong một kiến trúc cụ thể.

## 2. Trải nghiệm học AWS

Trong quá trình tham gia chương trình, em thấy việc học AWS hiệu quả hơn khi đi theo từng chủ đề nhỏ và có thực hành kèm theo. Ví dụ, khi học IAM, em hiểu hơn về phân quyền; khi học VPC và Security Group, em hiểu hơn về network; khi học RDS, em hiểu hơn về database endpoint và connection string; khi học Elastic Beanstalk và Amplify, em hiểu rõ hơn quy trình deploy ứng dụng.

Việc đọc tài liệu từ Cloud Journey, AWS Blog và các nội dung chia sẻ trong event giúp em nhìn AWS ở nhiều góc độ hơn. AWS không chỉ phục vụ deploy web app, mà còn liên quan đến security, AI/ML, container, data analytics, automation và vận hành hệ thống ở quy mô lớn.

Điều này giúp em có động lực học tiếp vì em thấy AWS là một mảng rộng, có nhiều hướng phát triển sau kỳ thực tập.

## 3. Trải nghiệm triển khai project lên AWS

Phần triển khai EAM Workspace lên AWS là phần giúp em học được nhiều nhất. Khi làm local, em chỉ cần quan tâm ứng dụng chạy được trên máy. Nhưng khi đưa lên AWS, em phải quan tâm thêm đến nhiều lớp khác:

- Frontend build có đúng output directory không.
- Amplify rewrite có chuyển `/api/*` đúng về API Gateway không.
- API Gateway có trỏ đúng backend Elastic Beanstalk không.
- Backend có đọc đúng biến môi trường không.
- RDS có cho phép backend kết nối không.
- SES credential có đúng SMTP username/password không.
- Health endpoint có trả về kết quả đúng không.

Những vấn đề này giúp em hiểu rõ hơn sự khác biệt giữa lập trình ứng dụng và triển khai ứng dụng. Một project hoàn chỉnh cần cả code, cấu hình, cloud service, kiểm thử và tài liệu hướng dẫn.

## 4. Sự hỗ trợ từ mentor và chương trình

Em đánh giá cao sự hỗ trợ từ mentor trong quá trình làm báo cáo và triển khai. Mentor giúp định hướng cách chia nội dung, cách mô tả kiến trúc, cách viết workshop, cách ghi chú ảnh minh họa và cách kiểm tra các phần AWS đã cấu hình.

Một điểm hữu ích là mentor thường hướng dẫn em tự kiểm tra lại vấn đề thay vì chỉ đưa ra đáp án. Khi gặp lỗi deploy, lỗi environment variables, lỗi SES/SMTP hoặc lỗi API endpoint, cách tiếp cận này giúp em tập kiểm tra từng lớp của hệ thống và hiểu nguyên nhân rõ hơn.

Chương trình cũng tạo cơ hội để em tham gia event và đọc blog kỹ thuật. Đây là phần giúp em mở rộng kiến thức ngoài project, đặc biệt là các chủ đề như EKS, service mesh, security automation, AI và cách AWS được dùng trong các bài toán thực tế.

## 5. Điều em hài lòng nhất

Điều em hài lòng nhất là sau chương trình, em không chỉ có một project nhóm mà còn có một báo cáo cá nhân hoàn chỉnh theo format workshop. Báo cáo này ghi lại quá trình học AWS, làm project, triển khai cloud, đọc blog, tham gia event và tự đánh giá.

Em cũng hài lòng vì đã hiểu rõ hơn cách một ứng dụng web có thể được triển khai trên AWS theo mô hình:

**Amplify Hosting -> API Gateway -> Elastic Beanstalk -> RDS**, kết hợp thêm **SES** cho email và **CloudWatch** cho kiểm tra vận hành.

Đây là kiến thức rất thực tế vì có thể áp dụng cho nhiều project web khác sau này.

## 6. Khó khăn trong quá trình tham gia

Một số khó khăn em gặp phải gồm:

- Ban đầu chưa quen với cách tổ chức báo cáo theo Hugo workshop.
- Chưa quen với việc phải viết song song worklog, proposal, blog, event, workshop và self-evaluation.
- Khi triển khai AWS, có nhiều phần cần kiểm tra cùng lúc như endpoint, rewrite rule, environment variables, RDS connection và SES credential.
- Một số lỗi không nằm ở code mà nằm ở cấu hình dịch vụ AWS, nên cần thời gian để xác định đúng nguyên nhân.
- Việc chụp ảnh workshop và viết mô tả cho từng ảnh mất nhiều thời gian hơn dự kiến.

Tuy vậy, những khó khăn này giúp em học được cách làm việc cẩn thận hơn. Khi triển khai cloud, mỗi bước cấu hình đều cần được ghi lại rõ ràng để sau này có thể kiểm tra hoặc làm lại.

## 7. Góp ý cho chương trình

Em nghĩ chương trình sẽ hỗ trợ sinh viên tốt hơn nếu bổ sung thêm một số nội dung sau:

- Có checklist AWS deployment mẫu cho project web full-stack, gồm frontend, backend, database, API Gateway, email và monitoring.
- Có buổi hướng dẫn riêng về cách đọc log và debug lỗi trên AWS, đặc biệt là CloudWatch, Elastic Beanstalk health và API Gateway.
- Có template workshop mẫu cho phần deploy AWS để sinh viên dễ hình dung cần viết gì, chụp ảnh gì và giải thích ra sao.
- Có hướng dẫn ngắn về cách quản lý biến môi trường, secrets và credential an toàn khi triển khai project.
- Có thêm bài thực hành nhỏ về IAM, VPC, RDS và Elastic Beanstalk trước khi sinh viên deploy project thật.
- Có checklist dọn dẹp tài nguyên AWS để tránh phát sinh chi phí sau khi hoàn thành báo cáo.

Những nội dung này sẽ giúp sinh viên tự tin hơn khi triển khai project và giảm thời gian xử lý các lỗi cấu hình cơ bản.

## 8. Mong muốn sau chương trình

Sau chương trình, em mong muốn tiếp tục học AWS theo hướng thực hành nhiều hơn. Các chủ đề em muốn tìm hiểu tiếp gồm:

- AWS CDK hoặc Terraform để triển khai hạ tầng bằng code.
- VPC nâng cao, private subnet, NAT Gateway và VPC Endpoint.
- CloudWatch Logs, metrics, alarm và dashboard.
- S3, CloudFront, custom domain và HTTPS.
- IAM policy, Secrets Manager và best practices về bảo mật.
- Tối ưu chi phí AWS cho môi trường demo và production nhỏ.

Nhìn chung, First Cloud AI Journey là một chương trình hữu ích cho sinh viên muốn bắt đầu với AWS. Chương trình giúp em hiểu rằng cloud không chỉ là nơi deploy ứng dụng, mà còn là nền tảng để thiết kế, vận hành, giám sát và cải thiện hệ thống một cách chuyên nghiệp hơn.
