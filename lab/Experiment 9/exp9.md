# Experiment 9 - SonarQube Static Code Analysis

**Name:** Nipun Agrawal  
**SAP ID:** 500119472  
**Course:** Containerization and DevOps Lab  

---

## 📸 Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-28%20182912.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20183350.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20185237.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20185302.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20185445.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20185851.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20190216.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20190515.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20190635.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20191220.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20193341.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20200937.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20200952.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20201001.png)
![Screenshot](Screenshots/Screenshot%202026-04-28%20201050.png)

---

## Objective

Perform static code analysis using **SonarQube** to detect:
- Bugs  
- Security vulnerabilities  
- Code smells  
- Maintainability issues  

---

## Theory

### Problem Statement
Code issues are often discovered too late during testing or after deployment.

### What is SonarQube?
SonarQube is an open-source platform that performs **static code analysis**.

---

## Key Terms

| Term | Meaning |
|------|--------|
| Quality Gate | Rules code must pass |
| Bug | Code error |
| Vulnerability | Security issue |
| Code Smell | Poor code quality |
| Technical Debt | Fixing effort |
| Coverage | Tested code % |
| Duplication | Repeated code |

---

## Architecture


Your Code → Sonar Scanner → SonarQube Server → Database


### Step 1: Start SonarQube

Bash
cd ~/Desktop/exp10
docker-compose up -d
Check logs:
Bash
docker-compose logs -f sonarqube
Verify:
Bash
docker ps
###  Step 2: Open Dashboard
Go to:

http://localhost:9000
Login:

username: admin  
password: admin
###  Step 3: Generate Token
Go to My Account → Security
Create token: scanner-token
Copy it
Set token:
Bash
export SONAR_TOKEN=your_token_here
###  Step 4: Run Analysis
Bash
sonar-scanner \
-Dsonar.projectKey=my-app \
-Dsonar.sources=. \
-Dsonar.host.url=http://localhost:9000 \
-Dsonar.token=$SONAR_TOKEN
### Step 5: View Results
Open:

http://localhost:9000/dashboard?id=my-app
 Common Errors & Fixes
 Port already in use
Bash
docker stop <container_id>
### Node.js not found
Bash
sudo apt install nodejs npm -y
 ### Network error
Bash
docker-compose down
docker-compose up -d
 Jenkins Integration (CI/CD)
Groovy
pipeline {
    agent any
    stages {
        stage('SonarQube Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }
    }
}
### Results
Code successfully analyzed
Issues detected
Quality gate passed
### Conclusion
SonarQube helps:
Improve code quality
Detect bugs early
Enhance security
Automate code review in CI/CD