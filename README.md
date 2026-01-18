# K8s-lab

A minimal beginner-friendly Kubernetes project to deploy an Nginx web server.

This repo contains declarative YAML manifests for:
- A Deployment managing Nginx Pods
- A Service to expose the app

## Prerequisites
- A running Kubernetes cluster (e.g., Minikube, Kind, or a cloud cluster)
- `kubectl` configured to access your cluster

## Deploying and Testing the Nginx Application

### Apply the manifests
```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

### Verify pods running, and nginx service
```bash
kubectl get pods -l app=nginx
kubectl get service my-nginx-service
```

### Access nginx server
```bash
minikube service my-nginx-service
kubectl port-forward svc/my-nginx-service 8080:80
```

### Cleanup
```bash
kubectl delete -f deployment.yaml
kubectl delete -f service.yaml
```

# Amazon EKS (Elastic Kubernetes Service)
Running your own Kubernetes control plane is complex and operationally heavy. Amazon EKS is AWS's managed Kubernetes service that handles the control plane for you.
Key points:

AWS manages the highly available control plane (API server, etcd, etc.) across multiple AZs.
You manage the worker nodes (via node groups or self-managed nodes, often using EC2 Auto Scaling Groups).
Fully compatible with upstream Kubernetes — you use the same kubectl and tools.
Integrates deeply with AWS services: IAM for auth, VPC networking, ELB/ALB for Services/Ingress, CloudWatch for logging/metrics, etc.

aws.amazon.comField Notes: Managing an Amazon EKS Cluster Using AWS CDK and ...
# Getting Started with EKS

Create an EKS cluster via AWS Console, CLI (eksctl), or Terraform/CDK.
Example with eksctl (popular community tool):Basheksctl create cluster --name my-cluster --region us-east-1 --nodegroup-name standard-workers --node-type t3.medium --nodes 3

Once created, kubectl automatically configures to talk to your EKS cluster.
Deploy apps exactly as you would on any Kubernetes cluster.

EKS vs Self-Managed Kubernetes


AspectSelf-Managed KubernetesAmazon EKSControl PlaneYou manage (HA, upgrades, etcd)AWS manages (HA, automatic upgrades)CostPotentially lower, more ops workPay for control plane + EC2 nodesUpgradesManualAWS offers managed upgrade pathsIntegrationGenericDeep AWS service integration (IAM, VPC, ALB)Compliance/CertificationsYou ensureAWS handles many (SOC, PCI, etc.)
EKS is the most popular managed Kubernetes offering, followed by GKE (Google) and AKS (Azure).