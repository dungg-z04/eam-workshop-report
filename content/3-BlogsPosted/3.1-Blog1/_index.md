---
title: "Blog 1"
date: 2026-06-25
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# Amazon EKS now supports control plane egress through your VPC

**Source:** [Amazon EKS now supports control plane egress through your VPC](https://aws.amazon.com/blogs/containers/amazon-eks-now-supports-control-plane-egress-through-your-vpc/)

Amazon EKS has added customer-routed control plane egress, which allows certain outbound traffic from the Kubernetes API Server to be routed through the user's own Amazon VPC. This feature helps enterprises gain better control over the path of requests initiated by the control plane, such as admission webhook callbacks, OIDC provider lookups, and aggregate API server requests.

Instead of allowing these flows to use the EKS-managed network path, users can apply familiar VPC controls such as route tables, security groups, VPC endpoints, AWS PrivateLink, NAT Gateway, or AWS Network Firewall. This is an important improvement for Kubernetes systems that require strong security, especially in enterprise, financial, healthcare, or compliance-heavy environments.


## Key points

- Customer-routed control plane egress allows "customer-controllable" outbound flows from the Kubernetes API Server to pass through an Elastic Network Interface (ENI) located in the user's VPC.
- Supported traffic types include admission webhook callbacks, OIDC discovery document lookups, requests to aggregate API servers, and DNS resolution that supports these flows.
- When this feature is enabled, users can apply route tables, security groups, endpoint policies, NAT Gateway, AWS PrivateLink, VPC endpoints, AWS Network Firewall, and existing egress control rules in the VPC.
- The feature is especially useful for systems that need private networking, private OIDC providers, or admission webhooks that are only reachable inside a private network.
- Control plane egress through VPC is different from the EKS private endpoint. The private endpoint controls inbound access to the Kubernetes API Server, while customer-routed egress controls outbound traffic from the API Server to related services.
- Users can enable it when creating a new cluster or updating an existing cluster by setting `controlPlaneEgressMode = CUSTOMER_ROUTED` in `resourcesVpcConfig`.
- After a cluster is moved to `CUSTOMER_ROUTED`, this setting is fixed for the cluster lifecycle and cannot be changed back to `AWS_MANAGED`.
- IAM condition key `eks:controlPlaneEgressMode` can be combined with AWS Organizations Service Control Policies to require clusters in an organization to use `CUSTOMER_ROUTED`.
- VPC Flow Logs can be used to observe and verify connections from EKS-managed cross-account ENIs to internal endpoints, supporting auditing and compliance.
- Some flows that are not part of the Kubernetes API Server, such as EKS Capabilities or AWS STS calls from IAM Authenticator, continue to use the EKS-managed path and do not go through the user's VPC.

## Image

The diagram below illustrates the architecture when Private Control Plane Networking is enabled. Customer-controllable traffic from `kube-apiserver` passes through an ENI in the user's VPC, then is controlled by network components such as VPC endpoints, NAT Gateway, Transit Gateway, or AWS PrivateLink before reaching customer destinations.

![Control plane egress through the user's VPC when Private Control Plane Networking is enabled](/eam-workshop-report/images/3-BlogsPosted/3.2-Blog2/CONTAINERS-269-1.png)

*Figure 1. Control plane egress through the user's VPC when Private Control Plane Networking is enabled. Source: AWS Blog.*


## Guide

To learn and apply this feature, the main steps are:

1. Identify the EKS cluster that needs private control plane networking and check the subnets, security groups, route tables, and DNS resolver in the VPC.
2. When creating a new cluster, configure `resources-vpc-config` and add `controlPlaneEgressMode=CUSTOMER_ROUTED` to route egress through the VPC.
3. For an existing cluster, use the `update-cluster-config` command to move it to `CUSTOMER_ROUTED`, while noting that this setting cannot be changed back to `AWS_MANAGED`.
4. Make sure the endpoints that the Kubernetes API Server needs to call, such as admission webhooks, OIDC providers, or aggregate API servers, are reachable from the cluster subnets through private DNS, an internal load balancer, a VPC endpoint, or PrivateLink.
5. Check security groups, route tables, and NAT or PrivateLink paths to avoid situations where the API Server cannot call a webhook or OIDC endpoint.
6. Use `aws eks describe-cluster` to verify the `controlPlaneEgressMode` value and enable VPC Flow Logs to monitor the traffic path for auditing.
7. If managing multiple AWS accounts, use AWS Organizations SCP with condition key `eks:controlPlaneEgressMode` to require clusters to enable `CUSTOMER_ROUTED` according to the organization's security standard.

### AWS CLI reference commands

```bash
# Create a new cluster with customer-routed control plane egress
aws eks create-cluster \
  --name my-cluster \
  --kubernetes-version 1.36 \
  --role-arn arn:aws:iam::111122223333:role/eks-cluster-role \
  --resources-vpc-config subnetIds=subnet-aaa,subnet-bbb,securityGroupIds=sg-xxx,controlPlaneEgressMode=CUSTOMER_ROUTED

# Enable on an existing cluster
aws eks update-cluster-config \
  --name my-cluster \
  --resources-vpc-config controlPlaneEgressMode=CUSTOMER_ROUTED

# Verify configuration
aws eks describe-cluster --name my-cluster \
  --query "cluster.resourcesVpcConfig.controlPlaneEgressMode"
```

## Conclusion

Customer-routed control plane egress makes Amazon EKS more suitable for environments that require strict network control. Instead of only managing traffic from worker nodes and workloads, users gain additional control over part of the outbound traffic from the Kubernetes API Server. This improves privacy, supports auditing, reduces risk when using internal webhooks or OIDC providers, and helps deploy EKS in enterprise systems with high security requirements.
