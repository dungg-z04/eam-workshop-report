---
title: "Blog 2"
date: 2026-06-25
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Amazon EKS Auto Mode and Istio Ambient Mesh

> Posted on [AWS Study Group VN](https://www.facebook.com/groups/660548818043427/) on June 24, 2026

**Source:** [AWS Containers Blog - Better Together: Amazon EKS Auto Mode and Istio Ambient Mesh](https://aws.amazon.com/blogs/containers/better-together-amazon-eks-auto-mode-and-istio-ambient-mesh/)


This blog post introduces how Amazon EKS Auto Mode can be combined with Istio Ambient Mesh to reduce the operational burden of Kubernetes and service mesh adoption in a cloud-native environment. EKS Auto Mode automates many operational parts of the cluster, while Istio Ambient Mesh provides security, observability, and traffic control without requiring a sidecar proxy for every pod.

The main highlight of the article is that this model allows enterprises to adopt service mesh in a lighter, more scalable way that fits microservices systems on Amazon EKS. Instead of managing many nodes, sidecars, and complex configurations, operation teams can use EKS Auto Mode together with ambient mode to focus more on applications and security policies.

## Key points

- EKS Auto Mode automates many cluster operations such as node provisioning, autoscaling, patching, and infrastructure management, helping reduce operational overhead for DevOps teams.
- Nodes in EKS Auto Mode run on EC2 managed instances, use a container-optimized operating system, and are managed by AWS across many platform responsibilities, making cluster operations more stable and simpler.
- Istio Ambient Mesh is a service mesh model that does not use traditional sidecars. Instead of attaching a proxy to each pod, ambient mesh uses the `ztunnel` component at the node level to handle security and Layer 4 traffic.
- When Layer 7 features are needed, such as HTTP routing, retries, timeouts, circuit breaking, or more detailed authorization policies, the system can add a waypoint proxy for a specific service or namespace.
- `ztunnel` creates a secure overlay between workloads through HBONE, helping service-to-service traffic stay protected with mTLS without requiring application code changes.
- Ambient Mesh can be enabled by adding the `istio.io/dataplane-mode=ambient` label to a namespace. Workloads in that namespace then automatically join the mesh.
- This model reduces operational overhead because teams do not need to manage a sidecar for every pod, while still keeping important service mesh benefits such as encryption, observability, and traffic policy.
- The blog also demonstrates how to use Kiali and Prometheus to observe the traffic graph, verify mTLS through `ztunnel`, and inspect communication between services in the sample application.
- In the hands-on section, the post shows how to create an EKS Auto Mode cluster, install Istio Ambient Mesh, deploy a sample retail store application, enable ambient mode, verify mTLS, and apply AuthorizationPolicy at both Layer 4 and Layer 7.
- For production environments, teams should consider AWS resource costs, proper IAM permissions, ingress gateway security, service-to-service authorization policies, and resource cleanup after testing.

## Images

The following two diagrams from the AWS Blog show how Istio Ambient Mesh works on Amazon EKS Auto Mode at Layer 4 and Layer 7.

![Istio Ambient Mesh Layer 4 architecture on Amazon EKS Auto Mode](/eam-workshop-report/images/3-BlogsPosted/3.1-Blog1/c-170-1.jpg)

*Figure 1. Istio Ambient Mesh architecture with Layer 4 features on Amazon EKS Auto Mode. Source: AWS Blog, Figure 1.*

![Istio Ambient Mesh Layer 7 architecture with waypoint proxy](/eam-workshop-report/images/3-BlogsPosted/3.1-Blog1/c-170-2.jpg)

*Figure 2. Istio Ambient Mesh architecture with waypoint proxy for Layer 7 features. Source: AWS Blog, Figure 2.*


## Guide

The content of the blog can be reproduced through the following general steps:

- Prepare the environment: install AWS CLI, `kubectl`, Helm, Terraform, and `envsubst`. The AWS account needs permission to create EKS, EC2, IAM, VPC, and related resources.
- Clone the AWS sample repository and move into the Terraform directory used for ambient mode.
- Run `terraform init`, `terraform plan`, and `terraform apply --auto-approve` to create the EKS Auto Mode cluster, node pool, Istio control plane, and required components.
- Configure `kubectl` with `aws eks update-kubeconfig`, then check pods in the `istio-system` namespace to make sure Istio is running.
- Install Prometheus and Kiali to observe mesh traffic, then port-forward Kiali to the local machine to inspect the service graph.
- Deploy the sample retail store application with Helm, including services such as cart, catalog, checkout, orders, and ui.
- Install Gateway API CRDs if the cluster does not already have them, then create a Gateway and HTTPRoute to allow external access to the application.
- Enable ambient mode for the `default` namespace by adding the `istio.io/dataplane-mode=ambient` label, then restart workloads so that pods join the mesh.
- Apply PeerAuthentication in `STRICT` mode to require mTLS in the mesh and test requests from a pod outside the mesh to validate the security policy.
- Create a Layer 4 AuthorizationPolicy to limit which service is allowed to call the catalog service.
- Deploy a waypoint proxy for the catalog service when Layer 7 control is needed, then use `targetRefs` in AuthorizationPolicy to limit access by HTTP method or path.
- After completing the practice, clean up AWS resources to avoid unnecessary costs.

## Reference commands

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

## Conclusion

The blog shows that EKS Auto Mode and Istio Ambient Mesh complement each other well when deploying modern Kubernetes workloads on AWS. EKS Auto Mode simplifies infrastructure operations, while Istio Ambient Mesh provides security and traffic control in a lighter way than the traditional sidecar model. This is a suitable approach for microservices systems that require security, observability, and scalability in a cloud-native environment.

<figure class="blog-group-post">
  <img src="/eam-workshop-report/images/3-BlogsPosted/3.2-Blog2/z8015011259315_7c6dbb49988bf6d90190842f5ae5b0ba.jpg" alt="Blog post 2 shared in the AWS group">
  <figcaption>Blog post shared in the AWS group.</figcaption>
</figure>
