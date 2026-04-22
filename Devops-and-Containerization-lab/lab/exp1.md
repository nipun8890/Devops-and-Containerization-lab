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

### Step 2: Verify WSL Installation
After restart, open PowerShell and execute:

ws1 --list --verbose

OR

ws1 -l -v

This displays:

Installed Linux distributions

WSL version (WSL 1 or WSL 2)
Running status
PS C:\WINDOWS\system32> wsl -l -v  
NAME STATE VERSION  
* docker desktop Running 2  
Ubuntu Running 2

### Step 3: Check and Change WSL Version

To convert Ubuntu to WSL 2:

wsl --set-version Ubuntu 2

To convert Ubuntu to WSL 1 (if needed):

wsl --set-version Ubuntu 1

To set WSL 2 as default for future installations:

wsl --set-default-version 2

PS C:\WINDOWS\system32> wsl --set-default Ubuntu  
The operation completed successfully.

### Step 4: Check Installed Linux Distributions

To list all available and installed distributions:

wsl --list --all

To install another distribution (example: Debian):

wsl --install -d Debian

PS C:\WINDOWS\system32> wsl --list --all Windows Subsystem for Linux Distributions: Ubuntu (Default) docker-osktop PS C:\WINDOWS\system32>

### Step 5: Set Default Linux Distribution

To set Ubuntu as default:

wsl --set-default Ubuntu

OR simply launch Ubuntu using:

Ws1

PS C:\WINDOWS\system32> wsl --set-default Ubuntu
The operation completed successfully.

### Step 6: Fix WSL 2 Kernel Update Issue (If Occurs)
If error appears:

"WSL 2 requires an update to its kernel"

Run:

wsl --set-version Ubuntu 2

If still unresolved, install the latest WSL kernel update from Microsoft and restart.

### Step 7: Common Errors and Solutions

Error: 'wsl' is not recognized as a command

Run in PowerShell (Admin):

dism.exe /online /enable-feature /featurename: Microsoft-Windows-Subsystem-Linux/all/norestart

Enable Virtual Machine Platform:

dism.exe /online /enable-feature / featurename: VirtualMachine Platform/all/norestart

Restart the system.

### Step 8: Virtualization Disabled Error (0x80370102)

If virtualization is disabled:

Restart PC
. Enter BIOS/UEFI (F2 / F10 / DEL / ESC)
Enable Intel VT-x / AMD-V
Save & Restart

### Step 9: Useful WSL Commands

Command

Description

wsl Start default Linux

wsl -d Ubuntu Start Ubuntu

wsl --terminate Ubuntu Stop Ubuntu

ws1 --shutdown Stop all WSL instances

wsl --unregister Ubuntu Remove Ubuntu completely

Result

Windows Subsystem for Linux (WSL) was successfully installed and configured. Ubuntu Linux distribution was setup and verified with WSL 2, enabling Linux command-line and DevOps tool usage on Windows.

Conclusion

WSL provides a powerful Linux development environment on Windows. It allows seamless execution of Linux tools and is highly suitable for cloud computing, DevOps, and container-based workflows.