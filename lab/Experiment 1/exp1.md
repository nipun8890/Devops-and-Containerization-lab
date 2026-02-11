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
![Download VirtualBox](screenshots/downloadvirtualbox.png)


![VirtualBox Website](screenshots/virtualbox.png)


![Vagrant Installation](./screenshots/vagrant.png)


![Vagrant Up](./screenshots/vagrantup.png)


![Vagrant SSH](./screenshots/vagrant-ssh.png)


![Verifying Nginx](./screenshots/verifyingnginx.png)




## Procedure



### Step 1: Install Docker
Download and install Docker Desktop from the official Docker website. After installation, start Docker Desktop.

---

Step 2: Verify WSL Installation
wsl --list --verbose



OR

wsl -l -v


This displays:

Installed Linux distributions

WSL version (WSL 1 or WSL 2)

Running status

Step 3: Check and Change WSL Version

Convert Ubuntu to WSL 2:

wsl --set-version Ubuntu 2


Convert to WSL 1 (if required):

wsl --set-version Ubuntu 1


Set WSL 2 as default:

wsl --set-default-version 2

Step 4: Check Installed Linux Distributions
wsl --list --all


Install another distribution (example: Debian):

wsl --install -d Debian

Step 5: Set Default Linux Distribution
wsl --set-default Ubuntu

Step 6: Fix WSL 2 Kernel Update Issue (If Occurs)

If error appears:

“WSL 2 requires an update to its kernel”

Run:

wsl --set-version Ubuntu 2


If unresolved, install the latest WSL kernel update from Microsoft and restart.

Step 7: Common Errors and Solutions

Error: 'wsl' is not recognized as a command

Run in PowerShell (Admin):

dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart


Enable Virtual Machine Platform:

dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart


Restart the system.

Step 8: Virtualization Disabled Error (0x80370102)

Restart PC

Enter BIOS/UEFI (F2 / F10 / DEL / ESC)

Enable Intel VT-x / AMD-V

Save & Restart

Step 9: Useful WSL Commands
Command	Description
wsl	Start default Linux
wsl -d Ubuntu	Start Ubuntu
wsl --terminate Ubuntu	Stop Ubuntu
wsl --shutdown	Stop all WSL instances
wsl --unregister Ubuntu	Remove Ubuntu completely
Result

Windows Subsystem for Linux (WSL) was successfully installed and configured. Ubuntu Linux distribution was set up and verified with WSL 2, enabling Linux command-line and DevOps tool usage on Windows.

Conclusion

WSL provides a powerful Linux development environment on Windows. It allows seamless execution of Linux tools and is highly suitable for cloud computing, DevOps, and container-based workflows.

Experiment – 1
Comparison of Virtual Machines (VMs) and Containers using Ubuntu and Nginx
Aim

To study, implement, and compare Virtual Machines (VMs) and Containers by deploying an Ubuntu-based Nginx web server in both environments and analyzing performance and resource utilization.

Objectives

Understand conceptual differences between VMs and Containers

Configure VM using VirtualBox and Vagrant

Configure Containers using Docker inside WSL

Deploy Nginx on both VM and Container

Compare performance and resource usage

System Requirements
Hardware

64-bit system with virtualization enabled

Minimum 8 GB RAM (4 GB acceptable)

Stable internet connection

Software

Oracle VirtualBox

Vagrant

Windows Subsystem for Linux (WSL 2)

Ubuntu (WSL)

Docker Engine

Theory
Virtual Machine (VM)

A VM emulates a complete physical computer including OS, kernel, libraries, and drivers.

Characteristics:

Full OS per VM

Strong isolation

High resource usage

Slower startup

Container

Containers virtualize at OS level and share the host kernel.

Characteristics:

Shared kernel

Lightweight

Fast startup

Efficient resource usage

Experiment Setup
PART A: Virtual Machine Setup (VirtualBox & Vagrant)
Step 1: Install VirtualBox

Download from official website

Install with default settings

Restart if prompted

Step 2: Install Vagrant
vagrant --version

Step 3: Create Ubuntu VM
mkdir vm-lab
cd vm-lab
vagrant init ubuntu/jammy64
vagrant up
vagrant ssh

Step 4: Install Nginx in VM
sudo apt update
sudo apt install -y nginx
sudo systemctl start nginx

Step 5: Verify Nginx
curl localhost

Step 6: Stop and Remove VM
vagrant halt
vagrant destroy

PART B: Container Setup using Docker (WSL)
Step 1: Install Docker
sudo apt update
sudo apt install -y docker.io
sudo systemctl start docker
sudo usermod -aG docker $USER


Logout and login again.

Step 2: Run Nginx Container
docker pull nginx
docker run -d -p 8080:80 --name nginx-container nginx


Verify:

curl localhost:8080

Comparison Table
Parameter	Virtual Machine	Container
Boot Time	High	Very Low
Resource Usage	High	Low
OS Isolation	Full OS	Shared Kernel
Performance	Moderate	High
Portability	Limited	High
Result

Containers were found to be lightweight, faster, and more resource-efficient than virtual machines, while VMs provide stronger isolation.

Conclusion

Containers are ideal for modern DevOps and cloud-native applications due to speed and efficiency, whereas Virtual Machines are preferred when full OS isolation is required.

Viva-Voce Questions

What is the main difference between VM and container?

Why do containers start faster than VMs?

What is the role of a hypervisor?

Can containers run different OS kernels?

Why is Docker considered lightweight?

References

VirtualBox Documentation

Vagrant Documentation












