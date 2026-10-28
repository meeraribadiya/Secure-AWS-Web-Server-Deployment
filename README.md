# ☁️ Secure AWS Web Server Deployment with Linux, VPC & Nginx

Production-ready hosting of a responsive web application (Amazon Clone) on **AWS EC2** using **Amazon Linux 2023**, custom **Security Groups**, **VPC networking**, and **Nginx** web server architecture.

---

## 📐 System Architecture

![AWS Architecture Diagram](screenshots/Architecture-diagram.drawio.png)

### 🏗️ Infrastructure & Network Specifications

| Component | Resource Type | Description / Configuration |
| :--- | :--- | :--- |
| **Cloud Provider** | Amazon Web Services (AWS) | Deployed in region `ap-south-1` (Mumbai) |
| **Compute Engine** | AWS EC2 (`t3.micro`) | Running Amazon Linux 2023 OS |
| **Virtual Private Cloud** | AWS VPC & Public Subnet | Default VPC with Internet Gateway routing |
| **Security Firewall** | AWS Security Group | Inbound rules for SSH (Port 22) & HTTP (Port 80) |
| **Web Server** | Nginx Engine | Serves static application build files |
| **Storage Layer** | AWS EBS (Elastic Block Store) | 8 GB SSD General Purpose storage volume |
| **CLI Management** | Git Bash, SSH, SCP | Remote administration and deployment pipeline |

---

## 📸 Deployment Proof & Screenshots

### 1. Live Application & Terminal CLI Operations
| Live Deployment View | Terminal Execution (SSH / SCP) |
| :---: | :---: |
| ![Live Web App](screenshots/aws-ec2-amazon-clone-deployment.png) | ![Git Bash Terminal](screenshots/Amazonclonegitbash.png) |

---

### 2. AWS Management Console Verification
| EC2 Launch Setup | VPC Network Dashboard | Subnet & Route Table | Nginx Welcome Verification |
| :---: | :---: | :---: | :---: |
| ![EC2 Config](screenshots/ec2-launch-config.png) | ![VPC Dashboard](screenshots/vpc-dashboard.png) | ![Subnet Route Table](screenshots/subnet-route-table.png) | ![Nginx Welcome](screenshots/nginx-welcome-page.png) |

---

## 🚀 Step-by-Step Execution Workflow

### Step 1: Compute & Network Provisioning
1. Launched an AWS EC2 `t3.micro` instance running **Amazon Linux 2023** in `ap-south-1`.
2. Configured an AWS Security Group with the following inbound traffic rules:
   * **Port 22 (SSH):** Remote terminal administration via RSA key pair (`.pem`).
   * **Port 80 (HTTP):** Inbound web access for public HTTP traffic.

### Step 2: Nginx Web Server Installation
Connected to the instance via SSH and configured Nginx service:

```bash
# Connect to EC2 instance
ssh -i "my-web-server-key.pem" ec2-user@<ec2-public-ip>

# Update package repositories & install Nginx
sudo dnf update -y
sudo dnf install -y nginx

# Start and enable Nginx daemon
sudo systemctl start nginx
sudo systemctl enable nginx
