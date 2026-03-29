# 🚀 ECS Fargate Multi-Tier Application with Terraform

This project provisions a **complete multi-tier application infrastructure on AWS ECS Fargate** using Terraform.

It includes:

* Frontend service
* Backend service
* RDS database
* Application Load Balancers
* VPC networking
* IAM roles

This setup represents a **real-world production-like architecture**.

---

## 📌 Project Overview

This project deploys:

* 🟢 Frontend container (UI)
* 🔵 Backend container (API)
* 🟡 MySQL RDS database
* 🌐 Application Load Balancers (ALB)
* 🧱 ECS Cluster (Fargate)
* 🔐 IAM roles
* 🌍 VPC with networking components

---

## 🏗️ Architecture

```
     Internet
        │
     Route53
        │
   Frontend ALB
        │
Frontend ECS Service
        │
     Route53
        │
   Backend ALB
        │
Backend ECS Service
        │
    RDS MySQL

```

---

## 📁 Project Structure

```
.
├── vpc.tf                     # VPC, subnets, routing
├── cluster.tf                 # ECS cluster
├── iam-role.tf                # IAM role for ECS tasks
├── datasource.tf              # Fetch existing AWS resources
├── frontend-task-service.tf   # Frontend ALB + ECS service
├── backend-task-sevice.tf     # Backend ALB + ECS service
├── rds.tf                     # MySQL RDS database
```

---

## ⚙️ How the Project Works

---

### 🔹 VPC Setup (`vpc.tf`)

* Creates VPC (`10.0.0.0/16`)
* Creates 2 public subnets across availability zones
* Attaches Internet Gateway
* Configures route tables

👉 Enables internet-facing services like ALB and ECS

---

### 🔹 ECS Cluster (`cluster.tf`)

* Creates ECS Cluster (`my-ecs-cluster`)
* Uses Fargate launch type

👉 Acts as compute engine for containers

---

### 🔹 IAM Role (`iam-role.tf`)

* Creates ECS Task Execution Role
* Allows:

  * Pulling images from ECR
  * Sending logs to CloudWatch

---

### 🔹 Data Sources (`datasource.tf`)

Fetches existing resources using tags:

* VPC
* Public subnets
* Private subnets
* Security groups

⚠️ Some infrastructure must already exist

---

### 🔹 Frontend Service (`frontend-task-service.tf`)

* Creates Internet-facing ALB
* Creates Target Group
* ECS Task:

  * CPU: 256
  * Memory: 512
  * Port: 80
* ECS Service:

  * Runs 1 task
  * Attached to ALB

👉 Handles user traffic

---

### 🔹 Backend Service (`backend-task-sevice.tf`)

* Separate ALB for backend
* ECS Task with environment variables:

```
DB_HOST = <RDS Endpoint>
PORT = 3306
DB_USERNAME = admin
DB_PASSWORD = veeranarni
```

* ECS Service connected to RDS

👉 Handles business logic

---

### 🔹 Database (`rds.tf`)

* MySQL 8.x
* Instance: db.t3.micro
* Multi-AZ enabled
* Storage: 20GB
* Publicly accessible

👉 Stores application data

---

## 🔄 Application Flow

1. User hits **Frontend ALB**
2. Request goes to **Frontend ECS container**
3. Frontend calls **Backend ALB**
4. Backend processes request
5. Backend connects to **RDS**
6. Response returns to user

---

## 🧰 Tech Stack

* AWS ECS (Fargate)
* Terraform
* Docker (ECR)
* Application Load Balancer
* MySQL RDS
* VPC Networking

---

## ⚠️ Important Notes

* ❗ Database password is hardcoded (not secure)
* ❗ RDS is publicly accessible
* ❗ Some resources are expected to exist already
* ❗ Multiple provider blocks should be consolidated

---

## 🚀 Deployment Steps

```bash
git clone https://github.com/ShubhamCloudOps/ECS-Fargate-Project-with-Terraform.git
cd ECS-Fargate-Project-with-Terraform

terraform init
terraform plan
terraform apply
```

---

## 🌐 Access Application

After deployment:

* Use Frontend ALB DNS to access UI
* Use Backend ALB DNS for API testing

---

## 💰 Cost Warning

This project creates billable AWS resources:

* ECS Fargate
* Application Load Balancers (2x)
* RDS (Multi-AZ)

👉 Always destroy resources after testing

---

## 🔄 Destroy Infrastructure

```bash
terraform destroy
```

---

## 📈 Future Improvements

* Use AWS Secrets Manager for credentials
* Make RDS private
* Add Auto Scaling
* Use HTTPS (ACM)
* Implement CI/CD (Jenkins / GitHub Actions)
* Use single ALB with path-based routing

---

## 👤 Author

**ShubhamCloudOps** 

---

## ⭐ Support

If you found this project helpful, give it a ⭐ on GitHub!
