---
title: "Blog 2"
date: 2026-06-25
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---
# Amazon EKS Auto Mode và Istio Ambient Mesh

**Nguồn:** [AWS Containers Blog - Better Together: Amazon EKS Auto Mode and Istio Ambient Mesh](https://aws.amazon.com/blogs/containers/better-together-amazon-eks-auto-mode-and-istio-ambient-mesh/)

## Amazon EKS Auto Mode và Istio Ambient Mesh

Bài blog giới thiệu cách kết hợp Amazon EKS Auto Mode với Istio Ambient Mesh nhằm giảm gánh nặng vận hành Kubernetes và service mesh trong môi trường cloud-native. EKS Auto Mode hỗ trợ tự động hóa nhiều thành phần vận hành của cluster, trong khi Istio Ambient Mesh cung cấp khả năng bảo mật, quan sát và kiểm soát lưu lượng mà không cần triển khai sidecar proxy cho từng pod.

Điểm nổi bật của bài viết là mô hình này cho phép doanh nghiệp triển khai service mesh theo hướng nhẹ hơn, dễ mở rộng hơn và phù hợp với các hệ thống microservices trên Amazon EKS. Thay vì phải quản lý nhiều node, sidecar và cấu hình phức tạp, đội ngũ vận hành có thể tận dụng EKS Auto Mode kết hợp ambient mode để tập trung vào ứng dụng và chính sách bảo mật.

## Các điểm chính cần nắm

- EKS Auto Mode tự động hóa nhiều công việc vận hành cluster như node provisioning, autoscaling, patching và quản lý hạ tầng, giúp giảm operational overhead cho đội ngũ DevOps.
- Các node trong EKS Auto Mode chạy trên EC2 managed instances, sử dụng hệ điều hành container-optimized và được AWS quản lý nhiều phần nền tảng, giúp việc vận hành cluster ổn định và đơn giản hơn.
- Istio Ambient Mesh là mô hình service mesh không sử dụng sidecar truyền thống. Thay vì gắn proxy vào từng pod, ambient mesh dùng thành phần ztunnel chạy ở cấp node để xử lý bảo mật và lưu lượng Layer 4.
- Khi cần các tính năng ở Layer 7 như HTTP routing, retries, timeouts, circuit breaking hoặc authorization policy chi tiết hơn, hệ thống có thể triển khai thêm waypoint proxy cho service hoặc namespace cụ thể.
- ztunnel tạo secure overlay giữa các workload thông qua HBONE, giúp lưu lượng service-to-service được bảo vệ bằng mTLS mà không cần sửa đổi mã nguồn ứng dụng.
- Việc bật Ambient Mesh có thể thực hiện bằng cách gắn nhãn `istio.io/dataplane-mode=ambient` cho namespace, từ đó các workload trong namespace sẽ tự động tham gia vào mesh.
- Mô hình này giúp giảm operational overhead vì không cần quản lý sidecar cho từng pod, đồng thời vẫn giữ được các lợi ích quan trọng của service mesh như encryption, observability và traffic policy.
- Bài blog cũng minh họa cách sử dụng Kiali và Prometheus để quan sát traffic graph, xác minh mTLS thông qua ztunnel và kiểm tra luồng giao tiếp giữa các service trong ứng dụng mẫu.
- Trong phần thực hành, bài viết hướng dẫn tạo EKS Auto Mode cluster, cài đặt Istio Ambient Mesh, triển khai ứng dụng mẫu retail store, bật ambient mode, kiểm tra mTLS và áp dụng AuthorizationPolicy ở cả Layer 4 và Layer 7.
- Đối với môi trường production, cần lưu ý chi phí tài nguyên AWS, quyền IAM phù hợp, bảo mật ingress gateway, chính sách phân quyền giữa các service và quy trình cleanup tài nguyên sau khi thử nghiệm.

## Hình ảnh

Dưới đây là hai hình minh họa kiến trúc gốc từ bài AWS Blog, thể hiện cách Istio Ambient Mesh hoạt động trên Amazon EKS Auto Mode ở hai mức Layer 4 và Layer 7.

![Kiến trúc Istio Ambient Mesh Layer 4 trên Amazon EKS Auto Mode](/eam-workshop-report/images/3-BlogsPosted/3.1-Blog1/c-170-1.jpg)

*Hình 1. Kiến trúc Istio Ambient Mesh với các tính năng Layer 4 trên Amazon EKS Auto Mode. Nguồn: AWS Blog, Figure 1.*

![Kiến trúc Istio Ambient Mesh Layer 7 với waypoint proxy](/eam-workshop-report/images/3-BlogsPosted/3.1-Blog1/c-170-2.jpg)

*Hình 2. Kiến trúc Istio Ambient Mesh với waypoint proxy cho các tính năng Layer 7. Nguồn: AWS Blog, Figure 2.*

## Hướng dẫn

Có thể tái hiện nội dung bài blog theo các bước tổng quát sau:

- Chuẩn bị môi trường: cài đặt AWS CLI, `kubectl`, Helm, Terraform và `envsubst`. Tài khoản AWS cần có quyền tạo EKS, EC2, IAM, VPC và các tài nguyên liên quan.
- Clone repository mẫu của AWS và chuyển vào thư mục Terraform dùng cho ambient mode.
- Chạy `terraform init`, `terraform plan` và `terraform apply --auto-approve` để tạo EKS Auto Mode cluster, node pool, Istio control plane và các thành phần cần thiết.
- Cấu hình `kubectl` bằng lệnh `aws eks update-kubeconfig`, sau đó kiểm tra các pod trong namespace `istio-system` để bảo đảm Istio đã hoạt động.
- Cài đặt Prometheus và Kiali để quan sát traffic trong mesh, sau đó port-forward Kiali về máy local để theo dõi service graph.
- Triển khai ứng dụng retail store mẫu bằng Helm, bao gồm các service như cart, catalog, checkout, orders và ui.
- Cài Gateway API CRDs nếu cluster chưa có sẵn, sau đó tạo Gateway và HTTPRoute để cho phép truy cập ứng dụng từ bên ngoài.
- Bật ambient mode cho namespace `default` bằng cách gắn nhãn `istio.io/dataplane-mode=ambient`, sau đó tải lại workload để các pod tham gia mesh.
- Áp PeerAuthentication ở chế độ `STRICT` để bắt buộc mTLS trong mesh và kiểm tra request từ pod ngoài mesh để xác minh chính sách bảo mật.
- Tạo AuthorizationPolicy ở Layer 4 để giới hạn service nào được phép gọi service catalog.
- Triển khai waypoint proxy cho service catalog nếu cần kiểm soát Layer 7, sau đó dùng `targetRefs` trong AuthorizationPolicy để giới hạn truy cập theo HTTP method hoặc path.
- Sau khi thực hành xong, cần cleanup các tài nguyên AWS để tránh phát sinh chi phí không cần thiết.

## Một số lệnh tham khảo

```bash
git clone https://github.com/aws-samples/sample-istio-ambient-eks-automode.git
cd sample-istio-ambient-eks-automode/terraform-blueprint/ambient

terraform init
terraform plan
terraform apply --auto-approve

aws eks --region us-west-2 update-kubeconfig --name ambient
kubectl get pods -A
kubectl label namespace default istio.io/dataplane-mode=ambient
kubectl port-forward svc/kiali 20001:20001 -n istio-system
```

## Kết luận

Bài blog cho thấy EKS Auto Mode và Istio Ambient Mesh là hai công nghệ bổ trợ tốt cho nhau trong quá trình triển khai Kubernetes hiện đại trên AWS. EKS Auto Mode giúp đơn giản hóa vận hành hạ tầng, còn Istio Ambient Mesh cung cấp khả năng bảo mật và kiểm soát lưu lượng theo hướng nhẹ hơn so với mô hình sidecar truyền thống. Đây là một hướng tiếp cận phù hợp cho các hệ thống microservices cần tính bảo mật, khả năng quan sát và khả năng mở rộng cao trong môi trường cloud-native.

<figure class="blog-group-post">
  <img src="/eam-workshop-report/images/3-BlogsPosted/3.2-Blog2/z8015011259315_7c6dbb49988bf6d90190842f5ae5b0ba.jpg" alt="Bài đăng blog 2 trên group AWS">
  <figcaption>Bài đăng đã chia sẻ trong group AWS.</figcaption>
</figure>
