# 🚀 k8s-manifests-local-chatapp

Kubernetes manifests for deploying a **full-stack chat application** on a local Docker Desktop (Windows) environment with Kubernetes enabled on a single-node cluster.

-----

## 📋 Table of Contents

- [Overview](#overview)
- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Deployment](#deployment)
- [Accessing the Application](#accessing-the-application)
- [Teardown](#teardown)
- [License](#license)

-----

## Overview

This repository contains all the Kubernetes manifest files needed to spin up a full-stack chat application locally. The stack includes:

- **Frontend** – Web UI served via a dedicated deployment and service
- **Backend** – REST/WebSocket API server
- **MongoDB** – Persistent database with a PersistentVolume and PersistentVolumeClaim
- **Ingress** – NGINX Ingress Controller to route external traffic to services
- **Secrets** – Kubernetes secrets for sensitive configuration (e.g. DB credentials)

All resources are scoped to the `k8s-chatapp` namespace.

-----

## Architecture

```
                        ┌─────────────────────────────────────────┐
                        │           k8s-chatapp Namespace          │
                        │                                          │
  Browser ──► Ingress ──►  Frontend Pod  ──►  Backend Pod         │
                        │                        │                 │
                        │               MongoDB Service            │
                        │                    │                     │
                        │              MongoDB Pod                 │
                        │            (PV + PVC mounted)            │
                        └─────────────────────────────────────────┘
```

-----

## Prerequisites

Ensure the following are installed and running before deploying:

|Tool                                                             |Version|Notes                        |
|-----------------------------------------------------------------|-------|-----------------------------|
|[Docker Desktop](https://www.docker.com/products/docker-desktop/)|Latest |Enable Kubernetes in settings|
|[kubectl](https://kubernetes.io/docs/tasks/tools/)               |v1.25+ |Kubernetes CLI               |
|NGINX Ingress Controller                                         |Latest |Required for ingress routing |

### Enable Kubernetes on Docker Desktop

1. Open Docker Desktop → **Settings** → **Kubernetes**
1. Check **Enable Kubernetes**
1. Click **Apply & Restart**

### Install NGINX Ingress Controller

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.0/deploy/static/provider/cloud/deploy.yaml
```

-----

## Project Structure

```
k8s-manifests-local-chatapp/
├── k8s-manifests/
│   ├── namespace.yaml            # Namespace: k8s-chatapp
│   ├── secrets.yaml              # Kubernetes Secrets (DB credentials, etc.)
│   ├── mongodb-pv.yaml           # PersistentVolume for MongoDB
│   ├── mongodb-pvc.yaml          # PersistentVolumeClaim for MongoDB
│   ├── mongodb-deployment.yaml   # MongoDB Deployment
│   ├── mongodb-service.yaml      # MongoDB ClusterIP Service
│   ├── backend-deployment.yaml   # Backend API Deployment
│   ├── backend-service.yaml      # Backend ClusterIP Service
│   ├── frontend-deployment.yaml  # Frontend Deployment
│   ├── frontend-service.yaml     # Frontend ClusterIP Service
│   └── ingress.yaml              # NGINX Ingress rules
├── .env                          # Environment variables (local use only)
├── .gitignore
├── LICENSE
└── README.md
```

-----

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/swapnilmali101/k8s-manifests-local-chatapp.git
cd k8s-manifests-local-chatapp
```

### 2. Configure Environment Variables

Copy or review the `.env` file and update any values as needed. Sensitive values should be base64-encoded and placed in `secrets.yaml`.

```bash
# Example: base64 encode a secret value
echo -n "your-password" | base64
```

-----

## Deployment

Apply all manifests in the following order from the `k8s-manifests/` directory:

```bash
cd k8s-manifests
```

### Step 1 – Create Namespace

```bash
kubectl create -f namespace.yaml
kubectl get ns
```

### Step 2 – Create Persistent Storage for MongoDB

```bash
kubectl apply -f mongodb-pv.yaml
kubectl apply -f mongodb-pvc.yaml
kubectl get pvc,pv -n k8s-chatapp
```

### Step 3 – Deploy MongoDB

```bash
kubectl apply -f mongodb-deployment.yaml
kubectl apply -f mongodb-service.yaml
```

### Step 4 – Apply Secrets

```bash
kubectl apply -f secrets.yaml
```

### Step 5 – Deploy Backend

```bash
kubectl apply -f backend-deployment.yaml
kubectl apply -f backend-service.yaml
```

### Step 6 – Deploy Frontend

```bash
kubectl apply -f frontend-deployment.yaml
kubectl apply -f frontend-service.yaml
```

### Step 7 – Apply Ingress

```bash
kubectl apply -f ingress.yaml
```

### Verify Everything Is Running

```bash
kubectl get pods -n k8s-chatapp
kubectl get svc -n k8s-chatapp
kubectl get ingress -n k8s-chatapp
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx
```

All pods should show `Running` status before proceeding.

-----

## Accessing the Application

### Via Ingress (Recommended)

Forward traffic from the NGINX Ingress Controller to your local machine:

```bash
kubectl port-forward svc/ingress-nginx-controller -n ingress-nginx 80:80
```

Then open your browser at: <http://localhost>

### Direct Backend Port-Forward (for debugging)

```bash
kubectl port-forward svc/backend 5001:5001 -n k8s-chatapp
```

Backend API available at: <http://localhost:5001>

-----

## Teardown

To remove all deployed resources and clean up the namespace:

```bash
kubectl delete namespace k8s-chatapp
kubectl get ns
```

> ⚠️ This will delete **all** resources in the `k8s-chatapp` namespace, including PersistentVolumeClaims and their data.

-----

## License

This project is licensed under the [MIT License](LICENSE).