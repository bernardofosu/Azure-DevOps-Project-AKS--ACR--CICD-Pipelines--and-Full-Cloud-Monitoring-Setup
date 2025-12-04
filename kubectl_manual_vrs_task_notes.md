# 🚀 Kubectl Installer vs Manual Kubectl on Self-Hosted Agent  
### 📘 Azure DevOps — Detailed Notes (with Emojis)

---

## 🎯 Overview  
When deploying to Kubernetes (AKS) using Azure DevOps, you have **two options** for kubectl availability:

1. **Use Azure DevOps task → `KubectlInstaller@0`**  
2. **Use manually installed kubectl on your self-hosted agent**

These two options behave differently. This document explains the differences and best practice.

---

# 🔵 1. KubectlInstaller@0 — Azure DevOps Task

### ✔ What it does  
The `KubectlInstaller@0` task:

- ⬇️ Downloads kubectl dynamically during the pipeline  
- 🔄 Ensures version consistency  
- 🧪 Makes kubectl available ONLY for that job  
- 🛡 Avoids interfering with system kubectl  
- 📌 Works across multiple clusters / versions

### ✔ YAML Example  
```yaml
steps:
  - task: KubectlInstaller@0
    inputs:
      kubectlVersion: 'latest'
```

### ⭐ When to use it  
| Scenario | Recommended? |
|---------|--------------|
| Consistent kubectl version across agents | ✅ Yes |
| AKS upgrades | ✅ Yes |
| Avoiding PATH issues | ✅ Yes |
| Need different kubectl versions per pipeline | ✅ Yes |

---

# 🔵 2. Manual Kubectl Installed on Self-Hosted Agent

### ✔ How it’s installed  
```sh
sudo az aks install-cli
```

or

```sh
sudo snap install kubectl --classic
```

### ❗ Issues with relying ONLY on manual kubectl  
- ⚠️ Pipeline runs under a **different user (azuredevops agent)**  
- ⚠️ PATH may not include `/usr/local/bin` or `/home/ubuntu/.local/bin`  
- ⚠️ kubectl version may become **incompatible** with AKS versions  
- ⚠️ Not reproducible across different agents  

### ✔ YAML Example (manual kubectl)
```yaml
steps:
- script: |
    export PATH=$PATH:/usr/bin:/home/ubuntu/.local/bin
    kubectl version --client
    kubectl apply -f app.yaml
  displayName: "Run kubectl manually"
```

---

# 🟢 3. Best Practice — What You Should Use

### ⭐ ALWAYS USE:
```yaml
- task: KubectlInstaller@0
    inputs:
      kubectlVersion: 'latest'
```

### Why?

| Benefit | Explanation |
|--------|-------------|
| 🎯 Predictable | kubectl version is controlled by pipeline, not server |
| 🔒 Safe | Does not override system kubectl |
| 🔄 Compatible | Matches AKS version every time |
| 🧪 Reliable | No PATH issues |
| 🌍 Cluster upgrades | No breaking changes |

---

# 🧠 4. When Manual kubectl is Still Useful  
- Testing commands on the agent  
- Debugging cluster connectivity  
- Running `kubectl get nodes` or logs manually  

But **not for production pipelines**.

---

# 🎉 Final Recommendation  
Use **KubectlInstaller@0** in all pipelines, even on self‑hosted agents.

This gives you:

- 🛡 Stability  
- 🧩 Compatibility  
- 🔁 Version control  
- 🔧 Easily portable CI/CD workflows  

---

If you want, I can also create a:

📦 Full CI/CD pipeline (Build → Scan → Push → Deploy)  
📝 Documentation for AKS Deployment with Azure DevOps  
🔐 Service account/Service principal RBAC guide  

Just tell me **“generate full pipeline”** or **“create RBAC guide”**!