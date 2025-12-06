# 🚀 CloudLiftDemo – Modernizing the CloudProfile Application

CloudLiftDemo is a project that demonstrates how a legacy multi-tier application can be modernized using **AWS managed services**, shifting away from VM-based deployment to a fully cloud-optimized architecture.

![alt text](<CloudLiftDemo Arcitechture.png>)

The goal is to improve agility, scalability, performance, and reduce operational overhead.

---

## 🌟 Project Overview

The application was earlier deployed using a **lift-and-shift strategy** on EC2.  
In this project, the entire stack is **re-architected** using PaaS and SaaS services:

- **Elastic Beanstalk** for application hosting  
- **Amazon RDS** for MySQL  
- **ElastiCache** for caching  
- **Amazon MQ** for messaging  
- **CloudFront + Route 53** for CDN & DNS  
- **S3** for artifact storage  

This modernization helps achieve a flexible, pay-as-you-go, auto-scaling, and highly managed environment.

---

## 🏗️ Architecture Summary

### **Frontend Stack**
- Elastic Beanstalk (EC2 + ALB + Auto Scaling)
- CloudFront (CDN)
- Route 53 (DNS)
- S3 (Artifact storage)

### **Backend Stack**
- Amazon RDS – MySQL  
- Amazon MQ – Managed message broker  
- ElastiCache – Redis caching  

---

## 🔁 Before vs After (Modernization Highlights)

| Old Setup (VM/EC2) | New Setup (AWS Managed) |
|--------------------|-------------------------|
| Tomcat on EC2 | Elastic Beanstalk |
| MySQL on VM/EC2 | Amazon RDS |
| Memcache on EC2 | ElastiCache |
| RabbitMQ on EC2 | Amazon MQ |
| Local DNS | Route 53 |
| No CDN | CloudFront |

---

## 💡 Why This Refactor?

- No server patching or maintenance  
- Built-in auto scaling  
- Highly available managed database  
- Global content delivery  
- Lower operational overhead  
- Faster deployment cycles  

---

## 🧩 High-Level Flow

1. User accesses the domain → Route 53  
2. Route 53 → CloudFront CDN  
3. CloudFront → Application Load Balancer (Beanstalk)  
4. ALB → EC2 instances (auto-scaled by Beanstalk)  
5. Application interacts with:
   - RDS
   - Amazon MQ
   - ElastiCache  
6. Artifacts are stored and deployed from S3  
7. CloudWatch monitors scaling & health  

---

## 🛠️ Implementation Steps

### **1. Core Setup**
- Create key pair  
- Create backend security group  
- Provision RDS, ElastiCache, and Amazon MQ  

### **2. Environment Deployment**
- Create Elastic Beanstalk environment  
- Update backend security group to allow Beanstalk access  
- Configure health check path to `/login`  
- Add HTTPS listener (443) on the load balancer  

### **3. Database Initialization**
- Launch a temporary EC2 instance  
- Connect to RDS using MySQL client  
- Initialize the application database  

### **4. Application Build**
- Update application properties with:  
  - RDS Endpoint  
  - MQ Endpoint  
  - ElastiCache Endpoint  
- Build the artifact  
- Upload to S3 & deploy to Beanstalk  

### **5. Global Access Setup**
- Create CloudFront distribution  
- Attach SSL certificate  
- Update DNS using Route 53 or GoDaddy  
- Test the final URL  

---

## 📈 Key Outcomes

- Zero-maintenance backend services  
- Auto-scaling application tier  
- Fully managed message broker  
- Highly available database  
- Global delivery with CDN  
- Cleaner, modular, cloud-friendly architecture  

---

## 🧪 Testing Checklist

- Application accessible via CloudFront URL  
- HTTPS working properly  
- Login page health check passing  
- Database connection successful  
- Messaging with MQ functioning  
- Cache layer responding  

---

