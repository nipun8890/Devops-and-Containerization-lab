# Containerization & DevOps Lab

## Student Details
 
* **Name:** Nipun Agrawal 
* **SAP ID:** 500119472
* **Batch:** B3 (CCVT)
## 📸 Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-21%20221220.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20221242.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20221314.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20221414.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20223544.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20223606.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20223628.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20223816.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20224528.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20224642.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20224720.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20224818.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20225949.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20225956.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20230004.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20230433.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20230441.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20230547.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20230904.png)
![Screenshot](Screenshots/Screenshot%202026-04-21%20233103.png)

# Lab – Experiment 6 
## Docker Run vs Docker Compose: Multi-Container Application Orchestration

---

## Lab Objectives

After completing this lab, students will be able to:

- Understand the relationship between `docker run` (imperative) and Docker Compose (declarative)
- Compare Docker Run flags with Docker Compose YAML
- Deploy single and multi-container applications
- Convert Docker Run commands to Docker Compose
- Manage volumes, networks, and environment variables
- Use Dockerfile with Docker Compose
- Deploy production-ready applications

---

## Prerequisites

- Docker installed and running  
- Basic knowledge of:
  - `docker run`
  - Port mapping
  - Volume mounting
  - Networking  
- YAML file format  
- Environment variables  

---

# Part A – Theory

## 1. Objective

Understand the relationship between Docker Run and Docker Compose.

---

## 2. Background Theory

### 2.1 Docker Run (Imperative Approach)

Docker Run creates and starts containers using command-line flags.

#### Common Options

```bash
-p              # Port mapping
-v              # Volume mounting
-e              # Environment variables
--network       # Network configuration
--restart       # Restart policy
--memory        # Memory limit
--cpus          # CPU limit
--name          # Container name
-d              # Detached mode
Advantages
Direct control
Quick testing
Suitable for simple containers
Disadvantages
Hard to manage multiple containers
Not reproducible
Error-prone
Not production-ready
Example
docker run -d \
  --name my-nginx \
  -p 8080:80 \
  -v ./html:/usr/share/nginx/html \
  -e NGINX_HOST=localhost \
  --restart unless-stopped \
  nginx:alpine
2.2 Docker Compose (Declarative Approach)

Docker Compose uses a YAML file to define services.

Advantages
Multi-container support
Reproducible
Easy lifecycle management
Built-in networking
Disadvantages
Requires YAML knowledge
No clustering
Example
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    container_name: my-nginx
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
    environment:
      NGINX_HOST: localhost
    restart: unless-stopped
3. Mapping: Docker Run vs Docker Compose
Docker Run	Docker Compose	Purpose
-p	ports	Port mapping
-v	volumes	Volume
-e	environment	Env variables
--name	container_name	Name
--network	networks	Network
--restart	restart	Restart
-d	up -d	Detached
4. Advantages of Docker Compose
Single command deployment
Reproducible configuration
Version control support
Service scaling
Automatic networking
Part B – Practical Tasks
Task 1: Single Container
Docker Run
docker run -d \
  --name lab-nginx \
  -p 8081:80 \
  -v $(pwd)/html:/usr/share/nginx/html \
  nginx:alpine

Check:

docker ps

Access:

http://localhost:8081

Cleanup:

docker stop lab-nginx
docker rm lab-nginx
Docker Compose
version: '3.8'

services:
  nginx:
    image: nginx:alpine
    container_name: lab-nginx
    ports:
      - "8081:80"
    volumes:
      - ./html:/usr/share/nginx/html

Run:

docker compose up -d
docker compose ps
docker compose down
Task 2: WordPress + MySQL
Docker Run
docker network create wp-net

docker run -d \
  --name mysql \
  --network wp-net \
  -e MYSQL_ROOT_PASSWORD=secret \
  -e MYSQL_DATABASE=wordpress \
  mysql:5.7

docker run -d \
  --name wordpress \
  --network wp-net \
  -p 8082:80 \
  -e WORDPRESS_DB_HOST=mysql \
  -e WORDPRESS_DB_PASSWORD=secret \
  wordpress:latest

Access:

http://localhost:8082

Cleanup:

docker stop wordpress mysql
docker rm wordpress mysql
docker network rm wp-net
Docker Compose
version: '3.8'

services:
  mysql:
    image: mysql:5.7
    container_name: wordpress_db
    environment:
      MYSQL_ROOT_PASSWORD: secret
      MYSQL_DATABASE: wordpress
    volumes:
      - mysql_data:/var/lib/mysql

  wordpress:
    image: wordpress:latest
    container_name: wordpress_app
    depends_on:
      - mysql
    ports:
      - "8082:80"
    environment:
      WORDPRESS_DB_HOST: mysql
      WORDPRESS_DB_PASSWORD: secret
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wp_data:/var/www/html

volumes:
  mysql_data:
  wp_data:

Run:

docker compose up -d
docker compose down -v
Part C – Conversion Tasks
Problem 1
docker run -d \
  --name webapp \
  -p 5000:5000 \
  -e APP_ENV=production \
  -e DEBUG=false \
  node:18-alpine
Solution
version: '3.8'

services:
  webapp:
    image: node:18-alpine
    container_name: webapp
    ports:
      - "5000:5000"
    environment:
      APP_ENV: production
      DEBUG: "false"
    restart: unless-stopped
Problem 2
version: '3.8'

services:
  postgres-db:
    image: postgres:15
    container_name: postgres-db
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - app-net

  backend:
    image: python:3.11-slim
    container_name: backend
    ports:
      - "8000:8000"
    environment:
      DB_HOST: postgres-db
      DB_USER: admin
      DB_PASS: secret
    depends_on:
      - postgres-db
    networks:
      - app-net

volumes:
  pgdata:

networks:
  app-net:
Best Practices
Use meaningful service names
Use .env files
Use named volumes
Avoid latest tag
Set resource limits
Add health checks
Key Takeaways
Docker Run → quick testing
Docker Compose → production use
YAML ensures reproducibility
Compose simplifies multi-container apps