# AWS-Personal-Portfolio-Deployment-EC2-RDS-Cloud-Networking

## 🔍 Project Overview

I deployed my personal portfolio website independently on AWS — not a guided lab, not a step-by-step tutorial, but a project I designed, configured, and troubleshot from scratch. The stack runs on an EC2 instance with Amazon Linux, uses Drupal as the CMS, and connects to a self-configured Amazon RDS MySQL database. The site is secured with SSL and served through a custom domain via DNS configuration.

---

## 🏗️ Architecture

Internet (HTTPS)
│
▼  DNS + SSL
┌─────────────────────┐         Port 3306 (TCP)        ┌────────────────────────┐
│    EC2 Instance     │  ──────────────────────────▶   │     RDS Instance        │
│  Amazon Linux       │                                 │  Amazon RDS MySQL       │
│  Drupal CMS         │                                 │  Security Group (SG-B)  │
│  Security Group (SG-A)                               │  Inbound: SG-A only     │
└─────────────────────┘                                 └────────────────────────┘
