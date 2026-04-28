# Experiment 11: Container Orchestration using Kubernetes

**Name:** Nipun Agrawal
**SAP ID:** 500119472
**Course:** Containerization and DevOps Lab

---
## 📸 Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-29%20004454.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004511.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004524.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004535.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004546.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004559.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004614.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004627.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004639.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004649.png)
![Screenshot](Screenshots/Screenshot%202026-04-29%20004702.png)
##  Objective

To understand Kubernetes as a container orchestration platform and perform:

* Deployment of applications
* Service exposure
* Scaling
* Self-healing

---

##  Theory

### Problem Statement

Docker Swarm provides basic orchestration but lacks:

* Advanced scheduling
* Auto-scaling
* Large ecosystem support

Modern applications require a more powerful orchestration platform.

---

### What is Kubernetes?

Kubernetes (K8s) is an open-source platform that automates:

* Deployment
* Scaling
* Management of containerized applications

---

### Key Features

* Declarative configuration using YAML
* Automatic scheduling
* Self-healing
* Auto-scaling
* Cloud-native support

---

### Core Concepts

| Docker Concept  | Kubernetes Equivalent | Meaning          |
| --------------- | --------------------- | ---------------- |
| Container       | Pod                   | Smallest unit    |
| Compose Service | Deployment            | Manages replicas |
| Load Balancer   | Service               | Exposes pods     |
| Replicas        | ReplicaSet            | Maintains copies |
| Machine         | Node                  | Runs pods        |

---

##  Prerequisites

* Docker installed
* Kubernetes cluster (Minikube/k3d)
* kubectl installed

---

##  Practical Implementation

---

### 🔹 Step 1: Start Kubernetes Cluster

```bash
minikube start
kubectl get nodes
```

---

### 🔹 Step 2: Create Deployment

```yaml
# wordpress-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress
spec:
  replicas: 2
  selector:
    matchLabels:
      app: wordpress
  template:
    metadata:
      labels:
        app: wordpress
    spec:
      containers:
      - name: wordpress
        image: wordpress:latest
        ports:
        - containerPort: 80
```

Apply:

```bash
kubectl apply -f wordpress-deployment.yaml
```

---

### 🔹 Step 3: Create Service

```yaml
# wordpress-service.yaml
apiVersion: v1
kind: Service
metadata:
  name: wordpress-service
spec:
  type: NodePort
  selector:
    app: wordpress
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30007
```

Apply:

```bash
kubectl apply -f wordpress-service.yaml
```

---

### 🔹 Step 4: Verify Deployment

```bash
kubectl get pods
kubectl get svc
```

---

### 🔹 Step 5: Access Application

```bash
minikube ip
```

Open in browser:

```
http://<minikube-ip>:30007
```

---

### 🔹 Step 6: Scale Deployment

```bash
kubectl scale deployment wordpress --replicas=4
kubectl get pods
```

---

### 🔹 Step 7: Self-Healing Test

```bash
kubectl get pods
kubectl delete pod <pod-name>
kubectl get pods
```

✔ Pod is automatically recreated

---

##  Swarm vs Kubernetes

| Feature      | Docker Swarm | Kubernetes |
| ------------ | ------------ | ---------- |
| Setup        | Easy         | Complex    |
| Scaling      | Manual       | Auto       |
| Self-healing | Basic        | Advanced   |
| Ecosystem    | Small        | Huge       |
| Industry use | Low          | High       |

---

##  Observations

* Kubernetes maintains desired state automatically
* Services provide stable networking
* Scaling is simple and effective
* Self-healing ensures high availability

---

##  Commands Cheat Sheet

```bash
kubectl apply -f file.yaml
kubectl get pods
kubectl get svc
kubectl get nodes
kubectl scale deployment <name> --replicas=N
kubectl delete pod <pod-name>
kubectl logs <pod-name>
kubectl describe pod <pod-name>
```

---

##  Result

* WordPress deployed successfully
* Service exposed via NodePort
* Scaling from 2 → 4 replicas achieved
* Self-healing verified

---

##  Conclusion

Kubernetes is a powerful orchestration tool that provides:

* Automatic scaling
* Self-healing
* Load balancing
* Declarative infrastructure

It is the **industry standard** for deploying modern applications.

---

##  Reference

Lab structure adapted from: 

---
