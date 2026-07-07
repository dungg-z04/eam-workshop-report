---
title: "Các bài blog đã đăng"
date: 2026-06-25
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Phần này tổng hợp các bài blog kỹ thuật mình đã đọc và chia sẻ trong quá trình thực tập. Các chủ đề được chọn tập trung vào Amazon EKS, vận hành Kubernetes, bảo mật service mesh, private networking và ứng dụng AI trong cloud security trên AWS.

### [Blog 1 - Amazon EKS now supports control plane egress through your VPC](3.1-Blog1/)

Nguồn: [AWS Containers Blog - Amazon EKS now supports control plane egress through your VPC](https://aws.amazon.com/blogs/containers/amazon-eks-now-supports-control-plane-egress-through-your-vpc/)

Bài viết giới thiệu customer-routed control plane egress cho Amazon EKS. Tính năng này cho phép outbound traffic do Kubernetes API Server khởi tạo được định tuyến qua VPC của người dùng, giúp tăng khả năng kiểm soát mạng, audit và tuân thủ.

### [Blog 2 - Better Together: Amazon EKS Auto Mode and Istio Ambient Mesh](3.2-Blog2/)

Nguồn: [AWS Containers Blog - Better Together: Amazon EKS Auto Mode and Istio Ambient Mesh](https://aws.amazon.com/blogs/containers/better-together-amazon-eks-auto-mode-and-istio-ambient-mesh/)

Bài viết giải thích cách kết hợp Amazon EKS Auto Mode và Istio Ambient Mesh để giảm khối lượng vận hành Kubernetes, đồng thời tăng cường bảo mật giao tiếp giữa các microservices. EKS Auto Mode tự động hóa các tác vụ ở tầng compute, trong khi Istio Ambient Mesh cung cấp service mesh không cần sidecar.

### [Blog 3 - Introducing AWS Continuum: Security at machine speed](3.3-Blog3/)

Nguồn: [AWS Security Blog - Introducing AWS Continuum: Security at machine speed](https://aws.amazon.com/blogs/security/introducing-aws-continuum-security-at-machine-speed/)

Bài viết giới thiệu AWS Continuum, một hướng tiếp cận mới giúp đội ngũ bảo mật xử lý lỗ hổng mã nguồn nhanh hơn bằng AI. Nội dung tập trung vào vòng đời xử lý lỗ hổng gồm discovery, prioritization, validation, mitigation và remediation.

Mình chọn các chủ đề này vì chúng liên quan trực tiếp đến vận hành cloud-native, bảo mật networking trong Kubernetes, quản trị hạ tầng hiện đại và xu hướng Agentic AI trong cloud security trên AWS.
