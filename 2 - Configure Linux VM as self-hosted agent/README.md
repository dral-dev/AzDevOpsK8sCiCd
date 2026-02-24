# 🚀 Configure Linux VM as Azure DevOps Self-Hosted Agent

This guide provides step-by-step instructions to:

1. Prepare a Linux VM (install Docker and prerequisites)
2. Configure the VM as a Self-Hosted Agent for Azure DevOps
3. Run and connect the agent to your Azure DevOps pipeline

---

# 📋 Prerequisites

Ensure you have the following before starting:

- Ubuntu-based Linux VM
- SSH access to the VM
- User account with `sudo` privileges
- SSH key pair
- Public IP address of the VM
- Azure DevOps organization access
- Personal Access Token (PAT)

---

# 🛠️ Step 1: Install Required Packages (Docker Setup)

These commands prepare the VM before configuring it as a self-hosted agent.

## 1️⃣ Update Package Lists

```bash
sudo apt update
```

---

## 2️⃣ Install Docker

```bash
sudo apt install docker.io -y
```

---

## 3️⃣ Grant Docker Permission to Logged-in User

```bash
sudo usermod -aG docker azureuser
```

---

## 4️⃣ Restart Docker Service

```bash
sudo systemctl restart docker
```

---

## 5️⃣ Reconnect to VM (Important)

Logout:

```bash
exit
```

Reconnect:

```bash
ssh -i <keyfile> azureuser@<VM_PUBLIC_IP>
```

Replace:

- `<keyfile>` → Path to your private SSH key
- `<VM_PUBLIC_IP>` → Public IP of your VM

---

## 6️⃣ Verify Docker Installation

```bash
docker pull hello-world
```

If the image downloads successfully without permission errors, Docker is properly installed and configured.

---

# 🔧 Install Miscellaneous Tools (If Needed)

This step is optional.

Depending on pipeline requirements, you may need additional utilities such as `unzip`.

If your pipeline throws errors related to missing tools, install them as needed.

Example:

```bash
sudo apt install unzip -y
```

---

# ⚙️ Step 2: Configure VM as Azure DevOps Self-Hosted Agent

## 1️⃣ Create Agent Directory

```bash
mkdir myagent && cd myagent
```

---

## 2️⃣ Download Azure DevOps Agent

Copy the download URL from the Azure DevOps portal (Agent Pool → New Agent → Linux).

Example:

```bash
wget https://download.agent.dev.azure.com/agent/4.268.0/vsts-agent-linux-x64-4.268.0.tar.gz
```

---

## 3️⃣ Extract the Downloaded Agent

```bash
tar zxvf vsts-agent-linux-x64-4.268.0.tar.gz
```

This only extracts the agent files.

---

## 4️⃣ Configure the Agent

Run:

```bash
./config.sh
```

You will be prompted for several inputs.

When asked for **Server URL**, enter:

```
https://dev.azure.com/<your-devops-org-name>
```

The setup will ask for:

- Authentication method
- Personal Access Token (PAT)
- Agent name
- Agent pool

Provide the required details when prompted.

---

## 5️⃣ Run the Agent

After successful configuration:

```bash
./run.sh
```

Your VM is now linked to Azure DevOps and ready to execute pipeline jobs.

---

# ✅ Final Outcome

After completing all steps:

- Docker is installed and working
- Required utilities are installed (if needed)
- Azure DevOps agent is configured
- VM is registered in Azure DevOps Agent Pool
- Pipelines can now run on this self-hosted agent

---

# 📚 Additional Resources

- Blog Post: techmilestonehb.com/---
- YouTube Video: -----

---

# 👨‍💻 Author

Your Name  
GitHub: https://github.com/yourusername

