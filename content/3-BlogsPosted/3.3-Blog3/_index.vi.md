---
title: "Blog 3"
date: 2026-06-25
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# AWS Continuum: Bảo mật ở tốc độ máy

**Nguồn:** [AWS Security Blog - Introducing AWS Continuum: Security at machine speed](https://aws.amazon.com/vi/blogs/security/introducing-aws-continuum-security-at-machine-speed/)

Bài blog giới thiệu AWS Continuum, một hướng tiếp cận mới của AWS nhằm hỗ trợ các đội ngũ bảo mật xử lý lỗ hổng mã nguồn ở tốc độ máy. Thay vì chỉ thu thập telemetry, lưu trữ, truy vấn và xây dựng dashboard để theo dõi, AWS nhấn mạnh mô hình mới gồm telemetry, context, reasoning và actions.

AWS Continuum for code vulnerabilities hiện được công bố ở dạng gated preview, tập trung vào toàn bộ vòng đời của lỗ hổng: từ phát hiện, ưu tiên, xác thực cho đến đề xuất giảm thiểu và khắc phục. Điểm đáng chú ý là hệ thống có thể kết hợp nhiều mô hình AI khác nhau, phân tích bối cảnh doanh nghiệp và đưa ra khuyến nghị có cơ sở thay vì áp dụng một bộ quy tắc chung cho mọi môi trường.

## Các điểm chính cần nắm

- AWS Continuum for code vulnerabilities được AWS công bố ở dạng gated preview, hướng đến việc xử lý vòng đời lỗ hổng mã nguồn từ discovery đến action.
- Continuum không chỉ phát hiện lỗ hổng mà còn phân tích bối cảnh thực tế của môi trường như hạ tầng AWS, quyền truy cập, network topology, mã nguồn, tài liệu nội bộ, quy trình vận hành và mức độ rủi ro của tổ chức.
- Quy trình hoạt động gồm 4 giai đoạn liên tục: Discovery, Prioritization, Validation, Mitigation and Remediation.
- Ở giai đoạn Discovery, hệ thống tiếp nhận backlog lỗ hổng hiện có và có thể thực hiện quét môi trường để tạo cái nhìn toàn diện hơn về các lỗ hổng cùng đường tấn công liên quan.
- Ở giai đoạn Prioritization, Continuum đánh giá mức độ quan trọng dựa trên câu hỏi như thành phần có đang được triển khai hay không, có thể truy cập được không, có nằm trên luồng production không và tác động kinh doanh nếu bị khai thác là gì.
- Ở giai đoạn Validation, hệ thống giúp giảm false positives bằng cách xác thực lỗ hổng theo bối cảnh môi trường và có thể tạo ví dụ khai thác trong môi trường sandbox để cung cấp bằng chứng có thể tái lập.
- Ở giai đoạn Mitigation and Remediation, Continuum đề xuất các biện pháp như thay đổi network, điều chỉnh policy hoặc tạo code patch; đồng thời xem xét blast radius và rollback path khi khả thi.
- Cách tiếp cận của AWS Continuum theo hướng "graduated trust": ban đầu chạy ở learn mode với human-in-the-loop, sau đó có thể chuyển dần sang enforce mode khi tổ chức đã đủ tin tưởng vào các khuyến nghị.
- Ngoài code vulnerabilities, AWS cũng đưa các khả năng như Continuum pen testing, Continuum code scanning và Continuum threat modeling vào cùng vòng lặp bảo mật.
- Tính năng này đặc biệt hữu ích với các tổ chức có số lượng lỗ hổng lớn, nhiều hệ thống phức tạp và cần ưu tiên xử lý theo rủi ro thực tế thay vì chỉ dựa trên mức độ nghiêm trọng chung.

## Hình ảnh

Hình minh họa vòng lặp hoạt động của AWS Continuum, dựa trên các giai đoạn Discovery, Prioritization, Validation, Mitigation and Remediation được mô tả trong bài blog.

![Sơ đồ minh họa vòng đời xử lý lỗ hổng của AWS Continuum](/eam-workshop-report/images/3-BlogsPosted/3.3-Blog3/aws-continuum-1.png)

*Hình 1. Sơ đồ minh họa vòng đời xử lý lỗ hổng của AWS Continuum. Nguồn nội dung: AWS Security Blog.*


## Hướng dẫn

1. Đọc phần "What we believe" để hiểu vì sao mô hình bảo mật truyền thống dựa nhiều vào telemetry và dashboard không còn đủ nhanh trước tốc độ phát hiện lỗ hổng bằng AI.
2. Ghi nhớ 4 giai đoạn chính của AWS Continuum: Discovery, Prioritization, Validation, Mitigation and Remediation.
3. Khi phân tích một hệ thống thực tế, có thể liên hệ bài blog với các nguồn dữ liệu như code repository, IAM permissions, network topology, tài liệu thiết kế hệ thống và mức độ quan trọng của workload.
4. AWS Continuum như một ví dụ về xu hướng Agentic AI trong bảo mật: AI không chỉ phát hiện vấn đề mà còn hỗ trợ suy luận, ưu tiên và đề xuất hành động khắc phục.
5. Do AWS Continuum for code vulnerabilities đang ở dạng gated preview, phần thực hành có thể dừng ở mức tìm hiểu kiến trúc, quy trình vận hành và đăng ký request access nếu tổ chức có nhu cầu trải nghiệm.

## Kết luận ngắn

AWS Continuum thể hiện định hướng mới trong lĩnh vực cloud security, nơi AI được sử dụng để tăng tốc quá trình phát hiện, đánh giá và khắc phục lỗ hổng. Thay vì chỉ cung cấp thông tin cho con người quan sát, hệ thống hướng đến việc tạo ra các hành động có căn cứ, có thể kiểm chứng và từng bước tự động hóa dưới sự kiểm soát của đội ngũ bảo mật.

<figure class="blog-group-post">
  <img src="/eam-workshop-report/images/3-BlogsPosted/3.3-Blog3/z8015011261961_733583f041bf45f21cbc876601b453b1.jpg" alt="Bài đăng blog 3 trên group AWS">
  <figcaption>Bài đăng đã chia sẻ trong group AWS.</figcaption>
</figure>
