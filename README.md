# Cosmocloud Helm Chart: `cosmocloud-deploy`

This repository contains the Helm Chart `cosmocloud-deploy` for deploying three applications as part of a unified setup:
- **Backend**
- **Frontend**
- **Redis Database**

## Features
- Deploys each application as a **Kubernetes Deployment** with 1 replica.
- Exposes the services using **Kubernetes Services** with appropriate configurations.
- Supports namespace isolation (default: `default`).
- Includes environment variable management for inter-service communication.

## Applications and Configuration

### 1. Backend Service
- **Image**: `shreybatra/sample-backend`
- **Environment Variable**: `REDIS_URI=redis://redis-svc:6379`
- **Service**:
  - **Type**: `ClusterIP`
  - **Name**: `backend-svc`
  - **Port**: `8000`

### 2. Frontend Service
- **Image**: `shreybatra/sample-frontend`
- **Environment Variable**: `BACKEND_URL=http://backend-svc:8000`
- **Service**:
  - **Type**: `NodePort`
  - **Name**: `frontend-svc`
  - **Port**: `5173`
  - **NodePort**: `31000`

### 3. Redis Service
- **Image**: `redis`
- **Service**:
  - **Type**: `ClusterIP`
  - **Name**: `redis-svc`
  - **Port**: `6379`

## Prerequisites
- **Helm**: Ensure Helm is installed and configured.
- **Minikube**: A running Minikube cluster.
- **kubectl**: To interact with the cluster.

## Deployment Steps

### 1. Install Required Tools
Ensure Helm, Minikube, and kubectl are installed on your system.

### 2. Setup Minikube
Start and configure Minikube.
```bash
minikube start
minikube status
```
Verify the cluster setup:
```bash
kubectl cluster-info
kubectl get nodes
```

### 3. Deploy the Helm Chart
Use the following command to install the `cosmocloud-deploy` Helm Chart:
```bash
helm install testapp cosmocloud-deploy --atomic --timeout 60s
```

### 4. Verify Deployment
Check the deployments and services to ensure they are running correctly:
```bash
kubectl get deployments
kubectl get services
```

## Folder Structure
```
cosmocloud-deploy/
  |- templates/
  |    |- backend-deployment.yaml
  |    |- backend-service.yaml
  |    |- frontend-deployment.yaml
  |    |- frontend-service.yaml
  |    |- redis-deployment.yaml
  |    |- redis-service.yaml
  |- values.yaml
  |- Chart.yaml
```

## Testing
The deployment will be automatically tested using the following command:
```bash
helm install testapp cosmocloud-deploy --atomic --timeout 60s
```
## Snapsots


![image](https://github.com/user-attachments/assets/71267449-78da-46d1-a920-f367334275f8)
![image](https://github.com/user-attachments/assets/a2363606-6ef7-4007-926b-90efba47169e)
![image](https://github.com/user-attachments/assets/2e3e38fa-b918-40f3-bacd-da73e5937ef8)
![image](https://github.com/user-attachments/assets/ebe58d65-8cf0-48f6-bfb6-fbde05556be4)
![image](https://github.com/user-attachments/assets/a62ac0f0-967c-4a2b-94a7-b26248cf1be6)











