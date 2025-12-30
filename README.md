# Advanced Terraform & Nginx Multi-Tier Architecture

## FATIMA JINNAH WOMEN UNIVERSITY, RAWALPINDI  
**Course:** Cloud Computing  
**Assignment:** II  
**Instructor:** Sir Waqas Saleem  

**Submitted By:** Manahil Shujah  
**Registration No:** 2023-BSE-043  
**Semester:** V  
**Section:** B  
**Department:** Software Engineering  

**GitHub Repository:**  
https://github.com/23-22411-043/cc_ManahilShujah_043_Assignment2

---

## Table of Contents

- Executive Summary  
- Architecture Overview  
- Part 1: Infrastructure Setup  
  - Project Structure  
  - Variable Configuration  
  - Networking Module  
  - Security Module  
  - Locals Configuration  
- Part 2: Webserver Module  
- Part 3: Server Configuration Scripts  
- Part 4: Infrastructure Deployment  
- Part 5: Nginx Configuration & Testing  
- Bonus Tasks  
- Common Issues and Solutions  
- Infrastructure Cleanup  
- Conclusion  

---

## Executive Summary

This project demonstrates the deployment of a **high-availability multi-tier web architecture** on **AWS** using **Terraform**. The infrastructure is provisioned using Infrastructure as Code (IaC) principles and incorporates an **Nginx reverse proxy/load balancer** in front of multiple **Apache backend servers**.

The Nginx server is configured with:
- HTTPS using a self-signed SSL certificate  
- Load balancing  
- Caching for performance optimization  
- Backup server for high availability  
- Security headers and rate limiting  

Terraform modules are used to ensure clean structure, reusability, and scalability.

---

## Architecture Overview

<img width="431" height="272" alt="assignment_part1_project_structure" src="https://github.com/user-attachments/assets/ab99a3b9-aab6-46d0-afe1-b435611373f7" />

**Architecture Components:**
- Custom VPC  
- Public subnet  
- Internet Gateway  
- Nginx EC2 instance (Reverse Proxy & Load Balancer)  
- Three Apache EC2 backend servers  
- Separate security groups  

---

## Part 1: Infrastructure Setup

### 1.1 Project Structure

The Terraform project is organized using modules for clarity and reusability.

Assignment2/
├── main.tf
├── variables.tf
├── outputs.tf
├── locals.tf
├── terraform.tfvars
├── .gitignore
├── modules/
│   ├── networking/
│   ├── security/
│   └── webserver/
├── scripts/
│   ├── apache.sh
│   └── nginx.sh
└── screenshots/

.gitignore Configuration

<img width="404" height="235" alt="assignment_part1_gitignore" src="https://github.com/user-attachments/assets/c4629ca3-7eed-4d3a-804b-53cf699c45ec" />

1.2 Variable Configuration
Terraform variables are defined in variables.tf and populated in terraform.tfvars.

<img width="371" height="455" alt="assignment_part1_variables_tf" src="https://github.com/user-attachments/assets/1630c047-9565-41cb-950d-4889fd9a0301" />

<img width="376" height="216" alt="assignment_part1_terraform_tfvars" src="https://github.com/user-attachments/assets/d7dea98e-a0da-4bf8-a4ee-b33b926b887b" />


1.3 Networking Module
The networking module provisions:

<img width="467" height="454" alt="assignment_part1_networking_module_main" src="https://github.com/user-attachments/assets/e36c5856-aba0-441f-90ec-c3c5bbbc8704" />

<img width="461" height="219" alt="assignment_part1_networking_module_outputs" src="https://github.com/user-attachments/assets/71f6629c-24f3-4f71-8a1b-32d4745f8307" />


1.4 Security Module
Security groups are configured using the principle of least privilege.

<img width="346" height="473" alt="assignment_part1_security_module  png" src="https://github.com/user-attachments/assets/41640070-56c4-4275-869a-d2569bdb3bf6" />


1.5 Locals Configuration

<img width="287" height="266" alt="assignment_part1_locals_tf" src="https://github.com/user-attachments/assets/9cb52e55-c56a-4d66-9ef0-6bd56dfdef43" />


Part 2: Webserver Module
2.1 Module Design
A reusable module is created for EC2 instances.

<img width="353" height="422" alt="assignment_part2_webserver_module_variables" src="https://github.com/user-attachments/assets/440dbe63-ad36-4731-9caa-f773c2fea6e5" />

<img width="396" height="428" alt="assignment_part2_main_tf_modules" src="https://github.com/user-attachments/assets/b994620d-33aa-4bc5-8276-2170ec7c0bbe" />

<img width="329" height="136" alt="assignment_part2_webserver_module_outputs" src="https://github.com/user-attachments/assets/7d0c24a1-aa69-461f-9e08-10e94f076294" />


2.2 Module Usage
The module is instantiated:

<img width="396" height="428" alt="assignment_part2_main_tf_modules" src="https://github.com/user-attachments/assets/73a637c1-7c3f-4ab0-813f-b72403d2a974" />

Part 3: Server Configuration Scripts
3.1 Apache Backend Server Script
The Apache script:

<img width="302" height="466" alt="assignment_part3_apache_script" src="https://github.com/user-attachments/assets/42042ed8-a74f-453b-9d78-825f1ac6eecb" />

3.2 Nginx Server Setup Script
The Nginx script configures:

<img width="293" height="458" alt="assignment_part3_nginx_script" src="https://github.com/user-attachments/assets/2d99280f-c0e7-4070-a9d7-4ae3e7b28973" />

Part 4: Infrastructure Deployment
4.1 Initial Deployment
Terraform commands executed:

<img width="305" height="118" alt="assignment_part4_ssh_keygen" src="https://github.com/user-attachments/assets/61741534-ace1-4359-a368-e6dc1f4bea0a" />

<img width="287" height="184" alt="assignment_part4_terraform_init" src="https://github.com/user-attachments/assets/8c8659b8-f9a0-4ad2-b241-00e39e108311" />

<img width="245" height="34" alt="assignment_part4_terraform_validate" src="https://github.com/user-attachments/assets/b7e035cb-dfc9-4ba5-930d-003eaab5dab0" />

<img width="574" height="84" alt="assignment_part4_terraform_plan" src="https://github.com/user-attachments/assets/8810de65-e437-48d9-a16d-75517c061615" />

<img width="602" height="118" alt="assignment_part4_terraform_apply" src="https://github.com/user-attachments/assets/ef1e32f9-6dd1-4423-8599-9739b3fedc6b" />

4.2 Output Configuration
Terraform outputs display:

<img width="344" height="437" alt="assignment_part4_terraform_output" src="https://github.com/user-attachments/assets/8521447f-2bca-4d95-bbc3-abf29216a5a5" />

<img width="598" height="492" alt="assignment_part4_outputs_json" src="https://github.com/user-attachments/assets/ddf05f3f-e276-45c2-adbb-87144d43e307" />


4.3 AWS Console Verification

<img width="952" height="281" alt="assignment_part4_aws_vpc  png" src="https://github.com/user-attachments/assets/84ca90aa-e2ba-4861-a7f6-a4fa5f3eb4dd" />

<img width="942" height="397" alt="assignment_part4_aws_subnet png" src="https://github.com/user-attachments/assets/12e8033e-79cb-44de-a7a2-c0c2065d1d02" />

<img width="956" height="271" alt="assignment_part4_aws_security_groups" src="https://github.com/user-attachments/assets/86539218-7dd5-43e5-a274-5ed1dab92ef0" />

<img width="956" height="362" alt="assignment_part4_aws_instances" src="https://github.com/user-attachments/assets/02fdd352-1f2d-472b-a962-96c9a865a349" />

Part 5: Nginx Configuration & Testing
5.1 Update Nginx Backend Configuration

<img width="293" height="142" alt="assignment_part5_ssh_nginx" src="https://github.com/user-attachments/assets/1a7df22b-9602-4963-a99b-f19443ecc7e8" />

<img width="212" height="150" alt="assignment_part5_nginx_conf_updated" src="https://github.com/user-attachments/assets/297eb7f2-a3da-4c3b-bc45-672a9e7ae1f2" />

<img width="395" height="93" alt="assignment_part5_nginx_test" src="https://github.com/user-attachments/assets/1009bd69-7a9c-483d-94ce-24823700268a" />

<img width="407" height="124" alt="assignment_part5_nginx_restart" src="https://github.com/user-attachments/assets/159d00b6-4cd1-4598-8047-481d447ff49f" />

5.2 Test Load Balancing

<img width="529" height="260" alt="assignment_part5_ssl_warning" src="https://github.com/user-attachments/assets/db35ab6a-d126-4a04-8397-3162cf906621" />

<img width="245" height="198" alt="assignment_part5_web1_response" src="https://github.com/user-attachments/assets/913ebcbf-1054-45ae-81fb-6cc5e011a7a8" />

<img width="228" height="197" alt="assignment_part5_web2_response  png" src="https://github.com/user-attachments/assets/7a26a8d3-5f2e-4c74-9fa4-be3cd19a7d66" />

5.3 Test Cache Functionality

<img width="217" height="102" alt="assignment_part5_cache_miss" src="https://github.com/user-attachments/assets/3f65e803-b2b2-44ba-a656-9fae867850a8" />

<img width="218" height="119" alt="assignment_part5_cache_hit  png" src="https://github.com/user-attachments/assets/d134a990-b280-4155-bf6c-b8597202ee02" />

<img width="302" height="86" alt="assignment_part5_cache_directory" src="https://github.com/user-attachments/assets/0981669a-6aba-449c-98c7-02f0b519ba14" />

<img width="301" height="84" alt="assignment_part5_access_log_cache" src="https://github.com/user-attachments/assets/99d1f847-33fd-4ad2-af5b-3462839c8e13" />


5.4 Test High Availability (Backup Server)

<img width="267" height="52" alt="assignment_part5_web1_stopped" src="https://github.com/user-attachments/assets/fccd001e-5410-4dc6-b5de-70c2623f137a" />

<img width="268" height="56" alt="assignment_part5_web2_stopped" src="https://github.com/user-attachments/assets/bbae75b4-2e67-415c-a643-5555d7ba12fb" />

<img width="185" height="143" alt="assignment_part5_backup_activated" src="https://github.com/user-attachments/assets/aa295b3c-bce0-443c-b207-9496cacd2e20" />

<img width="267" height="99" alt="assignment_part5_nginx_error_log" src="https://github.com/user-attachments/assets/b7974d2f-2adb-4b47-ad0d-239acafe4ffa" />

<img width="194" height="128" alt="assignment_part5_services_restored" src="https://github.com/user-attachments/assets/814fe041-99d4-4a9f-b09c-0cec8ac80d8e" />

5.5 Security & Performance Analysis

<img width="206" height="170" alt="assignment_part5_ssl_certificate" src="https://github.com/user-attachments/assets/aeb55468-ae16-4984-b799-79a653432f40" />

<img width="266" height="110" alt="assignment_part5_security_headers  png" src="https://github.com/user-attachments/assets/0a13ed8b-9ba5-4592-b48a-9c70dbed51c0" />

<img width="269" height="187" alt="assignment_part5_http_redirect" src="https://github.com/user-attachments/assets/e5c398da-d8cb-4b13-be87-0b79f38a4270" />

<img width="269" height="46" alt="assignment_part5_error_log_analysis" src="https://github.com/user-attachments/assets/69b10158-bdb5-4128-b4fd-0e4a665b4cd6" />

<img width="268" height="35" alt="assignment_part5_access_log_analysis" src="https://github.com/user-attachments/assets/9ce423d2-87e3-4f5f-9ecb-1b2e318be91d" />

Bonus Tasks
 see word file or pd file

Conclusion
This assignment provided practical experience in Terraform module design, AWS networking, and advanced Nginx configuration. The deployed infrastructure successfully demonstrates load balancing, caching, security, and high availability, aligning with real-world cloud architecture best practices.

