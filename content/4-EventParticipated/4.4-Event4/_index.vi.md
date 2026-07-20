---
title: "Event 4: AWS Security, Monitoring and Cloud Practitioner Sharing"
date: 2026-07-11
weight: 4
chapter: false
pre: " <b> 4.4. </b> "
---

## Thông tin sự kiện

| Nội dung | Chi tiết |
| --- | --- |
| Thời gian | Ngày 11/07/2026 |
| Địa điểm | Tầng 26, tòa nhà Bitexco Financial Tower |
| Hình thức tham gia | Tham gia trực tiếp |
| Vai trò | Người tham dự |
| Chủ đề chính | AWS Security Agent, bảo mật ứng dụng web, SLA, monitoring, CloudWatch, SNS, AWS Cloud Practitioner và định hướng học chứng chỉ AWS |

## Tổng quan

Sự kiện **AWS Security, Monitoring and Cloud Practitioner Sharing** là một buổi chia sẻ kiến thức về bảo mật, giám sát hệ thống và định hướng học chứng chỉ AWS dành cho sinh viên và người mới tiếp cận cloud computing. Nội dung sự kiện gồm ba phần chính: bảo mật ứng dụng web với AWS Security Agent, tư duy giám sát hệ thống từ SLA đến trải nghiệm người dùng, và lộ trình ôn thi chứng chỉ AWS Certified Cloud Practitioner.

Buổi chia sẻ giúp em có cái nhìn toàn diện hơn về quá trình xây dựng, vận hành và bảo vệ một hệ thống trên nền tảng AWS. Một hệ thống cloud không chỉ cần triển khai được, mà còn cần được theo dõi đúng chỉ số, phát hiện sớm rủi ro bảo mật và có quy trình phản hồi khi phát sinh sự cố.

Đối với project EAM Workspace, nội dung sự kiện có giá trị thực tế vì hệ thống cũng cần quan tâm đến các vấn đề tương tự: bảo vệ ứng dụng web, theo dõi trạng thái backend, kiểm tra API health, giám sát lỗi đăng nhập, cấu hình cảnh báo và hiểu rõ các dịch vụ AWS đang sử dụng trong kiến trúc triển khai.

## Nội dung chính

### 1. Securing Your Web Apps With AWS Security Agent

Phần trình bày đầu tiên tập trung vào chủ đề bảo mật ứng dụng web với AWS Security Agent. Diễn giả bắt đầu bằng việc nêu ra một số hạn chế trong quy trình kiểm thử bảo mật truyền thống. Các hoạt động như penetration testing thủ công thường tốn nhiều thời gian, chi phí cao, phụ thuộc vào kinh nghiệm của chuyên gia kiểm thử và khó đảm bảo độ bao phủ đồng đều cho toàn bộ hệ thống.

Từ vấn đề đó, Security Agent được giới thiệu như một hướng tiếp cận mới trong bảo mật ứng dụng. Với sự hỗ trợ của Amazon Bedrock, agent có thể suy luận, lập kế hoạch và thực hiện một số tác vụ bảo mật như đánh giá thiết kế, rà soát mã nguồn, phát hiện secret bị lộ hoặc mô phỏng một số kịch bản tấn công trên ứng dụng đang chạy.

Một điểm quan trọng là Security Agent có thể hỗ trợ ở nhiều giai đoạn trong vòng đời phát triển phần mềm. Ở giai đoạn thiết kế, agent có thể phân tích tài liệu kiến trúc hoặc mã Infrastructure as Code để kiểm tra mức độ tuân thủ các tiêu chuẩn bảo mật. Ở giai đoạn phát triển, agent có thể tham gia vào Pull Request để gợi ý lỗi hoặc cảnh báo cấu hình không an toàn. Ở giai đoạn kiểm thử, agent có thể hỗ trợ automated pentesting và cung cấp bằng chứng để nhóm kỹ thuật xác minh.

Tuy nhiên, nội dung chia sẻ cũng nhấn mạnh rằng Security Agent không thay thế hoàn toàn con người. Công cụ này vẫn có giới hạn khi gặp các cơ chế xác thực phức tạp, lỗi logic nghiệp vụ cần ngữ cảnh sâu hoặc các hệ thống có phạm vi kiểm thử lớn. Vì vậy, khi áp dụng AI agent trong bảo mật, nhóm phát triển cần xác định rõ phạm vi kiểm thử, theo dõi chi phí và kết hợp với đánh giá của con người trong các quyết định quan trọng.

Qua phần này, em hiểu rõ hơn rằng bảo mật ứng dụng hiện đại nên được tích hợp sớm vào quy trình phát triển, thay vì chỉ kiểm thử ở cuối dự án. Cách tiếp cận này phù hợp với tư duy shift-left security và giúp giảm rủi ro trước khi hệ thống được đưa lên môi trường production.

### 2. SLA and Monitoring - From SLA to Monitoring What Really Matters

Phần trình bày thứ hai tập trung vào SLA và monitoring trong quá trình vận hành hệ thống. Diễn giả đưa ra một tình huống rất thực tế: AWS Console có thể hiển thị tài nguyên bình thường, server vẫn chạy, CPU và memory không có dấu hiệu bất thường, nhưng người dùng vẫn không thể đăng nhập vào ứng dụng. Điều này cho thấy monitoring không nên chỉ dừng lại ở hạ tầng, mà cần đo cả trải nghiệm thực tế của người dùng.

SLA, hay Service Level Agreement, được giải thích là cam kết về mức độ dịch vụ giữa nhà cung cấp và khách hàng. SLA giúp xác định kỳ vọng rõ ràng, tăng trách nhiệm của nhà cung cấp và hỗ trợ quản lý rủi ro. Tuy nhiên, SLA của AWS chủ yếu áp dụng cho dịch vụ cloud do AWS cung cấp, còn trải nghiệm cuối cùng của người dùng vẫn phụ thuộc vào cách ứng dụng được thiết kế, triển khai và vận hành.

Một mô hình đáng chú ý trong phần này là **Monitoring Pyramid**. Tầng thấp nhất là infrastructure metrics như CPU, memory, disk, network, trạng thái EC2, RDS hoặc ALB. Tầng tiếp theo là application metrics như latency, error rate và request count. Cao hơn nữa là business metrics như login success rate, số lượng giao dịch thành công hoặc số lượng yêu cầu thất bại. Tầng cao nhất là customer experience, tức là người dùng có thật sự đăng nhập, thao tác và hoàn thành luồng nghiệp vụ được hay không.

Phần demo minh họa cho thấy endpoint health check có thể trả về `200 OK`, ALB target vẫn healthy, nhưng endpoint login vẫn thất bại nếu backend không kết nối được database. Thông điệp quan trọng là healthy infrastructure không đồng nghĩa với happy user experience. Một dashboard toàn màu xanh chưa chắc phản ánh đúng hệ thống đang hoạt động tốt với người dùng cuối.

Diễn giả cũng trình bày luồng cảnh báo từ custom metric đến alert. Ví dụ, hệ thống có thể ghi nhận metric như `LoginFailure` hoặc `LoginSuccessRate`, sau đó tạo CloudWatch Alarm với ngưỡng cảnh báo phù hợp. Khi vượt ngưỡng, alarm có thể gửi thông báo qua Amazon SNS đến email hoặc kênh chat để đội kỹ thuật phản hồi sớm.

Qua phần này, em liên hệ trực tiếp với EAM Workspace. Khi triển khai project lên AWS, việc kiểm tra `/api/health` là cần thiết nhưng chưa đủ. Hệ thống còn cần kiểm tra các luồng quan trọng như đăng nhập, tải danh sách tài sản, bàn giao tài sản, gửi yêu cầu hỗ trợ và gửi email OTP. Đây mới là các chỉ số phản ánh gần hơn trải nghiệm thật của người dùng.

### 3. Inside The Exam: AWS Cloud Practitioner

Phần trình bày thứ ba tập trung vào chứng chỉ **AWS Certified Cloud Practitioner**, một chứng chỉ nền tảng dành cho người mới bắt đầu học AWS. Diễn giả giới thiệu cấu trúc bài thi, các nhóm kiến thức chính và cách học phù hợp để không bị rối trước số lượng dịch vụ AWS rất lớn.

Bài thi AWS Certified Cloud Practitioner gồm 65 câu hỏi, thời gian làm bài 90 phút và điểm đạt là 700 trên thang điểm 1000. Chứng chỉ có hiệu lực trong 3 năm. Nội dung thi tập trung vào các khái niệm cloud, mô hình trách nhiệm chia sẻ, bảo mật, các dịch vụ AWS cốt lõi, billing, pricing và support.

Các domain chính của bài thi gồm:

- **Cloud Concepts**: khái niệm cloud, lợi ích của AWS Cloud và các mô hình triển khai.
- **Security and Compliance**: Shared Responsibility Model, IAM, security group, network ACL, AWS Shield, AWS WAF và AWS Artifact.
- **Cloud Technology and Services**: compute, storage, database, networking và các dịch vụ như EC2, Lambda, S3, RDS, DynamoDB, VPC, Route 53.
- **Billing, Pricing and Support**: Cost Explorer, AWS Budgets, pricing model và các gói AWS Support.

Một kinh nghiệm hữu ích là học AWS theo keyword và use case. Khi học một dịch vụ, người học nên gắn dịch vụ đó với tình huống sử dụng cụ thể. Ví dụ, khi gặp bài toán decouple microservices có thể nghĩ đến Amazon SQS; khi cần quản lý chi phí có thể liên hệ đến Cost Explorer hoặc AWS Budgets; khi cần database quan hệ có thể nghĩ đến Amazon RDS.

Diễn giả cũng nhấn mạnh việc review câu sai khi làm mock exam. Làm nhiều đề không quan trọng bằng việc hiểu vì sao một đáp án đúng và vì sao các đáp án còn lại sai. Ngoài ra, người học nên thực hành trên AWS Free Tier với các dịch vụ cơ bản như EC2, S3, IAM hoặc RDS để kiến thức lý thuyết trở nên dễ hiểu hơn.

Qua phần này, em hiểu rõ hơn vai trò của AWS Cloud Practitioner trong lộ trình học cloud. Đây là bước khởi đầu phù hợp để hệ thống hóa kiến thức nền tảng trước khi học sâu hơn về Solutions Architect, Developer hoặc SysOps Administrator.

## Kiến thức rút ra

- Bảo mật ứng dụng web cần được tích hợp vào toàn bộ vòng đời phát triển phần mềm, từ thiết kế, viết code đến kiểm thử ứng dụng đang chạy.
- AI agent có thể hỗ trợ design review, code review và penetration testing, nhưng vẫn cần con người kiểm soát phạm vi, chi phí và quyết định cuối cùng.
- Monitoring không chỉ là theo dõi CPU, memory hoặc trạng thái server, mà cần đo cả trải nghiệm thực tế của người dùng.
- Healthy infrastructure không đồng nghĩa với happy user experience; hệ thống cần có các chỉ số gần với nghiệp vụ như login success rate, error rate hoặc OTP success rate.
- CloudWatch, custom metrics, CloudWatch Alarm và SNS có thể kết hợp để xây dựng luồng cảnh báo sớm cho các vấn đề ảnh hưởng đến người dùng.
- AWS Cloud Practitioner là chứng chỉ nền tảng phù hợp để hệ thống hóa kiến thức AWS trước khi học các chứng chỉ chuyên sâu hơn.
- Khi học AWS, cần gắn mỗi dịch vụ với use case thực tế để dễ hiểu, dễ nhớ và dễ áp dụng vào project.

## Kết luận

Sự kiện AWS Security, Monitoring and Cloud Practitioner Sharing mang lại cho em nhiều kiến thức hữu ích về bảo mật ứng dụng web, giám sát hệ thống và định hướng học chứng chỉ AWS. Ba phần trình bày bổ trợ cho nhau, giúp em hiểu rằng một hệ thống cloud hiệu quả không chỉ cần triển khai thành công, mà còn cần được bảo mật tốt, giám sát đúng chỉ số và vận hành dựa trên trải nghiệm người dùng.

Những kiến thức này có thể áp dụng trực tiếp vào project EAM Workspace, đặc biệt ở các phần kiểm tra API health, theo dõi lỗi đăng nhập, cấu hình cảnh báo, bảo vệ ứng dụng web và hiểu rõ hơn vai trò của các dịch vụ AWS trong kiến trúc triển khai.

## Hình ảnh sự kiện

Một số hình ảnh được ghi lại trong quá trình tham gia sự kiện:

<div class="event-gallery event-gallery-compact">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526237_64486502297271719_8743030703712121879_f013b97836efa82730a725e22d470514.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526320_64486502297271719_8743030703712121879_b294dc252bc3541b272e973dd6a59c9f.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526349_64486502297271719_8743030703712121879_93c10150d149f5b0b3fe189ca88a9bf4.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526441_64486502297271719_8743030703712121879_1c55ea8f67e8b9373d603e8bdbee1a42.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526559_64486502297271719_8743030703712121879_d54d53cee3548cb6e264a2e0cfa016be.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526599_64486502297271719_8743030703712121879_290eb3a4e9e1b8040a7ff79de5a858f4.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
  <img src="/eam-workshop-report/images/4-EventParticipated/4.4-Event4/1784259526617_64486502297271719_8743030703712121879_12bc9fb98e59012a5daab6aab04adb17.jpg" alt="AWS Security, Monitoring and Cloud Practitioner Sharing">
</div>
