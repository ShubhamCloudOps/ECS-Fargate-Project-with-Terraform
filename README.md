# 🚀 EKS Fargate Project with Terraform

## 📌 Overview

This project demonstrates how to build a **fully serverless Kubernetes platform on AWS** using:

- **Amazon EKS (Elastic Kubernetes Service)**
- **AWS Fargate (serverless compute for containers)**
- **Terraform (Infrastructure as Code)**

The infrastructure is provisioned end-to-end using Terraform, and applications are deployed on EKS using Fargate without managing EC2 worker nodes.

Prerequisites: Build and push Frontend & Backend images to ECR using Docker.
---

## 🧠 Architecture

```
User → ALB → Kubernetes Service → Pods (Fargate)
                        ↑
                    EKS Cluster
                        ↑
                  Terraform (IaC)
```

---

## ⚙️ Tech Stack

- **Cloud Provider:** AWS  
- **Container Orchestration:** Kubernetes (EKS)  
- **Compute:** AWS Fargate  
- **Infrastructure as Code:** Terraform  
- **Networking:** VPC, Subnets, Internet Gateway, NAT Gateway  
- **Security:** IAM Roles & Policies, Security Groups  
- **Load Balancing:** AWS Application Load Balancer (ALB)  

---

## 📁 Project Structure

```
.
├── main.tf              # Main Terraform configuration
├── variables.tf         # Input variables
├── outputs.tf           # Output values
├── provider.tf          # AWS provider configuration
├── vpc.tf               # VPC and networking setup
├── eks.tf               # EKS cluster setup
├── fargate.tf           # Fargate profile configuration
├── iam.tf               # IAM roles and policies
└── README.md
```

---

## 🚀 Features

- ✅ Fully automated infrastructure using Terraform  
- ✅ Serverless Kubernetes using AWS Fargate  
- ✅ No EC2 worker node management  
- ✅ Secure networking with public/private subnets  
- ✅ IAM-based access control  
- ✅ Scalable and production-ready architecture  

---

## 🏗️ Infrastructure Components

### 🔹 VPC Setup
- Custom VPC with CIDR block  
- Public and private subnets  
- Internet Gateway and NAT Gateway  

### 🔹 EKS Cluster
- Managed Kubernetes control plane  
- Highly available and scalable  

### 🔹 Fargate Profile
- Runs Kubernetes pods without EC2 nodes  
- Namespace-based workload execution  

### 🔹 IAM Configuration
- Cluster role  
- Fargate pod execution role  

---

## 🛠️ Prerequisites

Before you begin, ensure you have:

- AWS Account  
- AWS CLI configured  
- Terraform installed (>= 1.x)  
- kubectl installed  

---

## ⚡ Setup & Deployment

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/ShubhamCloudOps/EKS-Fargate-Project-with-Terraform.git
cd EKS-Fargate-Project-with-Terraform
```

### 2️⃣ Initialize Terraform
```bash
terraform init
```

### 3️⃣ Validate Configuration
```bash
terraform validate
```

### 4️⃣ Plan Infrastructure
```bash
terraform plan
```

### 5️⃣ Apply Changes
```bash
terraform apply
```

---

## 🔍 Verify Cluster

Update kubeconfig:
```bash
aws eks --region <region> update-kubeconfig --name <cluster-name>
```

Check nodes:
```bash
kubectl get nodes
```

Check pods:
```bash
kubectl get pods -A
```

---

## 📦 Sample Deployment (Optional)

```bash
kubectl create deployment nginx --image=nginx
kubectl expose deployment nginx --type=LoadBalancer --port=80
```

---

## 🔐 Security Best Practices

- Use IAM roles instead of static credentials  
- Store secrets in AWS Secrets Manager / SSM  
- Restrict Security Group access  
- Use private subnets for workloads  

---

## 📈 Future Enhancements

- 🔹 CI/CD pipeline (Jenkins / GitHub Actions)  
- 🔹 Monitoring (Prometheus + Grafana / CloudWatch)  
- 🔹 Multi-environment setup (dev/stage/prod)  
- 🔹 Helm-based deployments  
- 🔹 Autoscaling (HPA + Cluster Autoscaler)  

---

## 💡 Key Learnings

- Implementing Infrastructure as Code using Terraform  
- Deploying serverless Kubernetes with EKS Fargate  
- Managing cloud networking and security  
- Designing scalable and production-ready systems  

---

## 👨‍💻 Author

**Shubham Kharche**  
DevOps / Cloud Engineer  

---

## ⭐ Support

If you found this project helpful:

- ⭐ Star the repository  
- 🍴 Fork it  
- 🛠️ Contribute  

---
