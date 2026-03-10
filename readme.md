# Django CI/CD Pipeline

This project demonstrates an automated CI/CD pipeline for deploying a Django web application using Jenkins, Docker, and Kubernetes. The pipeline builds a Docker image, pushes it to Docker Hub, and deploys the application to a Kubernetes cluster.

---

## Concepts

### Technologies Used

- Jenkins
- Docker
- Kubernetes
- Docker Hub
- Django
- AWS EC2
- Git
- GitHub

### Jenkins
An automation server used to implement continuous integration and continuous deployment pipelines.

### Docker
A containerization platform used to package the Django application and its dependencies into portable images.

### Kubernetes
A container orchestration system used to deploy, scale, and manage the application containers.

## CI/CD Pipeline Workflow

- Developer pushes code to GitHub
- Jenkins pipeline is triggered
- Docker image is built using the Dockerfile
- Image is pushed to Docker Hub
- Jenkins deploys the application to Kubernetes
- Kubernetes exposes the application using a NodePort service

### Key Features
- Automated CI/CD pipeline for a Django application
- Docker image build and push to Docker Hub
- Kubernetes-based deployment using Jenkins
- Centralized credential management
- Scalable and repeatable deployment process

### Limitations
- Requires preconfigured Jenkins and Kubernetes setup
- NodePort service exposure depends on EC2 availability
- Designed for learning and demonstration purposes

---

## Deployment Steps

Full deployment instructions:  
See full deployment instructions [here](docs/deployment-steps.md)

---

## Project Structure
```
django-cicd/
│
├── docs/
│ ├── deployment-steps.md 
│ └── screenshots/
│ 	├── stage_view.png 
│ 	├── dockerhub.png
│ 	├── web_application.png
│ 	└── architecture.png # Architecture diagram
├── notesapp/
│ ├── deployment.yaml
│ ├── service.yaml
├── Dockerfile
├── Jenkinsfile
├── manage.py
├── README.md
├── requirements.txt 
└── LICENSE 
```

---

## Architecture Diagram

**Django CI/CD – Web Application Architecture**  
![Architecture](docs/screenshots/architecture.png)

---

## Screenshots

**Jenkins Pipeline Stage View**  
![Stage View](docs/screenshots/stage_view.png)

**Docker Image on Docker Hub**  
![Docker Hub](docs/screenshots/dockerhub.png)

**Django Web Application**  
![Web Application](docs/screenshots/web_application.png)

---

## My Contribution

- Implemented Jenkins CI/CD pipeline
- Containerized the Django application using Docker
- Configured Docker Hub image push
- Deployed the application to Kubernetes using Jenkins

---

## License

MIT License. See `LICENSE` file for details.

