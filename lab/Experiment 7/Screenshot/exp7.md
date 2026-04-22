# Containerization & DevOps Lab  

## Experiment 7  
### CI/CD using Jenkins, GitHub and Docker Hub  

---

## Student Details

- **Name:** Nipun Agrawal
- **SAP ID:** 500119472
- **Batch:** B3 (CCVT)  

---
## 📸 Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-01%20085830.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20085839.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20085849.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20085917.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20085934.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20085953.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20090001.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20090010.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20091342.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20091353.png)

![Screenshot](Screenshots/Screenshot%202026-04-01%20091408.png)

![Screenshot](Screenshots/Screenshot%202026-04-22%20225925.png)

![Screenshot](Screenshots/Screenshot%202026-04-22%20231324.png)

## 1. Aim

To design and implement a complete CI/CD pipeline using Jenkins, integrating source code from GitHub, and building and pushing Docker images to Docker Hub.

---

## 2. Objectives

- Understand CI/CD workflow using Jenkins  
- Create GitHub repository with application + Jenkinsfile  
- Build Docker images from source code  
- Store Docker Hub credentials securely in Jenkins  
- Automate build & push using webhooks  
- Use host Docker engine inside Jenkins  

---

## 3. Theory

### 3.1 What is Jenkins?

Jenkins is a web-based automation server used to:

- Build applications  
- Test code  
- Deploy software  

**Features:**
- GUI dashboard  
- Plugin ecosystem  
- Pipeline as Code (Jenkinsfile)  

---

### 3.2 What is CI/CD?

**Continuous Integration (CI):**
- Code is automatically built and tested after every commit  

**Continuous Deployment (CD):**
- Built artifacts are automatically delivered/deployed  

---

### 3.3 Workflow Overview


Developer → GitHub → Webhook → Jenkins → Build → Docker Hub


---

## 4. Prerequisites

- Docker & Docker Compose installed  
- GitHub account  
- Docker Hub account  
- Basic Linux commands  

---

# Part A – GitHub Setup

## 5.1 Create Repository

Create a repo named:


my-app


---

## 5.2 Project Structure


my-app/
├── app.py
├── requirements.txt
├── Dockerfile
├── Jenkinsfile


---

## 5.3 Application Code

### app.py

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Hello from CI/CD Pipeline!"

app.run(host="0.0.0.0", port=80)
requirements.txt
flask
5.4 Dockerfile
FROM python:3.10-slim

WORKDIR /app
COPY . .

RUN pip install -r requirements.txt

EXPOSE 80
CMD ["python", "app.py"]
Build Process
Code pushed to GitHub
Jenkins pulls repo
Dockerfile builds environment
Dependencies installed
App packaged as Docker image
5.5 Jenkinsfile
pipeline {
    agent any

    environment {
        IMAGE_NAME = "your-dockerhub-username/myapp"
    }

    stages {

        stage('Clone Source') {
            steps {
                git 'https://github.com/your-username/my-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME:latest .'
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
                    sh 'echo $DOCKER_TOKEN | docker login -u your-dockerhub-username --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push $IMAGE_NAME:latest'
            }
        }
    }
}
Jenkinsfile Explanation
pipeline → defines workflow
agent any → runs anywhere
environment → reusable variables
stages → pipeline steps
git → clone repo
docker build → create image
withCredentials → secure login
docker push → upload image
Part B – Jenkins Setup
6.1 Docker Compose File
version: '3.8'

services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    restart: always
    ports:
      - "8082:8080"
      - "50001:50000"
    volumes:
      - jenkins_home:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
    user: root

volumes:
  jenkins_home:
6.2 Start Jenkins
docker compose up -d

Access:

http://localhost:8082
6.3 Unlock Jenkins
docker exec -it jenkins cat /var/jenkins_home/secrets/initialAdminPassword
6.4 Initial Setup
Install suggested plugins
Create admin user
Complete setup
Part C – Jenkins Configuration
7.1 Add Docker Hub Credentials

Path:

Manage Jenkins → Credentials → Add Credentials
Type: Secret Text
ID: dockerhub-token
7.2 Create Pipeline Job
New Item → Pipeline
Pipeline from SCM
Git repo URL
Script path: Jenkinsfile
Part D – GitHub Webhook
8.1 Configure Webhook
Settings → Webhooks → Add Webhook

Payload URL:

http://<your-server-ip>:8082/github-webhook/
Part E – Execution Flow
Step 1: Code Push

Developer pushes code

Step 2: Webhook

GitHub notifies Jenkins

Step 3: Jenkins Pipeline
Clone
Build
Login
Push
Step 4: Artifact Ready

Docker image available on Docker Hub

Role of Same Host Agent

Mounted path:

/var/run/docker.sock
Effect:
Jenkins uses host Docker
No extra agent required
Simple setup
Jenkins Pipeline Concept
withCredentials Example
withCredentials([string(credentialsId: 'dockerhub-token', variable: 'DOCKER_TOKEN')]) {
    sh 'echo $DOCKER_TOKEN | docker login -u username --password-stdin'
}
Why Important:
Prevents exposing secrets
Keeps pipeline secure
Safe for GitHub
Observations
Jenkins simplifies CI/CD
GitHub stores code + pipeline
Docker ensures consistency
Webhooks automate builds
Credentials improve security
Result
CI/CD pipeline successfully implemented
Code → Jenkins → Docker → Docker Hub
Key Takeaways
Jenkins is GUI + code-based
Always use credentials (no hardcoding)
Webhooks enable automation
Docker socket enables host access