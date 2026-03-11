# AWS EC2 Load Balancer Project

## Project Overview

This project demonstrates how to build a **highly available web architecture on AWS** using multiple EC2 instances behind an **Application Load Balancer (ALB)**.

Two web servers are deployed on separate **Amazon EC2 instances**. Each server runs the **Nginx web server** and hosts a simple static webpage. An **AWS Application Load Balancer** distributes incoming traffic between these servers to ensure **high availability and reliability**.

When a user refreshes the page, the load balancer routes traffic to different servers (**Web Server 1** or **Web Server 2**).

---

# Architecture Overview

The architecture consists of:

- Internet traffic entering the system
- AWS Application Load Balancer distributing requests
- Two EC2 instances running Nginx web servers
- Each server hosting a static webpage

### Architecture Flow

```
                Internet
                    │
                    ▼
        AWS Application Load Balancer
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
   EC2 Web Server 1        EC2 Web Server 2
        │                       │
      Nginx                   Nginx
   Static Website          Static Website
```

The load balancer distributes incoming requests between the EC2 instances to improve:

- Availability
- Fault tolerance
- Traffic distribution
- Reliability

---

# Technologies Used

- Amazon EC2
- AWS Application Load Balancer
- Nginx Web Server
- Amazon VPC
- Security Groups
- Linux (Amazon Linux 2023)

---

# Project Components

## Amazon EC2 Instances

Two EC2 instances were created:

- Web Server 1
- Web Server 2

Each instance hosts a static web page using the **Nginx web server**.

### Purpose

- Provide compute resources
- Host the website
- Handle incoming web traffic

---

## Nginx Web Server

Nginx was installed on both EC2 instances to serve the web pages.

### Installation Commands

```
sudo dnf update -y
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

### Purpose

- Serve static web content
- Handle HTTP requests

---

## Application Load Balancer

An **AWS Application Load Balancer (ALB)** was created to distribute incoming traffic between the EC2 instances.

### Configuration

- Listener: HTTP (Port 80)
- Scheme: Internet-facing
- Connected to Target Group

### Purpose

- Distribute traffic across multiple servers
- Improve fault tolerance
- Ensure high availability

---

## Target Group

A target group was created to register the EC2 instances.

### Configuration

- Protocol: HTTP
- Port: 80
- Health Check Path: /

The load balancer only sends traffic to **healthy servers**.

---

## Security Groups

Security groups were configured to allow public access to the web servers.

### Inbound Rules

| Type | Protocol | Port | Source |
|-----|-----|-----|-----|
| HTTP | TCP | 80 | 0.0.0.0/0 |

### Purpose

- Allow incoming web traffic
- Control network access
- Protect instances from unauthorized traffic

---

# Implementation Steps

## Step 1 – Launch EC2 Instances

1. Open AWS Management Console
2. Navigate to EC2
3. Launch two EC2 instances
4. Select Amazon Linux AMI
5. Choose instance type t3.micro
6. Configure security group to allow HTTP (Port 80)

---

## Step 2 – Install Nginx

Connect to the EC2 instance and run:

```
sudo dnf update -y
sudo dnf install nginx -y
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

## Step 3 – Deploy Website

Replace the default Nginx page with a custom HTML page.

Example:

```
sudo nano /usr/share/nginx/html/index.html
```

Each server was configured with a different page:

- Server 1 shows **Web Server 1**
- Server 2 shows **Web Server 2**

---

## Step 4 – Create Target Group

1. Go to EC2 → Target Groups
2. Create a new target group
3. Select target type Instance
4. Register both EC2 instances
5. Configure health checks

---

## Step 5 – Create Application Load Balancer

1. Go to EC2 → Load Balancers
2. Create Application Load Balancer
3. Select Internet Facing
4. Add HTTP listener (Port 80)
5. Attach the previously created Target Group

---

## Step 6 – Test Load Balancer

Open the Load Balancer DNS in a browser.

Example:

http://web-load-balancer-1649422783.ap-south-1.elb.amazonaws.com

Refreshing the page alternates between:

- Web Server 1
- Web Server 2

This confirms that load balancing is working correctly.

---

# Project Screenshots

## EC2 Instances

![EC2 Instances](screenshots/instances.png.png)

---

## Application Load Balancer

![Load Balancer](screenshots/load balancer.png.png)

---

## Target Group Health Status

![Target Group](screenshots/target-group.png)

---

## Web Server 1 Response

![Server 1](screenshots/server1.png.png)

---

## Web Server 2 Response

![Server 2](screenshots/server2.png.png)

---

# Result

The Application Load Balancer successfully distributes traffic between both EC2 instances.

### Benefits Achieved

- High availability
- Traffic distribution
- Improved reliability
- Fault tolerance

---

# Future Improvements

This architecture can be enhanced further by adding:

- Auto Scaling Group
- HTTPS with SSL certificates
- CloudWatch monitoring
- CI/CD pipeline
- Infrastructure as Code using Terraform

---

# Key Learning Outcomes

Through this project I learned:

- How to deploy web servers on AWS EC2
- How to install and configure Nginx
- How Application Load Balancers distribute traffic
- How to configure Target Groups and Health Checks
- How to design a basic high availability cloud architecture

---

# Author

Dheeraj Kumar  
Cloud & DevOps Enthusiast