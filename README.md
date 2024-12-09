# CI/CD Pipeline for Node.js Application

This repository demonstrates a CI/CD pipeline for a Node.js application using GitHub Actions, Docker, and Kubernetes.

## Features
1. **Automated Testing**: Runs tests on each pull request.
2. **Docker Integration**: Builds and pushes a Docker image.
3. **Kubernetes Deployment**: Deploys the application to a Kubernetes cluster.
4. **Notifications**: Provides feedback on deployment status.

## How It Works
1. **CI Stage**: Tests are executed on every pull request.
2. **CD Stage**: On push to `main`, a Docker image is built and deployed to Kubernetes.
3. **Notifications**: Deployment success or failure is logged.

### Prerequisites
- Node.js installed locally.
- Kubernetes cluster set up and `kubectl` configured.
- Docker Hub account for storing Docker images.

### Setup
1. Clone the repository.
2. Add the required secrets to GitHub.
3. Modify Kubernetes YAML files with your configuration.
4. Push code to trigger the pipeline.

### Folder Structure
- `Dockerfile`: Instructions for building the Docker image.
- `deployment.yaml`: Kubernetes deployment configuration.
- `service.yaml`: Kubernetes service configuration.
