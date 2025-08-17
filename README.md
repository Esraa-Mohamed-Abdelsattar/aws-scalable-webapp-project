# aws-scalable-webapp-project

## 📌 Project Overview
This project demonstrates how to deploy a **secure, highly available, and scalable web application** on AWS using **EC2**, **Application Load Balancer (ALB)**, and **Auto Scaling Groups (ASG)**. The setup ensures that the application can handle traffic spikes efficiently while minimizing operational costs.

---

## 🏗️ Architecture
The solution is built using a **multi-AZ design** for high availability.  

- **VPC** with **2 public subnets** and **2 private subnets** across **2 Availability Zones (AZs)**.  
- **Internet Gateway (IGW):** Provides internet access to public subnets.   
- **Application Load Balancer (ALB):** Distributes traffic across EC2 instances in multiple AZs.  
- **Auto Scaling Group (ASG):** Ensures the right number of EC2 instances are running.  
- **EC2 Instances (Web Tier):** Host the application.  
- **Amazon RDS (Optional, Multi-AZ):** Provides a reliable and managed backend database.  
- **IAM Roles :** Control access securely.  
- **CloudWatch + SNS:** Monitor system metrics and send alerts.  

📌 **High Availability:** EC2 instances are spread across **at least 2 AZs**.  
📌 **Scalability:** Auto Scaling adds/removes instances based on demand.  
📌 **Security:** Private subnets for databases, IAM roles for least privilege.  

---

## ⚙️ Deployment Steps

### 1. Networking
1. Create a **VPC** with 2 AZs.  
2. Create **public subnets** (for ALB, EC2) and **private subnets** (for RDS).  
3. Attach an **Internet Gateway** to the VPC.  
4. Configure **Route Tables**  

### 2. Compute & Load Balancer
1. Launch an **Application Load Balancer (ALB)** in public subnets.  
2. Configure **target groups** to forward requests to EC2 instances.  
3. Create an **Auto Scaling Group (ASG)**:  
   - Launch template with EC2 AMI (install Apache/Nginx + app).  
   - Spread across private subnets in 2 AZs.  
   - Configure scaling policies (scale out when CPU > 70%, scale in when CPU < 30%).  

### 3. Database (Optional)
1. Launch an **Amazon RDS (MySQL/PostgreSQL)** in Multi-AZ mode.  
2. Place RDS in **private subnets** for security.  
3. Configure **security groups** to allow access only from EC2 instances.  

### 4. Security
- **Security Groups**:  
  - ALB → Allow HTTP/HTTPS from the internet.  
  - EC2 → Allow only from ALB.  
  - RDS → Allow only from EC2 instances.  
- **IAM Roles**:  
  - EC2 → Role for S3 access (if needed).  
  - CloudWatch → Role for monitoring.  

### 5. Monitoring & Alerts
1. Create **CloudWatch Alarms** (e.g., CPU, memory, request count).  
2. Configure **SNS topic** for alert notifications (email/SMS).  

---

## 🛡️ Security Considerations
- Use **least privilege IAM roles**.  
- Place **databases in private subnets**.  
- Use **encrypted EBS volumes** and **RDS encryption**.    

---

## 📊 Cost Optimization
- Use **Auto Scaling** to handle peak traffic and scale in when idle.  
- Choose **EC2 Reserved/Spot Instances** for cost savings.  
- Use **RDS Multi-AZ only if required for production**.  

---

## 🎯 Learning Outcomes
By completing this project, you will learn:  
- How to set up a **scalable EC2-based application** on AWS.  
- How to use **ALB + ASG** for high availability and elasticity.  
- How to secure applications with **IAM, Security Groups, and private subnets**.  
- How to **monitor and optimize costs** using CloudWatch and scaling policies.  
