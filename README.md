# Node.js App Deployment to Minikube via GitHub Actions 

![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white)
![NodeJS](https://img.shields.io/badge/node.js-6DA55F?style=for-the-badge&logo=node.js&logoColor=white)
![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/github%20actions-%232671E5.svg?style=for-the-badge&logo=githubactions&logoColor=white)

This repository contains a **CI/CD (Continuous Integration & Continuous Deployment)** lab focused on automating the deployment of a Node.js application into a local **Minikube** cluster using **GitHub Actions**.

## Project Overview
The automated workflow performs the following tasks:
1.  **Provisioning:** Sets up a Minikube environment on the GitHub Actions runner.
2.  **Containerization:** Builds a Docker image of the Node.js application based on the `Dockerfile`.
3.  **Orchestration:** Deploys the application to Kubernetes using a YAML manifest (`k8s-node-app.yaml`).
4.  **Exposure:** Creates a `NodePort` service to allow external access to the application.
5.  **Verification:** Validates the service availability and retrieves the Minikube URL.

## Tech Stack
* **Runtime:** Node.js 14
* **Framework:** Express.js
* **Containers:** Docker
* **Orchestrator:** Kubernetes (Minikube)
* **Automation:** GitHub Actions (`medyagh/setup-minikube`)

## Repository Structure
* `.github/workflows/`: CI/CD pipeline definition.
* `Dockerfile`: Configuration for building the container image.
* `server.js`: Basic Node.js "Hello World" application.
* `package.json`: Project dependencies and scripts.
* `k8s-node-app.yaml`: Kubernetes Deployment and Service definitions.

## Workflow Execution
Upon a `push` to the `main` branch, the `.github/workflows/deploy-to-minikube-github-actions.yaml` file is triggered:

```bash
# Key commands executed within the pipeline:
minikube start
docker build -t node-app:latest .
kubectl apply -f k8s-node-app.yaml
minikube service nodejs-app --url
