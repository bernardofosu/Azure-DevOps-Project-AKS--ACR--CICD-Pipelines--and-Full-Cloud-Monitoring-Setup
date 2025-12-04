# 🟦 Azure DevOps – Pipeline Setup Notes

---

## ⭐ 1. Open Azure DevOps Project

- Go to **https://dev.azure.com**
- Select your project → **Azure DevOps Project**
- Navigate to **Pipelines → Pipelines**

---

## ⭐ 2. Create a New Pipeline

Click:

➡ **New Pipeline**

Azure asks: **Where is your code?**

Choose one of the sources:

- 🔵 **Azure Repos Git** (your repository inside Azure DevOps)
- 🟣 **GitHub**
- 🟠 **Bitbucket**
- 🔴 **Other Git**

---

## ⭐ 3. Select Your Repository

You selected:

📁 **Boardgame**

This is the repository that contains your application code.

---

## ⭐ 4. Configure Pipeline

Azure DevOps shows many templates:

- 🐳 **Docker** (Build a Docker image)
- 🚀 **Deploy to AKS** (Azure Kubernetes Service)
- 🌱 **Starter Pipeline** (minimal YAML)
- 📄 **Existing Azure Pipelines YAML File**
- ☁ **.NET, Android, Java, Function Apps**, etc.

You selected:

✨ **Starter Pipeline**

---

## ⭐ 5. Review & Edit the YAML

Azure auto‑generated a basic pipeline:

```yaml
trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- script: echo Hello, world!
  displayName: 'Run a one-line script'

- script: |
    echo Add other tasks here
    echo Build, test, deploy your project
  displayName: 'Run a multi-line script'
```

You updated the commit message to:

📝 **“Build Nodejs App using Azure DevOps YAML Pipeline”**

---

## ⭐ 6. Save & Run Pipeline

You selected:

✔ **Commit directly to main**

Then clicked **Save** → pipeline runs automatically.

Pipeline status:

🟢 **Azure DevOps Project-Maven-CI** (successful)

---

✨ *Notes created with emojis for easy reading and Canva usage.*
