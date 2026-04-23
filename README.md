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
