# Advanced Terraform & Nginx Multi-Tier Architecture  
**Assignment II – Cloud Computing**

## University Information
**Institution:** Fatima Jinnah Women University, Rawalpindi  
**Department:** Software Engineering  

**Submitted To:**  
Sir Waqas Saleem  

**Submitted By:**  
**Name:** Manahil Shujah  
**Registration No:** 2023-BSE-043  
**Semester:** V  
**Section:** B  

---

## Project Overview
This project implements a **multi-tier, high-availability web architecture on AWS** using **Terraform**. The purpose is to demonstrate Infrastructure as Code (IaC), modular Terraform design, AWS networking, and advanced **Nginx reverse proxy** configurations.

The architecture includes:
- One **Nginx server** acting as a reverse proxy and load balancer
- Three **Apache backend servers**, including one backup server
- HTTPS enabled using a self-signed SSL certificate
- Load balancing, caching, rate limiting, and failover support

---

## Architecture Overview
The system follows a reverse-proxy based architecture:

Client (Browser)
|
HTTPS Requests
|
Nginx Reverse Proxy (Public EC2)
|
Load Balancing
|
Apache Backend Servers (Private EC2s)

yaml
Copy code

---

## Project Structure
.
├── modules/
│ ├── networking/
│ ├── security/
│ └── webserver/
├── scripts/
│ ├── apache.sh
│ └── nginx.sh
├── main.tf
├── variables.tf
├── terraform.tfvars
├── locals.tf
├── outputs.tf
├── .gitignore
└── README.md

yaml
Copy code

---

## Terraform Modules

### Networking Module
Creates:
- VPC
- Subnets
- Internet Gateway
- Route Tables

### Security Module
Defines security groups:
- Nginx SG: HTTP, HTTPS, SSH allowed
- Backend SG: Traffic allowed only from Nginx

### Webserver Module
Reusable EC2 module used for:
- Nginx server
- Apache backend servers (using `for_each`)

---

## Server Configuration

### Apache Backend Servers
- Apache installed automatically
- Custom HTML page generated
- Displays EC2 metadata (hostname, IP) to verify load balancing

### Nginx Server
Configured to support:
- HTTPS with self-signed SSL
- Load balancing with backup server
- Proxy caching
- Security headers
- Rate limiting
- Custom error pages

---

## Deployment Steps

1. Initialize Terraform:
   ```bash
   terraform init
Validate configuration:

bash
Copy code
terraform validate
Review execution plan:

bash
Copy code
terraform plan
Deploy infrastructure:

bash
Copy code
terraform apply
Testing & Verification
Load Balancing
Refresh browser multiple times

Responses rotate between backend servers

Cache Verification
First request shows MISS

Subsequent requests show HIT in logs

High Availability
Primary backend servers stopped

Backup server successfully handles traffic

Security Testing
HTTP redirected to HTTPS

Security headers verified

Rate limiting returns HTTP 429

Bonus Features
Custom 404 and 502 error pages

Rate limiting

Automated health checks

Cleanup
To remove all AWS resources:

bash
Copy code
terraform destroy
Common Issues
SSH access issues: Check key permissions and security groups

Backend not responding: Verify Apache service and IPs

SSL errors: Check certificate paths and permissions

Conclusion
This project demonstrates practical implementation of Terraform, AWS infrastructure, and Nginx advanced features. The deployed system successfully supports load balancing, caching, security, and high availability, reflecting real-world cloud architecture best practices.

yaml
Copy code

---
