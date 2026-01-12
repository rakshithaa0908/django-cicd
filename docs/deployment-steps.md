# Deployment Steps for Django CI/CD Pipeline

This guide outlines how to automate build and deployment of a Django application using Jenkins, Docker, Docker Hub, and Kubernetes on AWS.
---

## 1. AWS Setup

### Launch 2 EC2 instances
- AMI: `Ubuntu 22.04 LTS`
- Instance Type: `m7i-flex.large`
- Key pair: `mykey`
- Auto assign public IP: enabled
- Security group: allow all traffic(for demo purpose)
- Rename instances:
    - master – Jenkins, Docker, Kubernetes
    - slave – Kubernetes worker

---

## 2. Connect to the EC2 Instance

### Login to Server
`$ sudo su -`

### Install Required Tools
On the master node, install:
Jenkins
Docker
Kubernetes (kubectl, kubeadm, kubelet)
Allow Jenkins to run Docker:
```
usermod -aG docker jenkins
```
Access Jenkins:
```
http://master-public-ip:8080
```

## 3. Create Jenkins Pipeline

### Fork Repository
`https://github.com/swathis10/django-notes-app`

### Create a Jenkins pipeline job
Add stages for:
- Clone code
- Build Docker image
- Push image to Docker Hub
---

## 4. Docker Image Build & Push
- Build image using Dockerfile
- Push image to Docker Hub using Jenkins credentials

## 5. Kubernetes Deployment

### Add Kubernetes config as Jenkins secret (k8)
Create:
```
deployment.yaml
service.yaml(NodePort)
```
Deploy using Jenkins pipeline with `kubectl apply`

## 6.Access Application
- Get service port: `$ kubectl get svc`
- Open in browser: `$ http://master-public-dns:node-port`
- If the setup is correct, the web application will be accessible from the browser.
---
