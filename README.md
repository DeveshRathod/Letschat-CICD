# 💬 LetsChat – Cloud-Native Deployment (Terraform | Github Actions | AWS ECS)

This project demonstrates a production-grade DevOps setup built around **Terraform modular infrastructure**, **Github Actions**, **secure containerization**, and **AWS ECS Fargate**.  
Application details are intentionally minimized—focus is on **infra, automation, security, and delivery**.


---
## 🧰 Demo

![Demo GIF](https://drive.google.com/file/d/1_MM6eg89JrWMt3fgGXj5AH_7k-248h7z/view?usp=sharing)

---

## 🧰 Tech Stack 

- **Terraform (modular)** – ECS, ALB, CloudMap, IAM, SGs, VPC Endpoints  
- **Github Actions CI/CD** – Multi-stage build/test/scan/deploy pipeline  
- **Docker (non-root, hardened images)**  
- **Trivy** – Image vulnerability scanning  
- **SonarQube** – Code quality gates  
- **AWS ECS Fargate** – Container orchestration  
- **Secrets Manager** – Secure config  
- **S3** – Terraform remote state + build artifacts  
- **CloudWatch** – Logs + metrics  
- **CloudMap** – Internal service discovery (private DNS)

---

## 🚀 CI/CD Pipeline (Github Actions)

A fully automated pipeline that handles:

1. **Checkout**  
2. **SonarQube Analysis**  
3. **Docker Build (non-root)**  
4. **Trivy Scan (block on high severity)**  
5. **Image Push**  
6. **Terraform Init/Plan/Apply**  
7. **ECS Rolling Deployment**

✔ Zero manual steps  
✔ Same pipeline for both frontend & backend  
✔ Ensures consistent, secure, repeatable deployments  

---

## 🏗️ Infrastructure (Terraform)

Infrastructure is built using a clean, reusable module structure:

```
modules/
  ecs/
  service/
  route53/

environments/
  dev/
  qa/
  prod/

tfvars/
  dev.tfvars
  qa.tfvars
  prod.tfvars
```

### Key Infra Capabilities

- Private-only ECS services  
- Load balancer for frontend  
- CloudMap for backend internal DNS  
- VPC Endpoints for S3, ECR, Secrets Manager, CloudWatch  
- IAM least-privilege roles  
- Autoscaling based on CPU/Mem  
- Remote state stored in S3  

> Backend is not public—communication happens only through CloudMap inside the VPC.

---

## 🔐 Security Highlights

- Non-root Docker images  
- Trivy enforcement in CI  
- All traffic kept private using VPC endpoints  
- AWS IAM + scoped task execution roles  
- S3-backed state with locking  
- No public SG rules for backend  

---

## 📦 DevOps Highlights

- Complete infra as code  
- Modular + multi-env Terraform  
- Automated build/scan/deploy pipelines  
- Private VPC-only architecture  
- CloudMap-based microservice communication  
- Secure secret storage using AWS Secrets Manager  
- Zero-downtime ECS deployments  

---

## 🔖 Author  

**Devesh Rathod**  
GitHub: https://github.com/DeveshRathod  
DevOps | Cloud | Automation  
