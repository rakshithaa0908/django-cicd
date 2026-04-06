# Deployment Steps for Django CI/CD Pipeline
This guide outlines how to automate build and deployment of a Django application using Jenkins, Docker, Docker Hub, and Kubernetes on AWS.

---

## 1. AWS Setup

### Launch 2 EC2 instances
- AMI: `Ubuntu 22.04 LTS`
- Instance Type: `m7i-flex.large`
- Key pair: `mykey`
- Auto assign public IP: enabled
- Security group: Allow all traffic ⚠️ For demo purposes only — restrict in production- Rename instances:
    - master – Jenkins, Docker, Kubernetes
    - slave – Kubernetes worker

---

## 2. Connect to the EC2 Instance

### Login to Server
`$ sudo su -`

### Install Required Tools
On the master node, install the following:

**Jenkins**
```
$ apt install jenkins -y
$ systemctl start jenkins
$ systemctl status jenkins
```
**Docker**
```
$ apt install docker.io -y
$ systemctl start docker
$ systemctl status docker
```
**Kubernetes**
```
$ apt install -y kubectl kubeadm kubelet
$ kubeadm init
```
Allow Jenkins to run Docker commands:
```
$ usermod -aG docker jenkins
$ systemctl restart jenkins
```
Access Jenkins at:
```
http://master-public-ip:8080
```
---
## 3. Create Jenkins Pipeline

### Fork Repository
Fork the repository to your GitHub account:
[https://github.com/swathis10/django-notes-app](https://github.com/swathis10/django-notes-app)

### Clone Repository
```
$ git clone https://github.com/your-username/django-notes-app.git
$ cd django-notes-app
```

### Create a Jenkins pipeline job
Add stages for:
- Clone code from GitHub
- Build Docker image using Dockerfile
- Push image to Docker Hub
- Deploy application to Kubernetes using kubectl
---

## 4. Docker Image Build & Push
Jenkins handles the build and push automatically via the pipeline.
Ensure the following credentials are stored in Jenkins:
- **Docker Hub username and password** — used to push the image

Verify the image was pushed successfully by checking Docker Hub after the pipeline runs.

## 5. Kubernetes Deployment
### Add Kubernetes Config as Jenkins Credential
Add your kubeconfig file as a secret in Jenkins credentials (ID: `k8`).
This allows Jenkins to authenticate with the Kubernetes cluster.

### Apply Kubernetes Manifests
The repository already includes:
- `deployment.yaml` — defines the app deployment
- `service.yaml` — exposes the app via NodePort

Jenkins deploys them automatically using:
```
$ kubectl apply -f deployment.yaml
$ kubectl apply -f service.yaml
```

## 6.Access Application
- Get service port: `$ kubectl get svc`
- Open in browser: `http://master-public-dns:node-port`
- If the setup is correct, the web application will be accessible from the browser.
---
> ✅ Deployment complete. The Django application is now running on your Kubernetes cluster.
