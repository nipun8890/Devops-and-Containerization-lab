# Containerization and DevOps Lab  
## Experiment – 1  
### Introduction to Docker and Containerization

---

### Name: Nipun Agrawal  
### Roll No: R2142230048  
### SAP ID: 500119472
### Course: Containerization and DevOps Lab  

---

## Aim
To understand the concept of containerization and Docker, install Docker on the system, run basic Docker commands, and study the difference between Docker containers and virtual machines.

---

## Objectives
1. To understand what containerization is.
2. To install Docker on the system.
3. To run a basic Docker container.
4. To study the difference between containers and virtual machines.

---

## Theory

### What is Containerization?
Containerization is a lightweight virtualization technique that packages an application along with its dependencies into a single unit called a **container**. This ensures that the application runs consistently across different environments.

---

### Docker
Docker is an open-source containerization platform that allows developers to build, ship, and run applications inside containers. Docker containers share the host operating system kernel, making them fast and resource-efficient.

---

### Containers vs Virtual Machines

| Feature | Containers | Virtual Machines |
|------|-----------|----------------|
| OS Kernel | Shared | Separate |
| Startup Time | Very Fast | Slow |
| Resource Usage | Low | High |
| Size | Lightweight | Heavy |

---

## System Requirements

### Hardware Requirements
- 64-bit system
- Minimum 4 GB RAM
- Virtualization enabled in BIOS

### Software Requirements
- Windows 10 / Windows 11
- Docker Desktop
- VS Code
- Git

---

## Procedure

### Step 1: Install Docker
Download and install Docker Desktop from the official Docker website. After installation, start Docker Desktop.

---

### Step 2: Verify Docker Installation
Open terminal or command prompt and run:

```bash
docker --version
