# ☁️ Secure AWS Web Server Deployment with Linux, VPC & Nginx

> **Production-ready cloud hosting of a web application (Amazon Clone) on AWS EC2 using Amazon Linux 2023, custom Security Group configurations, and Nginx reverse proxy architecture.**

---

## 📐 System Architecture

The following diagram illustrates the network flow and infrastructure design implemented in **AWS `ap-south-1` (Mumbai)**:

![AWS Cloud Infrastructure Architecture](screenshots/Architecture-diagram.png)

### 🏗️ Architecture Breakdown

| Component | Resource Type | Function in Deployment |
| :--- | :--- | :--- |
| **AWS Region** | `ap-south-1` (Mumbai) | Geographic region hosting the cloud infrastructure |
| **Virtual Private Cloud (VPC)** | Default VPC | Isolated virtual network environment |
| **Public Subnet** | Route-table enabled subnet | Allows public internet ingress and egress routing |
| **Internet Gateway (IGW)** | AWS Managed IGW | Connects the VPC directly to the public internet |
| **Route Tables** | Target `0.0.0.0/0` -> IGW | Directs HTTP and SSH internet requests to the subnet |
| **Security Group** | State-based Virtual Firewall | Restricts inbound traffic to Ports 22 (SSH) and 80 (HTTP) |
| **Compute Engine** | AWS EC2 (`t3.micro`) | Amazon Linux 2023 virtual server executing Nginx |
| **Storage Engine** | AWS EBS (8 GB General Purpose SSD) | Persistent block storage for OS and web assets |

---

## 📸 Deployment Proof & Screenshots

### 1. Live Web Application Served via EC2
Website active and serving static HTML/CSS assets over public IP (`65.2.10.78`):

![Live Amazon Clone Deployment](screenshots/aws-ec2-amazon-clone-deployment.png)

---

### 2. Terminal Administration & CLI File Synchronization
Managing the server via **SSH** key authentication and transferring production builds using **SCP**:

![Git Bash CLI Operations](screenshots/Amazonclonegitbash.png)

---

### 3. AWS Console Verification

| EC2 Launch Setup | VPC Network Dashboard | Subnet & Routing Table | Nginx Status Verification |
| :---: | :---: | :---: | :---: |
| ![EC2 Config](screenshots/ec2-launch-config.png) | ![VPC Dashboard](screenshots/vpc-dashboard.png) | ![Subnet Route Table](screenshots/subnet-route-table.png) | ![Nginx Welcome](screenshots/nginx-welcome-page.png) |

---

## 🛠️ Technology Stack

| Layer | Technology / Tool Used |
| :--- | :--- |
| **Cloud Provider** | Amazon Web Services (AWS) |
| **Operating System** | Amazon Linux 2023 |
| **Web Server** | Nginx |
| **Terminal & CLI Tools** | Git Bash, SSH, SCP |
| **Security & Keys** | RSA Key-Pair Authentication (`.pem`) |
| **Version Control** | Git & GitHub |

---

## 🚀 Step-by-Step Execution Workflow

### Step 1: Compute & Network Provisioning
1. Launched an AWS EC2 `t3.micro` instance running **Amazon Linux 2023** in `ap-south-1`.
2. Created a Security Group with explicit inbound access rules:

| Type | Protocol | Port Range | Source | Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **SSH** | TCP | 22 | `0.0.0.0/0` | Secure remote shell management |
| **HTTP** | TCP | 80 | `0.0.0.0/0` | Public web access |

---

### Step 2: Nginx Web Server Installation
Connected to the instance via SSH and configured Nginx services:

```bash
# Connect to EC2 instance
ssh -i "my-web-server-key.pem" ec2-user@<ec2-public-ip>

# Update package manager and install Nginx
sudo dnf update -y
sudo dnf install -y nginx

# Start and enable Nginx daemon
sudo systemctl start nginx
sudo systemctl enable nginx
