# Containerization & DevOps Lab

## 📌 Student Details

* **Name:** Nipun Agrawal 
* **SAP ID:** 500119472
* **Batch:** B3 (CCVT)

---

##  Lab Experiment 5

### Data Persistence, Volumes, Environment Variables, Networking, Logs & Monitoring

---

##  Objectives

* Understand Docker data persistence using anonymous, named, and bind mounts
* Manage environment variables and `.env` files
* Inspect container logs, processes, and resource usage
* Create and use Docker networks
* Apply monitoring and cleanup commands

---

##  Prerequisites

* Docker installed and running
* Basic knowledge of:

  * `docker run`
  * `docker volume`
  * `docker exec`
  * `docker inspect`
  * Linux commands

---

#  Part 1 — Volumes & Data Persistence

### 1. Without Volume (Data Lost)

```bash
docker run -it --name test-container ubuntu /bin/bash

# Inside container
echo "Hello World" > /data/message.txt
cat /data/message.txt
exit
```

---

### 2. Anonymous Volume

```bash
docker run -d -v /app/data --name web1 nginx
docker volume ls
```

---

### 3. Named Volume (Recommended)

```bash
docker volume create mydata
docker run -d -v mydata:/app/data --name web2 nginx

docker volume ls
docker volume inspect mydata
```

---

### 4. Bind Mount (Host ↔ Container)

```bash
mkdir -p ~/myapp-data

docker run -d -v ~/myapp-data:/app/data --name web3 nginx

echo "From Host" > ~/myapp-data/host-file.txt

docker exec web3 cat /app/data/host-file.txt
```

---

### 5. MySQL Persistent Storage

```bash
docker run -d \
  --name mysql-db \
  -v mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  mysql:8.0
```

```bash
docker stop mysql-db
docker rm mysql-db

docker run -d \
  --name new-mysql \
  -v mysql-data:/var/lib/mysql \
  -e MYSQL_ROOT_PASSWORD=secret \
  mysql:8.0
```

---

#  Part 2 — Bind Mount Config Files

```bash
mkdir -p ~/nginx-config

echo 'server {
    listen 80;
    server_name localhost;
    location / {
        return 200 "Hello from mounted config!";
    }
}' > ~/nginx-config/nginx.conf
```

```bash
docker run -d \
  --name nginx-custom \
  -p 8080:80 \
  -v ~/nginx-config/nginx.conf:/etc/nginx/conf.d/default.conf \
  nginx
```

```bash
curl http://localhost:8080
```

---

#  Part 3 — Volume Management

```bash
docker volume create app-volume
docker volume inspect app-volume
```

```bash
docker volume prune
docker volume rm volume-name
```

```bash
docker cp local-file.txt container-name:/path/in/volume
```

---

#  Part 4 — Environment Variables

### Single Variable

```bash
docker run -d \
  --name app1 \
  -e DATABASE_URL="postgres://user:pass@db:5432/mydb" \
  -e DEBUG="true" \
  -p 3000:3000 \
  my-node-app
```

---

### Multiple Variables

```bash
docker run -d \
  -e VAR1=value1 \
  -e VAR2=value2 \
  -e VAR3=value3 \
  my-app
```

---

### Using `.env` File

```bash
echo "DATABASE_HOST=localhost" > .env
echo "DATABASE_PORT=5432" >> .env
echo "API_KEY=secret123" >> .env
```

```bash
docker run -d \
  --env-file .env \
  --name app2 \
  my-app
```

---

#  Example Dockerfile (Flask)

```Dockerfile
FROM python:3.9-slim

ENV PYTHONUNBUFFERED=1
ENV PYTHONDONTWRITEBYTECODE=1

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY app.py .

ENV PORT=5000
ENV DEBUG=false

EXPOSE 5000

CMD ["python", "app.py"]
```

---

#  Part 5 — Logs, Processes & Monitoring

### View Environment

```bash
docker exec flask-app env
docker exec flask-app printenv DATABASE_HOST
```

---

### Processes

```bash
docker top container-name
```

---

### Logs

```bash
docker logs container-name
docker logs -f container-name
docker logs --tail 100 -t container-name
```

---

### Resource Usage

```bash
docker stats
docker stats --no-stream
```

---

# Part 6 — Networking

```bash
docker network ls
docker network create my-network
docker network inspect my-network
```

```bash
docker run -d --name web1 --network my-network nginx
docker run -d --name web2 --network my-network nginx

docker exec web1 curl http://web2
```

---

#  Part 8 — Monitoring Script

```bash
bash monitor.sh
```

---

##  Conclusion

* Learned Docker volume types and persistence
* Configured environment variables and `.env` files
* Used logs and monitoring tools for debugging
* Implemented Docker networking for container communication

---

##  References

* Docker Official Docs: https://docs.docker.com
