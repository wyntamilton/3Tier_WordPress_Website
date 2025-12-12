# 🌐 3-Tier WordPress Deployment on AWS  

## 📌 Project Overview  
This project is a full end-to-end **WordPress deployment** built on a secure **3-Tier Traditional Architecture** in AWS.

The environment consists of isolated network layers, private compute resources, a managed MySQL database, and an Application Load Balancer that exposes WordPress to the internet while keeping all sensitive infrastructure private.  

This project demonstrates my ability to:

- Design and deploy multi-tier architectures using AWS best practices  
- Build and configure VPCs, subnets, route tables, NAT gateways, and security groups  
- Deploy EC2 instances in private subnets and access them securely through a PuTTY  
- Configure RDS MySQL for WordPress  
- Use EFS for scalable shared storage  
- Configure an Application Load Balancer to distribute traffic  
- Install, configure, and secure a WordPress application stack on Linux  
---

## 🌍 Real-World Problem This Project Solves  

Modern web applications require **security, scalability, and high availability**. A simple single-server deployment cannot handle real production workloads and exposes the database and application to the internet, creating security risks.

This project solves those problems by:

---

### ✔️ Isolating applications in private subnets  
The WordPress EC2 instances and RDS database **cannot be reached from the internet**, protecting them from attacks.

### ✔️ Using a Load Balancer for availability  
An Application Load Balancer distributes traffic across multiple instances, improving performance and uptime.

### ✔️ Enabling secure outbound updates through NAT  
Private EC2 instances can download updates without exposing themselves or their private IPs.

### ✔️ Providing a scalable, production-ready foundation  
This architecture mirrors real-world enterprise deployments, making it easy to scale horizontally, manage traffic, and integrate additional services.

---

## 🛠️ Tools & Technologies Used  

### **AWS Services**
- **Amazon VPC** – custom isolated network  
- **Subnets (Public & Private)** – for tier separation  
- **Internet Gateway (IGW)** – internet access for public layer  
- **NAT Gateway** – allows outbound internet for private instances  
- **Route Tables** – control traffic routing  
- **Amazon EC2** – bastion host + WordPress application servers  
- **Amazon RDS (MySQL)** – managed WordPress database  
- **Amazon EFS** – shared file storage  
- **Application Load Balancer (ALB)** – distributes traffic  
- **IAM Roles & Policies** – secure permissions  
- **Security Groups** – firewall rules for each layer  

### **Linux + Application Stack**
- Apache (httpd)  
- PHP & PHP extensions  
- WordPress configuration  

### **Networking & Access**
- SSH tunneling through a PuTTY
- Private IP connectivity for web + DB tiers  

---
# 🧠 Steps Performed

## 1️⃣ Networking Setup – VPC, Subnets & Routing  
I built the network by creating a custom VPC with public and private subnets to separate the internet-facing resources from the internal application and database layers. I attached an Internet Gateway for public access, created route tables for both subnet types, and configured NAT Gateways so private instances could reach the internet for updates without being exposed. This setup established the secure network structure needed for the entire project.

#### 📸 Screenshots
Putty: <br/>
<img src="https://i.imgur.com/p6ysvQB.png" height="80%" width="80%" alt="IAM ROLE"/>
<br />
<br />
VPC: <br/>
<img src="https://i.imgur.com/KBkE7ID.png" height="80%" width="80%" alt="IAM ROLE"/>
<br />
<br />
InternetGateway:  <br/>
<img src="https://i.imgur.com/t9yw8Uj.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
Subnets: <br/>
<img src="https://i.imgur.com/J8vd1be.png" height="80%" width="80%" alt="IAM ROLE"/>
<br />
<br />
NAT:  <br/>
<img src="https://i.imgur.com/FmwJumg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

## 2️⃣ Security Controls – Security Groups & IAM  
I created Security Groups for each tier, including the public EC2 instance, private WordPress servers, ALB, and RDS database. Each group was configured with tightly controlled inbound rules so only the correct resources could communicate. IAM roles were added where needed to allow AWS services to securely interact. This ensured the architecture followed proper access control and security best practices.

Security Group: <br/>
<img src="https://i.imgur.com/jFyGiRH.png" height="80%" width="80%" alt="IAM ROLE"/>
<br />
<br />
Instance:  <br/>
<img src="https://i.imgur.com/fqCXqbA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

## 3️⃣ Database Setup – DB Subnet Group, RDS MySQL, and EFS  
For the database layer, I created a DB Subnet Group using private subnets and deployed an Amazon RDS MySQL instance that could only be accessed by the WordPress application servers. I also created an EFS file system with mount targets in the private subnets to enable shared file storage for WordPress if needed. This step established the persistent and secure backend required for the application.
<br />
EFS:  <br/>
<img src="https://i.imgur.com/5FwB8D7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

## 4️⃣ Compute Setup – EC2 Instances, PuTTY Access, and WordPress  
I launched one EC2 instance in a public subnet and connected to it directly using PuTTY. This server was used to configure the system and perform installation steps. I also launched two additional EC2 instances in private subnets that served as the WordPress application servers. After connecting and configuring them, I installed Apache, PHP, WordPress, mounted EFS (optional), and updated the wp-config.php file with the RDS database details.

<br />
MYSQL: <br/>
<img src="https://i.imgur.com/ku3j2ST.png" height="80%" width="80%" alt="IAM ROLE"/>
<br />
<br />
PHP:  <br/>
<img src="https://i.imgur.com/hFIFshH.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
## 5️⃣ Application Load Balancer – Target Group & Listener  
To expose the WordPress site, I created an Application Load Balancer in the public subnets. I then created a target group and registered both private EC2 application servers. After configuring the ALB listener on port 80 to forward traffic to the target group, the ALB successfully routed incoming traffic to the WordPress servers. This provided a secure and scalable entry point to the application.
<br />
<br />
WordPress: <br />
<img src="https://i.imgur.com/4a5INi2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
