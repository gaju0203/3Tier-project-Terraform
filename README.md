## 3-Tier Architecture on AWS using Terraform
## Project Overview

I worked on a 3-Tier Architecture project on AWS using Terraform, where I automated the complete infrastructure using Infrastructure as Code and a modular design.

The architecture is divided into three layers: Web, Application, and Database, each deployed in separate subnets to ensure security, scalability, and high availability.

<img width="1191" height="635" alt="3-tier-project-TERRAFORM" src="https://github.com/user-attachments/assets/a2c40830-8a6e-4f25-b329-ed3d168e1823" />


## 3-Tier Architecture Explained

The architecture is divided into three logical layers:

### Presentation Tier (Web Layer)
- Public-facing layer
- Hosted on EC2 instances
- Accessible via Application Load Balancer
- Deployed in public subnets
  # In the Web tier, I deployed EC2 instances in public subnets behind an Application Load Balancer.The ALB receives traffic from the internet and distributes it to the web servers.Security Groups allow only HTTP/HTTPS traffic from the ALB, not directly from the internet.


### Application Tier (App Layer)
- Handles business logic
- EC2 instances in private subnets
- No direct internet access
  # The Application tier runs in private subnets with no direct internet access.These EC2 instances handle the business logic and only accept traffic from the Web tier.This improves security by isolating the application layer.

  
### Database Tier (DB Layer)
- Data storage layer
- Amazon RDS in private subnets
- Highly secure and isolated
  # The Database tier uses Amazon RDS, deployed in private subnets.The database is accessible only from the Application tier, not from the Web tier or internet.This ensures data security and follows AWS best practices.

## Technologies Used
- **Amazon VPC**
- **EC2**
- **Application Load Balancer**
- **Amazon RDS**
- **IAM**
- **Security Groups**
- **Remote Backend (S3 + DynamoDB)**


---
### I used Terraform modules to keep the code reusable and clean.Separate modules were created for VPC, EC2, ALB, and RDS.
## Terraform Modules

### VPC Module
- Creates VPC
- Public & private subnets
- Internet Gateway & route tables

### EC2 Module
- Launches EC2 instances
- Web and application servers
- Uses private/public subnets accordingly

### ALB Module
- Application Load Balancer
- Target groups & listeners
- Routes traffic to web tier

### RDS Module
- Creates RDS instance
- Private subnet placement
- Secure security groups

---

# I also configured a remote backend using S3 and DynamoDB for state storage and locking, which is important for team environments.

## Remote Backend Configuration

Terraform state is stored remotely using:

- **Amazon S3** – state file storage
- **DynamoDB** – state locking

Defined in `backend.tf` for:
- Team collaboration
- State consistency
- Safe infrastructure updates

---

### How to Deploy This Project

### 1️⃣ Clone the Repository
```bash
git clone 
cd 3Tier-project-Terraform
# Deployment Flow:- terraform init to initialize modules and backend,
                    terraform plan to review changes,
                    terraform apply to create infrastructure.
# Author 
Gaju Sawase
Aspiring AWS DevOps Engineer

