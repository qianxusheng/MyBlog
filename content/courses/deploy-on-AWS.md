---
title: "Deploying Full-Stack Applications on AWS: A Practical Guide"
date: 2025-12-12
description: "Learn how to deploy a full-stack application on AWS using EC2, S3, Nginx, and GitHub Actions for CI/CD automation"
tags: ["AWS", "DevOps", "Deployment", "EC2", "S3", "CI/CD", "Nginx"]
---

**My Project Repository**: [https://github.com/qianxusheng/PA-LawSearch](https://github.com/qianxusheng/PA-LawSearch)

## Core Deployment Steps

1. **Launch EC2 Instance**
   - Provision a cloud server (EC2 instance) to host your backend services

2. **SSH Connection**
   - Connect to the EC2 instance via SSH using its public IP address

3. **Environment Setup**
   - Install required dependencies: Python, Elasticsearch, Redis, and other runtime dependencies
   - Configure the application environment

4. **Service Configuration with systemd**
   - Create systemd service files to manage backend services
   - Configure services to run as background processes
   - Expose necessary ports for frontend communication

5. **Service Management**
   - Write systemd scripts for easy service restart and management
   - Enable services to auto-start on system boot

6. **Frontend Hosting**
   - Create an S3 bucket to host static frontend assets
   - Configure S3 for static website hosting

## Key Learning Areas

### 1. Linux System Administration
- Basic command-line operations (navigation, file management, permissions)
- Process management and systemd service configuration
- Ubuntu-specific package management (apt)

### 2. AWS Infrastructure
- EC2 instance configuration (instance type, storage, AMI selection)
- Security Groups and network access control
- IAM roles and permissions management

### 3. CI/CD with GitHub Actions
- Configure GitHub repository secrets (AWS access keys, credentials)
- Set up automated deployment workflows
- Implement automatic application updates and service restarts on EC2
- backend you need to restart the services
- frontend you need to rebuild the frontend application,to generate new static files and then update the static files that you uploaded on the S3 before

### 4. Network Architecture & Security
- **CORS (Cross-Origin Resource Sharing)**: Handle browser security restrictions when frontend and backend are on different domains
- **Nginx as Reverse Proxy**: 
  - Acts as a middleman between client and backend services
  - Unifies frontend and backend under a single domain to avoid CORS issues
  - Provides SSL/TLS termination

### 5. Security Best Practices
- **Internal Communication**: Backend ↔ Elasticsearch can use HTTP within the private network
- **External Communication**: Frontend ↔ Backend must use HTTPS for encrypted client-server communication
- Implement proper SSL/TLS certificates for production environments

### 6. Environment Configuration Management
- **Local vs Production Environment Differences**:
  - **Development (Local)**: Frontend typically runs on `localhost:3000`, backend on `localhost:8000`
  - **Production (AWS)**: Services run on different domains/ports (e.g., frontend on S3, backend on EC2)
- **Configuration Files**: Use environment variables (`.env` files) to manage different endpoints:
  - Local: `API_URL=http://localhost:8000`
  - Production: `API_URL=https://api.yourdomain.com`
- **Common Pitfalls**:
  - Hardcoding localhost URLs in production builds
  - Forgetting to update API endpoints when deploying
  - Mixed HTTP/HTTPS protocol issues causing connection failures