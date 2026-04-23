# AWS-Personal-Portfolio-Deployment-EC2-RDS-Cloud-Networking

## 🔍 Project Overview

I deployed my personal portfolio website independently on AWS — not a guided lab, not a step-by-step tutorial, but a project I designed, configured, and troubleshot from scratch. The stack runs on an EC2 instance with Amazon Linux, uses Drupal as the CMS, and connects to a self-configured Amazon RDS MySQL database. The site is secured with SSL and served through a custom domain via DNS configuration.

---

## 🏗️ Architecture

<img width="818" height="305" alt="Architecture" src="https://github.com/user-attachments/assets/2a1040f9-e359-465a-96e7-0fc1277e71f8" />

---

## ⚙️ Tech Stack

| Technology        | Purpose                                              |
|-------------------|------------------------------------------------------|
| Amazon EC2        | Virtual server hosting the application               |
| Amazon Linux      | OS running on the EC2 instance                       |
| Drupal            | Content management system for the portfolio site     |
| Amazon RDS MySQL  | Managed relational database for Drupal content       |
| AWS Security Groups | Network-level firewall controlling inbound/outbound traffic |
| SSL Certificate   | Encrypts traffic between users and the server        |
| DNS Configuration | Maps custom domain to the EC2 public IP              |

---

## 🔐 Layer & Technology Breakdown 

**Layer 1 — Public Access** 
DNS resolves the custom domain to the EC2 instance's public IP. SSL terminates at the server, encrypting all traffic between the browser and the application. 

**Layer 2 — Application (EC2)** The EC2 instance runs Amazon Linux with Drupal installed. This layer handles all web requests, renders pages, and communicates with the database backend. 

**Layer 3 — Network Security (Security Groups)
** Two security groups control access: 
- SG-A is attached to EC2 and allows inbound HTTPS from the internet. - SG-B is attached to RDS and allows inbound TCP on port 3306 — but only from SG-A. 
The database is never exposed to the public internet. 

**Layer 4 — Data (RDS)** 
Amazon RDS manages the MySQL database. Drupal reads and writes content here. The RDS instance lives in a private subnet accessible only via the EC2 security group rule. 
