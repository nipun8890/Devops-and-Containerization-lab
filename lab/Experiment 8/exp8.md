# Containerization & DevOps Lab  
## Experiment 8 – Ansible  

---

### Name: Nipun Agrawal 
### SAP ID: 500119472
### Batch: B3 (CCVT)  

---

##  Screenshots

![Screenshot](Screenshots/Screenshot%202026-04-15%20085015.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085028.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085033.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085042.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085051.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085059.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085107.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085115.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085122.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085133.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085139.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085148.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085612.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20085655.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20090302.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20090352.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20090716.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20090831.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091157.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091204.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091213.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091222.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091311.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091443.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091450.png)
![Screenshot](Screenshots/Screenshot%202026-04-15%20091457.png)
## 1. Theory

### 1.1 Problem Statement
Managing infrastructure manually across multiple servers leads to:
- Configuration drift  
- Inconsistent environments  
- Repetitive work  

---

### 1.2 What is Ansible?
Ansible is an **open-source automation tool** used for:
- Configuration management  
- Application deployment  
- Orchestration  

**Features:**
- Agentless (uses SSH / WinRM)
- YAML-based playbooks

---

### 1.3 How Ansible Solves the Problem
- Agentless architecture  
- Idempotent execution  
- Declarative syntax  
- Push-based model  

---

### 1.4 Key Concepts

| Component | Description |
|----------|------------|
| Control Node | Where Ansible runs |
| Managed Nodes | Target systems |
| Inventory | List of servers |
| Playbooks | YAML automation files |
| Tasks | Individual actions |
| Modules | Built-in tools |
| Roles | Reusable structure |

---

### 1.5 Benefits
- Free & open-source  
- Easy to use  
- No agents required  
- Strong community support  

---

## 2. Part A – Ansible Demo

### 2.1 Install Ansible

#### Using pip
```bash
pip install ansible
ansible --version
Using apt
sudo apt update -y
sudo apt install ansible -y
ansible --version
2.2 Post Installation Check
ansible localhost -m ping

Expected Output:

localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
3. Docker + SSH Setup
3.1 Generate SSH Key
ssh-keygen -t rsa -b 4096
cp ~/.ssh/id_rsa.pub .
cp ~/.ssh/id_rsa .
3.2 Dockerfile
FROM ubuntu

RUN apt update -y
RUN apt install -y python3 python3-pip openssh-server

RUN mkdir -p /run/sshd && \
    echo 'root:password' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

COPY id_rsa /root/.ssh/id_rsa
COPY id_rsa.pub /root/.ssh/authorized_keys

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
3.3 Build Image
docker build -t ubuntu-server .
3.4 Test SSH
docker run -d -p 2222:22 ubuntu-server
ssh -i ~/.ssh/id_rsa root@localhost -p 2222
4. Ansible with Docker
4.1 Run 4 Containers
for i in {1..4}; do
  docker run -d -p 220${i}:22 --name server${i} ubuntu-server
done
4.2 Inventory File
[servers]
172.17.0.2
172.17.0.3
172.17.0.4
172.17.0.5

[servers:vars]
ansible_user=root
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_python_interpreter=/usr/bin/python3
4.3 Test Connectivity
ansible all -i inventory.ini -m ping
5. Playbook
5.1 Create Playbook
---
- name: Update and configure servers
  hosts: all
  become: yes

  tasks:
    - name: Update apt packages
      apt:
        update_cache: yes

    - name: Install packages
      apt:
        name: ["vim", "htop", "wget"]
        state: present

    - name: Create test file
      copy:
        dest: /root/ansible_test.txt
        content: "Configured by Ansible"
5.2 ###  Run Playbook
ansible-playbook -i inventory.ini playbook.yml

5.3 ###  Verify
ansible all -i inventory.ini -m command -a "cat /root/ansible_test.txt"
6. Additional Playbook
---
- name: Configure servers
  hosts: servers
  become: yes

  tasks:
    - name: Update packages
      apt:
        update_cache: yes

    - name: Install Python
      apt:
        name: python3
        state: latest

7. Why Ansible?
Scalable
Consistent
Efficient
Infrastructure as Code
8. ### Observations
SSH key login required
Docker simulates servers
Inventory organizes hosts
Playbooks automate tasks
9. #### Result

Ansible successfully configured multiple Docker containers using playbooks.

10. ### Conclusion

Ansible simplifies server management through automation, making deployments faster, consistent, and reliable.