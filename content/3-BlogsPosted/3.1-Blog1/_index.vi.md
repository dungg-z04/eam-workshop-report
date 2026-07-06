---
title: "Blog 1"
date: 2026-06-25
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Amazon EKS now supports control plane egress through your VPC

**Nguồn:** [Amazon EKS now supports control plane egress through your VPC](https://aws.amazon.com/blogs/containers/amazon-eks-now-supports-control-plane-egress-through-your-vpc/)

Amazon EKS đã bổ sung khả năng customer-routed control plane egress, cho phép định tuyến một số lưu lượng outbound từ Kubernetes API Server đi qua chính Amazon VPC của người dùng. Tính năng này giúp doanh nghiệp kiểm soát tốt hơn đường đi của các request do control plane khởi tạo, chẳng hạn như admission webhook callback, truy vấn OIDC provider và aggregate API server request.

Thay vì để các luồng này đi theo đường mạng do EKS quản lý, người dùng có thể áp dụng các cơ chế kiểm soát quen thuộc trong VPC như route table, security group, VPC endpoint, AWS PrivateLink, NAT Gateway hoặc AWS Network Firewall. Đây là cải tiến quan trọng đối với các hệ thống Kubernetes yêu cầu bảo mật cao, đặc biệt trong môi trường doanh nghiệp, tài chính, y tế hoặc các tổ chức có yêu cầu tuân thủ nghiêm ngặt.


## Các điểm chính cần nắm

- Customer-routed control plane egress cho phép các luồng outbound "customer-controllable" từ Kubernetes API Server đi qua Elastic Network Interface (ENI) nằm trong VPC của người dùng.
- Các loại lưu lượng được hỗ trợ bao gồm admission webhook callback, truy vấn tài liệu khám phá OIDC, yêu cầu đến aggregate API server và DNS resolution phục vụ cho các luồng này.
- Khi bật tính năng này, người dùng có thể áp dụng route table, security group, endpoint policy, NAT Gateway, AWS PrivateLink, VPC endpoint, AWS Network Firewall và các quy tắc egress control sẵn có trong VPC.
- Tính năng đặc biệt hữu ích cho các hệ thống cần private networking, private OIDC provider hoặc admission webhook chỉ có thể truy cập bên trong mạng riêng.
- Control plane egress qua VPC khác với EKS private endpoint: private endpoint kiểm soát chiều inbound đến Kubernetes API Server, còn customer-routed egress kiểm soát chiều outbound từ API Server ra các dịch vụ liên quan.
- Người dùng có thể bật khi tạo cluster mới hoặc cập nhật cluster hiện có bằng cách đặt `controlPlaneEgressMode = CUSTOMER_ROUTED` trong `resourcesVpcConfig`.
- Sau khi cluster chuyển sang `CUSTOMER_ROUTED`, thiết lập này là cố định trong suốt vòng đời cluster và không thể chuyển ngược về `AWS_MANAGED`.
- Có thể dùng IAM condition key `eks:controlPlaneEgressMode` kết hợp với AWS Organizations Service Control Policies để bắt buộc các cluster trong tổ chức phải sử dụng chế độ `CUSTOMER_ROUTED`.
- VPC Flow Logs có thể được sử dụng để quan sát và xác minh các kết nối từ EKS-managed cross-account ENI đến các endpoint nội bộ, hỗ trợ kiểm toán và tuân thủ.
- Một số luồng không thuộc Kubernetes API Server, ví dụ EKS Capabilities hoặc AWS STS call từ IAM Authenticator, vẫn tiếp tục đi theo đường EKS-managed và không đi qua VPC của người dùng.

## Hình ảnh

Hình minh họa kiến trúc khi Private Control Plane Networking được bật. Lưu lượng customer-controllable từ `kube-apiserver` đi qua ENI trong VPC của người dùng, sau đó chịu sự kiểm soát bởi các thành phần mạng như VPC endpoint, NAT Gateway, Transit Gateway hoặc AWS PrivateLink trước khi đi đến customer destinations.

![Control plane egress đi qua VPC của người dùng khi bật Private Control Plane Networking](/eam-workshop-report/images/3-BlogsPosted/3.2-Blog2/CONTAINERS-269-1.png)

*Hình 1. Control plane egress đi qua VPC của người dùng khi bật Private Control Plane Networking. Nguồn: AWS Blog.*


## Hướng dẫn

Để tìm hiểu và áp dụng tính năng này, có thể thực hiện theo các bước chính sau:

1. Xác định cluster EKS cần sử dụng private control plane networking và kiểm tra các subnet, security group, route table, DNS resolver trong VPC.
2. Khi tạo cluster mới, cấu hình `resources-vpc-config` và thêm `controlPlaneEgressMode=CUSTOMER_ROUTED` để bật định tuyến egress qua VPC.
3. Với cluster hiện có, sử dụng lệnh `update-cluster-config` để chuyển sang chế độ `CUSTOMER_ROUTED`, đồng thời lưu ý rằng thiết lập này không thể quay lại `AWS_MANAGED`.
4. Đảm bảo các endpoint mà Kubernetes API Server cần gọi, chẳng hạn admission webhook, OIDC provider hoặc aggregate API server, có thể truy cập được từ subnet của cluster thông qua private DNS, internal load balancer, VPC endpoint hoặc PrivateLink.
5. Kiểm tra security group, route table và NAT/PrivateLink path để tránh trường hợp API Server không gọi được webhook hoặc OIDC endpoint.
6. Sử dụng `aws eks describe-cluster` để xác minh giá trị `controlPlaneEgressMode` và bật VPC Flow Logs để theo dõi đường đi của lưu lượng phục vụ kiểm toán.
7. Nếu quản lý nhiều tài khoản AWS, có thể dùng AWS Organizations SCP với condition key `eks:controlPlaneEgressMode` để yêu cầu các cluster phải bật `CUSTOMER_ROUTED` theo chuẩn bảo mật của tổ chức.

### Ví dụ lệnh AWS CLI tham khảo

```bash
# Tạo cluster mới với customer-routed control plane egress
aws eks create-cluster \
  --name my-cluster \
  --kubernetes-version 1.36 \
  --role-arn arn:aws:iam::111122223333:role/eks-cluster-role \
  --resources-vpc-config subnetIds=subnet-aaa,subnet-bbb,securityGroupIds=sg-xxx,controlPlaneEgressMode=CUSTOMER_ROUTED

# Bật trên cluster hiện có
aws eks update-cluster-config \
  --name my-cluster \
  --resources-vpc-config controlPlaneEgressMode=CUSTOMER_ROUTED

# Kiểm tra cấu hình
aws eks describe-cluster --name my-cluster \
  --query "cluster.resourcesVpcConfig.controlPlaneEgressMode"
```

## Kết luận 

Tính năng customer-routed control plane egress giúp Amazon EKS phù hợp hơn với các môi trường yêu cầu kiểm soát mạng nghiêm ngặt. Thay vì chỉ quản lý lưu lượng của worker nodes và workloads, người dùng có thêm khả năng kiểm soát một phần lưu lượng outbound từ Kubernetes API Server. Điều này giúp tăng tính riêng tư, hỗ trợ kiểm toán, giảm rủi ro khi sử dụng webhook hoặc OIDC provider nội bộ và giúp triển khai EKS trong các hệ thống doanh nghiệp có yêu cầu bảo mật cao.
