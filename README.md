## AWS-Personal-Portfolio-Deployment-EC2-RDS-Cloud-Networking

## 🔍 Project Overview

I deployed my personal portfolio website independently on AWS — not a guided lab, not a step-by-step tutorial, but a project I designed, configured, and troubleshot from scratch. The stack runs on an EC2 instance with Amazon Linux, uses Drupal as the CMS, and connects to a self-configured Amazon RDS MySQL database. The site is secured with SSL and served through a custom domain via DNS configuration.

---

## 🏗️ Architecture (diagram)

<img width="818" height="305" alt="Architecture" src="https://github.com/user-attachments/assets/2a1040f9-e359-465a-96e7-0fc1277e71f8" />

---

## 📸 AWS Console — Proof of Deployment

Both instances are stopped to manage costs and avoid unnecessary charges — fully operational during active development and can be restarted to demonstrate the live EC2 → RDS connection.

EC2 Instance (t3.micro — Amazon Linux)
<img width="1567" height="236" alt="Instances" src="https://github.com/user-attachments/assets/5170d619-1402-4e40-9d34-ef9b0afa7180" />


RDS Database (db.t4g.micro — MySQL)
<img width="1545" height="262" alt="Aurora and RDS" src="https://github.com/user-attachments/assets/eb871258-6085-4a9a-b223-ea052a3dbc1f" />

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

Layer 1 — Public Access
DNS resolves the custom domain to the EC2 instance's public IP. SSL terminates at the server, encrypting all traffic between the browser and the application. 

Layer 2 — Application (EC2)
The EC2 instance runs Amazon Linux with Drupal installed. This layer handles all web requests, renders pages, and communicates with the database backend. 

Layer 3 — Network Security (Security Groups)
Two security groups control access: 
- SG-A is attached to EC2 and allows inbound HTTPS from the internet.
- SG-B is attached to RDS and allows inbound TCP on port 3306 — but only from SG-A. The database is never exposed to the public internet. 

Layer 4 — Data (RDS)
Amazon RDS manages the MySQL database. Drupal reads and writes content here. The RDS instance lives in a private subnet accessible only via the EC2 security group rule. 

---

## 📂 Repo Structure

```
aws-portfolio-deployment/
│
├── README.md                        # Project documentation (this file)
├── architecture/
│   └── architecture-diagram.png     # Visual architecture diagram
├── screenshots/
│   ├── ec2-instance.png             # AWS Console — EC2 instance (t3.micro)
│   └── rds-instance.png             # AWS Console — RDS MySQL instance (db.t4g.micro)
├── config/
│   ├── drupal-settings.php          # Drupal DB connection config (redacted)
│   └── security-group-rules.md     # Notes on SG-A and SG-B configuration
└── notes/
    └── troubleshooting-log.md       # Debugging notes including the RDS port 3306 fix

```

---

## 💡 Key Takeaways 

The problem that taught me the most: Everything was configured — EC2 running, RDS live, Drupal installed — but Drupal kept timing out on the database connection. After checking credentials and restarting services, I traced it to one missing inbound rule: the RDS security group wasn't allowing traffic on port 3306 from the EC2 security group. 

One rule. That was the fix. But understanding *why* that rule had to be scoped specifically to the EC2 security group — and why opening port 3306 to 0.0.0.0/0 would expose the database to the entire internet — taught me more about cloud networking than anything I had read before. 

What I learned:
- How AWS security groups act as stateful, layer-4 firewalls 
- Why databases should never have public inbound rules — access should always be scoped to trusted resources 
- How to troubleshoot connectivity issues across EC2 and RDS by isolating each layer
- How DNS propagation and SSL termination work in a real deployment  


