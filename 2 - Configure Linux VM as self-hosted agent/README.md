# 🚀 Linux VM Setup as Self-Hosted Agent for Azure DevOps

This document provides step-by-step instructions to configure an Ubuntu Linux Virtual Machine as a **self-hosted agent** for an Azure DevOps pipeline.

---

## 📑 Table of Contents

- [Prerequisites](#-prerequisites)
- [Installation Steps](#️-installation-steps)
- [Verification](#-verification)
- [Outcome](#-outcome)
- [Next Steps](#-next-steps)

---

## 📋 Prerequisites

Ensure the following requirements are met before proceeding:

- Ubuntu-based Linux VM
- SSH access to the VM
- User account with `sudo` privileges
- SSH key pair
- Public IP address of the VM

---

## 🛠️ Installation Steps

### 1️⃣ Update Package Lists

Update the system package index to fetch the latest package metadata.

```bash
sudo apt update
```

---

### 2️⃣ Install Docker

Install Docker using Ubuntu’s default package repository.

```bash
sudo apt install docker.io -y
```

Verify Docker installation:

```bash
docker --version
```

---

### 3️⃣ Grant Docker Permissions to Logged-in User

Add the current user (`azureuser`) to the Docker group so Docker commands can run without `sudo`.

```bash
sudo usermod -aG docker azureuser
```

---

### 4️⃣ Restart Docker Service

Restart the Docker service to apply changes.

```bash
sudo systemctl restart docker
```

(Optional) Verify Docker service status:

```bash
sudo systemctl status docker
```

---

### 5️⃣ Reconnect to the VM

Log out and reconnect to ensure group membership changes take effect.

Logout:

```bash
exit
```

Reconnect via SSH:

```bash
ssh -i <keyfile> azureuser@<VM_PUBLIC_IP>
```

Replace:

- `<keyfile>` with the path to your private SSH key file  
- `<VM_PUBLIC_IP>` with the VM’s public IP address  

---

## 🔎 Verification

Confirm that the logged-in user can execute Docker commands without `sudo`.

```bash
docker pull hello-world
```

If the image downloads successfully without permission errors, Docker is correctly configured.

---

## ✅ Outc