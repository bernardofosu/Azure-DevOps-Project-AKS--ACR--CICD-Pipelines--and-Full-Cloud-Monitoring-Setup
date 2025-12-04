# 🚀 Azure DevOps Notes with Emojis

## 📌 Resource Groups Created Automatically

When you create an AKS cluster, Azure automatically generates additional resource groups:

- **k8-rg** – 🧑‍💻 Your main resource group
- **MC_k8-rg_azuredevops-k8_westeurope** – 🏗️ Managed cluster resource group for node pools, networking, etc.
- **NetworkWatcherRG** – 👁️ Network monitoring and diagnostics
- **MA_defaultazuremonitorworkspace...** – 📊 Azure Monitor Log Analytics workspace

These are **normal** and required for AKS and monitoring features.

---

## 🔧 SonarQube Java Scan Fix

Since your project is Java Spring Boot:

### ✅ Correct Properties

```
sonar.java.binaries=target/classes
```

### 🛠️ Correct Pipeline Order

1. 🔍 SonarQubePrepare
2. 🏗️ Maven Build (`clean package`)
3. 🔎 SonarQubeAnalyze
4. 📤 SonarQubePublish

### ❌ Do NOT use for Java:

```
sonar.java.binaries=.
```

This is only for **non‑Java** projects.

---

## 🤖 Notes

- AKS always creates extra RGs → ✔️ expected
- SonarQube requires compiled `.class` files → ensure Maven build runs before scanning
- If you need a fully working pipeline YAML, I can generate it

---

Let me know if you want this expanded or new sections added! 😊
