# **MarketPeak E-Commerce Platform Deployment**  
*A comprehensive guide to deploying an e-commerce site using Git, Linux, and AWS*

![E-Commerce Deployment](https://cdn.pixabay.com/photo/2019/06/30/19/26/online-store-4309188_1280.jpg)

## **Table of Contents**
1. [Project Overview](#-project-overview)
2. [Git Version Control](#-git-version-control)
3. [AWS EC2 Deployment](#-aws-ec2-deployment)
4. [CI/CD Workflow](#-cicd-workflow)
5. [Troubleshooting](#-troubleshooting)
6. [Submission Guidelines](#-submission-guidelines)

---

## **📌 Project Overview**
Deploy "MarketPeak" e-commerce platform with:
- **Git** for version control  
- **Linux** (Amazon Linux 2) as the server OS  
- **AWS EC2** for cloud hosting  
- **Apache HTTPD** as the web server  

**Key Features**:
- Product listings  
- Shopping cart functionality  
- User authentication (template-based)  

---

## **🔄 Git Version Control**

### **1. Initialize Repository**
```bash
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce
git init
```

### **2. Add Template**
1. Download template from [Tooplate](https://www.tooplate.com/)  
2. Extract into project directory  
3. Customize (optional):
   - Update `logo.png`  
   - Modify `styles.css`  

### **3. Commit Changes**
```bash
git add .
git config --global user.name "YourName"
git config --global user.email "your@email.com"
git commit -m "Initial commit with e-commerce template"
```

### **4. Push to GitHub**
```bash
git remote add origin https://github.com/your-username/MarketPeak_Ecommerce.git
git push -u origin main
```

---

## **☁️ AWS EC2 Deployment**

### **1. Launch EC2 Instance**
1. **AMI**: Amazon Linux 2  
2. **Type**: `t2.micro` (Free Tier)  
3. **Security Group**: Allow HTTP (80), SSH (22)  

### **2. Connect via SSH**
```bash
ssh -i "your-key.pem" ec2-user@your-public-ip
```

### **3. Install Apache**
```bash
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd
```

### **4. Deploy Website**
```bash
# Clone repo (HTTPS/SSH)
git clone https://github.com/your-username/MarketPeak_Ecommerce.git

# Move files to web root
sudo rm -rf /var/www/html/*
sudo cp -r MarketPeak_Ecommerce/* /var/www/html/
```

### **5. Access Site**
Open browser:  
`http://<your-ec2-public-ip>`

---

## **⚙️ CI/CD Workflow**

### **Development Branch Workflow**
```bash
git checkout -b development
# Make changes...
git add .
git commit -m "Add new product filter"
git push origin development
```

### **Merge to Production**
1. Create PR on GitHub  
2. Review → Merge `development` into `main`  
3. On EC2:
   ```bash
   cd /var/www/html
   sudo git pull origin main
   sudo systemctl reload httpd
   ```

---

## **��️ Troubleshooting**

| Issue | Solution |
|-------|----------|
| **403 Forbidden** | Check `/var/www/html` permissions: `sudo chmod -R 755 /var/www/html` |
| **Git Push Rejected** | Pull latest changes first: `git pull origin main --rebase` |
| **Apache Not Running** | Debug with: `sudo systemctl status httpd` |

---

## Screenshots

<img width="871" alt="Snipaste_2025-07-07_01-40-58" src="https://github.com/user-attachments/assets/3bda0a1b-87d0-4a09-a3b6-f86d3e11d3ce" />

<img width="535" alt="Snipaste_2025-07-07_01-51-21" src="https://github.com/user-attachments/assets/690b2415-d9dc-4af4-9dc5-c60c25eb50d8" />



<img width="424" alt="Snipaste_2025-07-07_10-11-50" src="https://github.com/user-attachments/assets/2309681f-4e7d-4839-97ee-ee52d26513f4" />


<img width="1380" alt="Snipaste_2025-07-07_10-16-33" src="https://github.com/user-attachments/assets/51a5ee05-550d-4025-993e-4957a981c29c" />


<img width="558" alt="Snipaste_2025-07-07_10-18-18" src="https://github.com/user-attachments/assets/1c58174d-4fa5-4dc2-b7e1-043ce50ae310" />


<img width="624" alt="Snipaste_2025-07-07_10-21-18" src="https://github.com/user-attachments/assets/15af99c3-1b01-4c85-a71e-026a4aedf60f" />


<img width="595" alt="Snipaste_2025-07-07_10-22-30" src="https://github.com/user-attachments/assets/c318aa81-85be-44eb-b6b4-4525da0a7bf7" />


<img width="560" alt="Snipaste_2025-07-07_10-24-49" src="https://github.com/user-attachments/assets/488cd622-170a-48a7-a1a4-5a22028f0b85" />

---

**Pro Tip**: Use `terraform` or `AWS CloudFormation` to automate deployments in future iterations!  

```bash
# Verify deployment
curl -I http://localhost
```

update for development branch
