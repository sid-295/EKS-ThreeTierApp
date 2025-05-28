# EKS Three-Tier Application

This project demonstrates deployment of a Three-Tier Web Application using Docker and AWS EKS.

## Overview
The application consists of three parts:
- Frontend (ReactJS)
- Backend (NodeJS)
- Database (MongoDB)


## Steps I followed

### 1. Create EKS Cluster using eksctl
```bash
eksctl create cluster --name three-tier-cluster --region us-east-1 --node-type t2.medium --nodes 2 --nodes-min 2 --nodes-max 2
```

### 2. Update kubeconfig to connect kubectl with EKS cluster
```bash
aws eks update-kubeconfig --region us-east-1 --name three-tier-cluster
```



### 3. Install Helm (if not installed)
```bash
sudo snap install helm --classic
```
### 4. sudo snap install helm --classic
```bash
helm repo add eks https://aws.github.io/eks-charts
helm repo update eks
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=my-cluster --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller
kubectl get deployment -n kube-system aws-load-balancer-controller
kubectl apply -f full_stack_lb.yaml
```

### 5. Deploy Helm charts (for example, AWS Load Balancer Controller)
```bash
helm repo add eks https://aws.github.io/eks-charts
helm repo update
helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=three-tier-cluster --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller
```

## Cleanup

To delete the EKS cluster and avoid unnecessary charges:
```bash
eksctl delete cluster --name three-tier-cluster --region us-east-1
```

---

Feel free to customize the manifests and Docker images to add your own features!

---

Happy Deploying! 🚀
