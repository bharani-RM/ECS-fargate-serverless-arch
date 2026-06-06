# Portfolio Website Deployment using AWS ECS Fargate with Auto Scaling

## Project Overview

This project demonstrates how to deploy a containerized portfolio website using AWS ECS Fargate with an Application Load Balancer and Auto Scaling.

The portfolio website is packaged into a Docker container, stored in Amazon ECR, deployed using ECS Fargate, and exposed to users through an Application Load Balancer.

---

## Features

* Containerized portfolio website
* Deployment using AWS ECS Fargate
* Docker image storage using Amazon ECR
* Application Load Balancer integration
* Multi-AZ deployment
* Auto Scaling configuration
* CloudWatch monitoring support
* Highly available architecture

---

## Architecture

```text
Users
   |
   v
Application Load Balancer
   |
   v
ECS Fargate Service
   |
   +-------------------+
   |                   |
Task 1              Task 2
(Nginx)             (Nginx)
   |
   v
Amazon ECR Repository
```

---

## Networking Architecture

```text
Internet
   |
Internet Gateway
   |
VPC (10.0.0.0/16)

Public Subnet A (AZ1)
    |
ECS Task 1

Public Subnet B (AZ2)
    |
ECS Task 2

Application Load Balancer
```

---

## Technology Stack

* HTML
* CSS
* Docker
* Nginx
* AWS ECS Fargate
* Amazon ECR
* Application Load Balancer
* CloudWatch
* Auto Scaling
* VPC Networking

---

## Project Structure

```text
portfolio/
│
├── index.html
├── style.css
├── Dockerfile
└── README.md
```

---

## Docker Configuration

Dockerfile:

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html

EXPOSE 80
```

---

## Build Docker Image

```bash
docker build -t portfolio .
```

Run locally:

```bash
docker run -p 8080:80 portfolio
```

Open:

```text
http://localhost:8080
```

---

## Push Container to Amazon ECR

Create repository:

```bash
aws ecr create-repository --repository-name portfolio
```

Login:

```bash
aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin ACCOUNT_ID.dkr.ecr.ap-south-1.amazonaws.com
```

Tag image:

```bash
docker tag portfolio:latest ACCOUNT_ID.dkr.ecr.ap-south-1.amazonaws.com/portfolio:latest
```

Push image:

```bash
docker push ACCOUNT_ID.dkr.ecr.ap-south-1.amazonaws.com/portfolio:latest
```

---

## ECS Deployment Steps

1. Create VPC and Public Subnets
2. Configure Internet Gateway and Route Tables
3. Create Security Groups
4. Create ECS Cluster
5. Create Task Definition
6. Create Application Load Balancer
7. Create ECS Service
8. Attach Target Group
9. Enable Auto Scaling
10. Test deployment

---

## Auto Scaling Configuration

Minimum Tasks:

```text
2
```

Maximum Tasks:

```text
6
```

Scaling Metric:

```text
CPU Utilization
```

Target:

```text
70%
```

---

## Security Groups

ALB Security Group:

```text
Inbound:
HTTP 80 -> Anywhere
```

Task Security Group:

```text
Inbound:
Port 80 -> ALB Security Group
```

---

## Monitoring

Monitor deployment using:

* CloudWatch Metrics
* ECS Service Metrics
* Target Group Health Checks
* Load Balancer Metrics

---

## Future Improvements

* HTTPS support
* Custom domain integration
* CI/CD pipeline
* Blue-Green deployment
* Infrastructure as Code using Terraform

---

## Learning Outcomes

This project demonstrates:

* Containerization
* AWS Networking
* ECS Fargate Deployment
* Auto Scaling
* Load Balancing
* Cloud Infrastructure Design
* Docker Workflows
* Cloud Monitoring

```
```

