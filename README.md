# 🚀 3-Tier Infrastructure Deployment Using Terraform Modules

## Introduction
This project demonstrates the creation and deployment of a **3-tier architecture** on **Amazon Web Services (AWS)** using **Terraform modules**. It follows industry best practices for modular, scalable, and secure infrastructure as code (IaC).

---

## 📁 Project Structure

```

3-tier-terraform/
├── main.tf               # Root Terraform file invoking modules
├── variables.tf          # Input variable definitions
├── outputs.tf            # Output variable definitions
├── terraform.tfvars      # Actual variable values
├── backend.tf            # Optional backend config for remote state (S3/DynamoDB)
│
├── modules/
│   ├── vpc/              # VPC, Subnets, NAT, IGW
│   ├── web/              # EC2 instance setup for Web Tier
│   ├── app/              # EC2 instance setup for App Tier
│   ├── db/               # RDS MySQL instance setup
│   └── security/         # Security Groups for all tiers

````

---

## 🧾 Project Overview

This 3-tier architecture follows a widely adopted software design pattern that organizes applications into **Web**, **Application**, and **Database** tiers. Each tier is:

- **Isolated** in its own subnet
- **Secured** using Terraform-managed security groups
- **Provisioned** using reusable Terraform modules

---

## 🏗️ Architecture Overview

### 1️⃣ Web Tier
- Deployed in public subnets
- EC2 instances with a web server (Apache/Nginx)
- Accessible via HTTP/HTTPS and SSH

### 2️⃣ Application Tier
- Deployed in private subnets
- EC2 instances running backend services (e.g., Python/Node.js)
- Communicates only with Web Tier and DB Tier
- No direct internet access

### 3️⃣ Database Tier
- Deployed in private subnets
- Amazon RDS MySQL
- Accessible only from Application Tier

---

## 🌐 Network Design

- Custom **VPC**
- **Public Subnets** (Web Tier)
- **Private Subnets** (App and DB Tiers)
- **Internet Gateway** for external traffic
- **NAT Gateway** for private subnet egress
- Route tables with proper subnet associations

---

## 🔐 Security Groups

| Layer         | Inbound Access From               |
|---------------|-----------------------------------|
| Web Tier      | HTTP/HTTPS/SSH from internet      |
| App Tier      | Custom port (e.g., 8080) from Web |
| Database Tier | MySQL (3306) from App Tier        |

---

## ⚙️ Module Breakdown

### 🔹 `vpc/`
- VPC, subnets, routing, NAT/IGW

### 🔹 `security/`
- Creates security groups for all tiers

### 🔹 `web/`
- Public EC2 with Apache/Nginx and user data script

### 🔹 `app/`
- Private EC2 for backend logic

### 🔹 `db/`
- RDS MySQL, subnet group, and secure access

---

## 🛠 Tools Used

| Tool         | Purpose                        |
|--------------|--------------------------------|
| Terraform    | Infrastructure provisioning   |
| AWS EC2      | Compute instances              |
| AWS RDS      | Managed MySQL DB               |
| AWS VPC      | Networking and isolation       |

---

## 🚀 Deployment Steps

```bash
# Clone the repository
git clone https://github.com/Swatiz-cloud/3-tier-terraform-modules.git
cd 3-tier-terraform

# Configure variable values in terraform.tfvars

# Initialize Terraform
terraform init

# Validate configuration
terraform validate

# Preview the changes
terraform plan

# Apply the configuration
terraform apply
````

---

## 📤 Output Values

* Public IP of Web EC2 instance
* Private IPs of App EC2 instance
* RDS MySQL endpoint
* Subnet and VPC IDs

---

## 🛡️ Security Measures

* Public access restricted to Web Tier only
* App and DB tiers in private subnets
* NAT Gateway used for secure outbound access
* Sensitive data stored securely in `.tfvars`

---

## 🧹 Cleanup Instructions

```bash
# Destroy all infrastructure
terraform destroy

# Optional cleanup
rm -rf .terraform terraform.tfstate*
```

Verify AWS Console to ensure all resources are removed.

---

## 📈 Benefits of Modular Terraform

* 🔍 **Clarity** – Separation of concerns improves maintainability
* ♻️ **Reusability** – Modules can be reused in different environments
* 📏 **Consistency** – Predictable and parameterized deployments
* 🚀 **Scalability** – Easy to add/remove components
* 🤖 **Automation** – Full IaC workflow

---

## 🧪 Future Enhancements

* Add ALB for Web Tier
* Enable Auto Scaling Groups
* Use Secrets Manager or SSM for DB credentials
* Enable HTTPS via ACM
* Add CloudWatch for logging and monitoring
* Use remote backend with S3 & DynamoDB

---

## ✅ Conclusion

This project provides a **modular, secure, and scalable** AWS infrastructure using Terraform. It is a strong base for production-ready applications and can easily be extended for high availability, automation, and DevOps pipelines.

---

**Author**: [Swatiz-cloud](https://github.com/Swatiz-cloud)
📌 *Feel free to fork and contribute!*


