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
```bash
docker build -t yourusername/yourwebapp .
docker run -p 3000:3000 yourusername/yourwebapp
