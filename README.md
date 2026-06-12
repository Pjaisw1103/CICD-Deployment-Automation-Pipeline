# 🚀 Automated CI/CD Deployment Pipeline for Todo Application

This repository houses the infrastructure configurations for a multi-service Todo Application. It decouples the **Dockerization Setup** (the container environment) from the **CI/CD Pipeline** (the automation engine) to maintain a clean DevOps architecture.

---

## 📦 Application Component Source

This repository automates and orchestrates deployment for the following external sub-modules:
* **Frontend UI:** [devopsinsiders/ReactTodoUIMonolith](https://github.com/devopsinsiders/ReactTodoUIMonolith.git) (ReactJS)
* **Backend API:** [devopsinsiders/PyTodoBackendMonolith](https://github.com/devopsinsiders/PyTodoBackendMonolith.git) (Python API)

---

## 🐋 1. Dockerization Strategy & Configuration

The application ecosystem uses independent container environments defined within this repository. This guarantees that the applications run exactly the same way in local development as they do on production servers.

### 🖥️ Frontend Docker Environment
* **Approach:** Multi-stage Docker build.
* **Stage 1 (Build):** Spins up a Node.js lightweight container to install NPM packages and compile production-ready static assets.
* **Stage 2 (Production):** Drops the heavy Node modules and copies only the compiled HTML/JS build into a super-lightweight **Nginx Alpine** image to serve the frontend securely and instantly.

### ⚙️ Backend Docker Environment
* **Approach:** Optimized Python base layout.
* **Execution:** Installs application dependencies via `pip` out of a cached layer strategy to speed up consecutive image builds, exposing the required WSGI/ASGI application ports.

---

## 🔄 2. CI/CD Pipeline Workflow & Breakdown

The automation pipeline acts as the runtime scheduler. It handles testing, packaging, and shipping the code automatically without any human intervention.

### Pipeline Execution Stages:
* **Trigger Event:** Executed autonomously on any code push or pull_request merging into the main branch.
* **Environment Provisioning:** Automatically spins up a fresh runner agent, maps secrets securely, and injects runtime configurations.
* **Build Execution:** Calls the underlying Dockerfiles dynamically, injecting the production `BACKEND_API_URL` variable as build arguments into the React image.
* **Artifact Shipping:** Authenticates into Docker Hub using encrypted repo secrets and ships the tagged production images.
* **Target Deployment:** Connects to the host environment hosting the application container engine, runs a rolling update, and replaces old container workloads seamlessly.

---

## 🚀 How to Run Locally

### Prerequisites
* Docker Desktop installed.

### Step-by-Step Local Deployment

1. **Clone this Automation Infrastructure repository:**
   ```bash
   git clone [https://github.com/Pjaisw1103/CICD-Deployment-Automation-Pipeline.git](https://github.com/Pjaisw1103/CICD-Deployment-Automation-Pipeline.git)
   cd CICD-Deployment-Automation-Pipeline
