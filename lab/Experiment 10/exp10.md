# Experiment 10: Orchestration using Docker Compose & Docker Swarm

**Name:** Nipun Agrawal
**SAP ID:** 500119472
**Course:** Containerization and DevOps Lab

## 📸 Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-28%20235415.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235514.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235523.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235541.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235556.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235608.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235623.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235633.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235645.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20235654.png)
## Objective

Understand container orchestration by moving from Docker Compose to Docker Swarm.
Learn how to:

* Deploy a stack
* Scale services
* Observe self-healing
* Manage multi-container applications

---

##  Theory

### Problem Statement

Running containers manually works for simple applications, but real-world apps:

* Have multiple services
* Need scaling
* Require automatic recovery

Docker Compose helps manage multi-container apps, but:

* ❌ No clustering
* ❌ No self-healing
* ❌ No load balancing

---

### What is Orchestration?

Orchestration = automatic management of containers

It provides:

* Scaling (increase/decrease containers)
* Self-healing (auto restart failed containers)
* Load balancing
* Service management

---

###  Progression Path

```
docker run → Docker Compose → Docker Swarm → Kubernetes
```

| Level      | Description                      |
| ---------- | -------------------------------- |
| docker run | Single container                 |
| Compose    | Multi-container (single machine) |
| Swarm      | Basic orchestration              |
| Kubernetes | Advanced orchestration           |

---

### Compose vs Swarm

| Feature        | Docker Compose | Docker Swarm |
| -------------- | -------------- | ------------ |
| Scope          | Single machine | Cluster      |
| Scaling        | Limited        | Built-in     |
| Self-healing   | ❌              | ✅            |
| Load balancing | ❌              | ✅            |
| Use case       | Development    | Production   |

---

##  Prerequisites

* Docker installed
* Docker Compose installed
* Swarm mode enabled
* Experiment 6 (WordPress + MySQL setup)

---

##  Practical Steps

### 🔹 Step 1: Stop Existing Containers

```bash
docker compose down -v
docker ps
```

---

### 🔹 Step 2: Initialize Swarm

```bash
docker swarm init
docker node ls
```

✔ Node becomes **Manager & Leader**

---

### 🔹 Step 3: Deploy Stack

```bash
docker stack deploy -c docker-compose.yml wpstack
```

✔ Creates services instead of containers

---

### 🔹 Step 4: Verify Deployment

```bash
docker service ls
docker service ps wpstack_wordpress
docker ps
```

---

### 🔹 Step 5: Access Application

Open in browser:

```
http://localhost:8080
```

✔ WordPress setup page appears

---

### 🔹 Step 6: Scale Application

```bash
docker service scale wpstack_wordpress=3
```

Verify:

```bash
docker service ls
docker service ps wpstack_wordpress
```

✔ Now 3 replicas running

---

### 🔹 Step 7: Test Self-Healing

```bash
docker ps | grep wordpress
docker kill <container-id>
docker service ps wpstack_wordpress
```

✔ Swarm automatically creates new container

---

### 🔹 Step 8: Remove Stack

```bash
docker stack rm wpstack
docker service ls
docker ps
```

✔ Cleanup completed

---

##  Analysis

### Key Observations

* Same Compose file works in Swarm
* Swarm uses **services instead of containers**
* Scaling is automatic
* Self-healing replaces failed containers
* Load balancing handled internally

---

##  Quick Commands

```bash
docker compose down -v
docker swarm init
docker stack deploy -c docker-compose.yml wpstack
docker service ls
docker service ps wpstack_wordpress
docker service scale wpstack_wordpress=3
docker kill <container-id>
docker stack rm wpstack
```

---

##  Result

* Stack deployed successfully
* Services verified
* Scaling tested
* Self-healing confirmed

---

##  Conclusion

Docker Swarm extends Docker Compose by adding:

* Orchestration
* Scaling
* Self-healing

It acts as a bridge between basic container usage and advanced tools like Kubernetes.

---
