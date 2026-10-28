# ☁️ Secure AWS Web Server Deployment (Amazon Clone)

> **Amazon Linux 2023 EC2 instance aur Nginx web server ka use karke Amazon Clone web app ko AWS par live host karne ka complete project documentation.**

---

## 📐 System Architecture

Yeh architecture diagram batata hai ki client request kaise **Internet Gateway**, **VPC Route Tables**, aur **Security Group** se hote hue EC2 instance tak pahunchti hai:

![AWS Architecture Diagram](screenshots/Architecture-diagram.drawio.png)

---

## 🛠️ Infrastructure & Tech Stack

| Layer | Technology / Resource Used | Description |
| :--- | :--- | :--- |
| **Cloud Provider** | Amazon Web Services (AWS) | Region: `ap-south-1` (Mumbai) |
| **Compute Engine** | AWS EC2 (`t3.micro`) | Amazon Linux 2023 OS |
| **Networking** | AWS VPC & Public Subnet | Default VPC infrastructure with Internet Gateway |
| **Security** | AWS Security Group | Inbound rules: Port 22 (SSH) & Port 80 (HTTP) |
| **Web Server** | Nginx | Reverse proxy & static file server |
| **Storage** | AWS EBS | 8 GB SSD block volume |
| **CLI Tools** | Git Bash, SSH, SCP | Remote administration & file synchronization |

---

## 📸 Deployment Proof & Verification

### 1. Live Amazon Clone Application
Public IP address (`65.2.10.78`) par live load ho raha website:

![Live Deployment](screenshots/aws-ec2-amazon-clone-deployment.png)

---

### 2. Terminal Administration & File Transfer
Git Bash ke dwara SSH key se server login aur SCP se production files upload karna:

![Terminal Command Log](screenshots/Amazonclonegitbash.png)

---

## 🚀 Step-by-Step Deployment Guide

### Step 1: AWS Instance & Security Group Setup
1. AWS Console me `ap-south-1` region me **Amazon Linux 2023** EC2 instance launch kiya (`t3.micro`).
2. Security Group me 2 Inbound Rules add kiye:
   * **Port 22 (SSH):** Remote terminal access ke liye.
   * **Port 80 (HTTP):** Web browser access ke liye.

---

### Step 2: Nginx Web Server Install Karna
EC2 instance me SSH se login karke Nginx install aur start kiya:

```bash
# SSH connection command
ssh -i "my-web-server-key.pem" ec2-user@<ec2-public-ip>

# Nginx installation
sudo dnf update -y
sudo dnf install -y nginx

# Nginx start aur enable karna
sudo systemctl start nginx
sudo systemctl enable nginx
