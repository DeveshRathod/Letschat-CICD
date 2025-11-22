# 💬 LetsChat – Cloud‐Native CI/CD with Jenkins & Terraform

LetsChat is a cloud-native, **containerized** chat application orchestrated on **AWS ECS** and delivered through a **Jenkins-driven CI/CD pipeline** with SonarQube, Docker, Trivy, and **Terraform**. It features a React (Vite) frontend, Node.js backend with Socket.io, MongoDB, JWT auth, and secure media handling.


![Demo GIF](https://drive.google.com/uc?export=view&id=12K5E4gYXCzI-SRLQSEtVjQcgPub7yEgR)

---

## 🗄️ Database

**MongoDB (Atlas)**  
Used for storing:

- User profiles
- Friends and connections
- Messages and chat history
- Media metadata (images)

---

## ⚙️ Backend

**Stack:** Node.js + Express + Socket.io  
**Auth:** JWT, bcryptjs, and cookies  
**Storage:** Cloudinary for media files

### Key Features

- Stateless authentication using JWT
- Secure password hashing via bcrypt
- Cookies for refresh tokens
- Real-time bi-directional chat with Socket.io
- Scalable API design for chat, user, and friend management

### 🧩 CI/CD Pipeline (Jenkins)

1. **Checkout Code** – Jenkins fetches latest code and asks for image tag.
2. **SonarQube Scan** – Code quality and linting checks.
3. **ECR Check** – Ensures AWS ECR repository exists.
4. **Docker Build & Push** – Builds image and pushes to AWS ECR.
5. **Trivy Image Check** – Checks vulnarabilities in docker image.
6. **Terraform Apply** – Automates backend infra provisioning and deployment.

---

## ☁️ Backend Infrastructure (Terraform + AWS)

**Terraform** automates full infrastructure provisioning:

### Resources Created

- ECS Cluster for containerized backend
- IAM Roles and Policies for ECS tasks
- VPC with private subnets
- VPC Endpoints for:
  - S3
  - ECR
  - Secrets Manager
  - CloudWatch
  - CloudMap (for service discovery)
- ECS Service + Task Definition
- Service Discovery (CloudMap) for internal access
- NAT Gateway for DB access
- Security Groups for controlled communication
- S3 Bucket for Terraform remote state storage
- Autoscaling for ECS tasks

> ❗ Backend is **not exposed publicly** — it’s discoverable internally via **CloudMap** DNS from the frontend service.

---

## 💻 Frontend

**Stack:** React (Vite) + TailwindCSS + Zustand + React Router  
**State Management:** Zustand  
**Auth:** Cookies + JWT Tokens  
**Notifications:** React Toast

### CI/CD Pipeline (Jenkins)

- Similar to backend: checkout → sonar → docker → Trivy → ecr → terraform.
- Terraform fetches backend service namespace & cluster info dynamically and sets it as environment variables for frontend deployment.

### Deployment

- Frontend runs in **private subnets** and is accessible via **Load Balancer (LB)**.
- Communicates securely with backend via **CloudMap service name and namespace**.
- Supports **auto-scaling** for high traffic and performance.

---

## 🧠 Highlights

- Fully automated CI/CD using Jenkins + Terraform + AWS ECS
- Private backend accessible only within VPC
- Secure media and message handling
- Real-time chat and notifications via Socket.io
- Robust authentication and scalable design

---

## 🔐 Security & Networking

- Backend is **private** (no public access) — reachable only by frontend ECS service.
- **IAM roles** tightly scoped for least privilege.
- **VPC endpoints** ensure private connectivity to AWS services.
- **Secrets Manager** stores sensitive environment variables securely.
- **S3 remote state** ensures consistency across Terraform executions.

---

## 🧰 Tech Stack

| Layer    | Technology                                      |
| -------- | ----------------------------------------------- |
| Frontend | React (Vite), TailwindCSS, Zustand, Toastify    |
| Backend  | Node.js, Express, Socket.io                     |
| Database | MongoDB                                         |
| Storage  | Cloudinary                                      |
| Infra    | Terraform, AWS ECS, CloudMap, ECR, S3, IAM, VPC |
| CI/CD    | Jenkins, SonarQube, Docker                      |
| Auth     | JWT, bcryptjs, Cookies                          |

---

## 🧩 Project Structure

```
Shopease/
├── letschat-backend/                         # Node.js Express app + Jenkins file + Terraform (submodule)
├── letschat-frontend/                        # React Vite app + Jenkins file + Terraform (submodule)
├── README.md
└── .gitmodules                               # Submodule references
```

---

## 📸 Architecture Overview

**Frontend (Vite React)** → **Load Balancer (Private)** → **ECS Backend (CloudMap Discovery)** → **MongoDB + Cloudinary**

---

## 🚀 Project Highlights

- Fully automated multi-environment deployment
- Complete infrastructure-as-code setup with Terraform
- Zero-downtime deployment on AWS ECS
- End-to-end DevSecOps with SonarQube + Trivy
- Real-time chat

---

### 🔖 Author

**Devesh Rathod**  
📧 [GitHub Profile](https://github.com/DeveshRathod)  
💼 DevOps | Full Stack | Cloud Engineer

---
