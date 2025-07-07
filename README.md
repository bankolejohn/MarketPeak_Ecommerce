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

## **📝 Submission Guidelines**

### **1. Documentation**
Include in `README.md`:
- Deployment steps  
- Screenshots of live site  
- Challenges faced  

### **2. Repository Contents**
```
MarketPeak_Ecommerce/
├── index.html          # Homepage
├── products/           # Product listings
├── css/                # Stylesheets
├── img/                # Product images
└── README.md           # Project documentation
```

### **3. Submission**
1. Push final code to GitHub  
2. Share repo link on darey.io  

---

**Pro Tip**: Use `terraform` or `AWS CloudFormation` to automate deployments in future iterations!  

```bash
# Verify deployment
curl -I http://localhost
```
