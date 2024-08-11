# webapp-k8s-deployment

## Introduction
This is an open-source webapp for a teck-challenge:

- Choose an open source webapp project from Github
- Containerize the webapp project
- Build helm charts to deploy to a Kubernetes cluster (minikube or kind can be used locally for testing)
- Create a CI/CD pipeline/workflow for the webapp project to be build, run tests & deploy to K8s environment
- The CI pipeline/workflow will include anything that is relevant to the webapp project
- Include README.MD on how to test solution

## Prerequisites
- Docker
- Kubernetes (Minikube)
- Helm

## Setup Instructions

### Build and Run Docker Container
#### Firs of all cd to the dockerfile directory and build the image from it and run a container from image

```bash
docker build -t myname/webapp .
docker run -p 3000:3000 myname/yourwebapp
```
### Build Helm Charts to Deploy to Kubernetes
```bash
helm create webapp-chart
```
1-Modify the templates in helm/templates.
2-Update the values.yaml file with necessary values like image repository and tag
```bash
image:
  repository: myname/webapp
  tag: latest
service:
  type: NodePort
  port: 3000
```
3- Now deploy it to minikube:

```bash
helm install webapp ./webapp-chart
```
4- Verify Deployment:
```bash
kubectl get pods
kubectl get svc
```

### Create a CI/CD Pipeline/Workflow

- Create a .github/workflows/ci-cd.yml file in your repository.
- Define jobs for building the Docker image, running tests, and deploying to Kubernetes:
```bash
name: CI/CD Pipeline

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v1
    - name: Build Docker Image
      run: docker build -t myname/webapp .
    - name: Push Docker Image
      run: docker push myame/webapp

  deploy:
    needs: build
    runs-on: ubuntu-latest
    steps:
    - name: Set up Kubectl
      uses: azure/setup-kubectl@v1
    - name: Deploy to Kubernetes
      run: helm upgrade --install webapp ./webapp-chart
```

### Testing:
After deployment, visit `http://<minikube-ip>:<nodeport>` to see the running webapp


