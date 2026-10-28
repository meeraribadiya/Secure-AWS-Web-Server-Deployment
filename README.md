# Secure AWS Web Server Deployment with Linux, VPC & Nginx

A hands-on cloud project demonstrating how to deploy a static Amazon Clone website on AWS EC2 using Amazon Linux 2023, Nginx, and AWS networking services.

## Architecture Diagram

![AWS Architecture Diagram](<Architecture diagram.drawio.png>)

## Technologies Used

- **AWS EC2:** Hosts the web server.
- **Amazon Linux 2023:** Operating system for the EC2 instance.
- **Nginx:** Serves the website.
- **VPC and Public Subnet:** Provide network connectivity.
- **Internet Gateway and Route Table:** Enable internet traffic.
- **Security Groups:** Control network access.
- **Git Bash, SSH and SCP:** Connect to the server and transfer files.
- **Git and GitHub:** Manage project files and version control.

## Deployment Steps

### 1. Launch EC2 Instance

Launch an EC2 instance using Amazon Linux 2023 in the Mumbai region (`ap-south-1`). Configure a key pair and security group.

### 2. Configure Security Group

| Type | Port | Source |
|---|---:|---|
| SSH | 22 | `65.2.10.78`|
| HTTP | 80 | `0.0.0.0/0` |

### 3. Connect to EC2

Open Git Bash in the folder containing your `.pem` key and connect using SSH.

```bash
chmod 400 my-web-server-key.pem
ssh -i "my-web-server-key.pem" ec2-user@65.2.10.78
```

Replace the key filename and public IP with your actual values.

### 4. Install Nginx

Run these commands inside the EC2 terminal:

```bash
sudo dnf update -y
sudo dnf install -y nginx
sudo systemctl enable --now nginx
```

### 5. Deploy the Website

Transfer your website files using SCP and place them in Nginx's web root directory:

`/usr/share/nginx/html/`

### 6. Verify Deployment

Open the following URL in your browser:

`http://65.2.10.78`

Your website should appear if the instance and Nginx are configured correctly.

## Security Notes

- Restrict SSH access to your own IP address.
- Never upload your private `.pem` key or AWS credentials to GitHub.
- Check AWS Free Tier eligibility and potential charges before launching resources.

## Key Learnings

- EC2 instance setup and Linux server administration.
- Nginx installation and web hosting.
- AWS VPC, subnet, route table, and Internet Gateway fundamentals.
- SSH authentication and SCP file transfer.
- Security Group configuration and basic cloud security.
