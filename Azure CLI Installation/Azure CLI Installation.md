# 📝 Azure CLI Installation Notes (With Commands & Explanations)

https://learn.microsoft.com/cli/azure/install-azure-cli

## ✅ Overview

The Azure CLI can be installed using **two methods**:

1. **One‑command automatic installation** (fastest)
2. **Step‑by‑step manual installation** (more control)

These notes summarize both methods clearly.

---

# 🚀 Option 1: Install Azure CLI With One Command

This method uses an official Microsoft installation script.

### 👉 Command (Ubuntu/Debian)

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

### 📌 Notes

- Downloads and runs the official Azure CLI installer.
- Safe to use because the script is from **Microsoft**.
- You can inspect the script first:

  ```bash
  curl -sL https://aka.ms/InstallAzureCLIDeb -o install.sh
  nano install.sh
  ```

---

# 🛠 Option 2: Step-by-Step Azure CLI Installation

Use this if you want to understand each stage of the installation.

## 1️⃣ Install Required Packages

These packages allow apt to download and verify Microsoft packages.

```bash
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```

---

## 2️⃣ Download and Install Microsoft Signing Key

This ensures apt trusts the Azure CLI repository.

```bash
sudo mkdir -p /etc/apt/keyrings
curl -sLS https://packages.microsoft.com/keys/microsoft.asc |
  gpg --dearmor | sudo tee /etc/apt/keyrings/microsoft.gpg > /dev/null
sudo chmod go+r /etc/apt/keyrings/microsoft.gpg
```

---

## 3️⃣ Add the Azure CLI Software Repository

Tells apt where to download Azure CLI from.

```bash
AZ_DIST=$(lsb_release -cs)
echo "Types: deb
URIs: https://packages.microsoft.com/repos/azure-cli/
Suites: ${AZ_DIST}
Components: main
Architectures: $(dpkg --print-architecture)
Signed-by: /etc/apt/keyrings/microsoft.gpg" | sudo tee /etc/apt/sources.list.d/azure-cli.sources
```

---

## 4️⃣ Update & Install Azure CLI

```bash
sudo apt-get update
sudo apt-get install azure-cli
```

---

# 🧪 Verify Installation

```bash
az version
```

You should see the CLI version and modules.

---

# 🏁 After Installation (Important)

### Login to Azure:

```bash
az login
```

### Connect to your AKS cluster:

```bash
az aks get-credentials --resource-group k8-res-group --name k8-for-azuredevops
```

---

# 🎉 Summary

- Use **Option 1** for quick installation.
- Use **Option 2** for full transparency and manual control.
- After installing, run `az login` and connect to your AKS cluster.

These notes help you install Azure CLI anytime with confidence! 💙
