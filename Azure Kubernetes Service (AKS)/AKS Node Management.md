# 🧩 AKS Node Management Explained

## 🤖 Node Auto Provisioning (NAP)

Automatically adds or removes nodes based on pending pods.

- 📈 Scales when pods need more CPU/RAM
- 📉 Removes unused nodes to save cost
- ⚡ Great for unpredictable workloads
- 💰 Helps optimize cost + performance

---

## 🧵 Node Pools

Separate groups of nodes for different workloads.

- 🧰 **system pool** → runs Kubernetes system services
- 🚀 **user/app pools** → run your application pods
- ✨ Supports Linux & Windows pools
- 🧠 Each pool can have different VM sizes, OS, scaling rules

Your example:

- Name: `agentpool`
- Type: System
- VM: Standard_DS2_v2
- OS: Ubuntu
- Scale range: 2–5 nodes
- Max pods per node: 110

---

## 🪄 Virtual Nodes (Serverless Pods)

Run pods on Azure Container Instances (ACI) instantly.

- ⚡ Instant scale (no VM startup time)
- 💵 Pay only for running time
- 🌀 Perfect for burst/overflow traffic
- ❌ Not ideal for long-running workloads

---

## 🔐 Node Pool OS Disk Encryption

All AKS node disks are encrypted by default.

Options:

- 🔒 **Microsoft-managed keys** (default, secure)
- 🗝️ **Customer-managed keys (CMK)** using Azure Key Vault

CMK is required for:

- 🏦 Banking
- 🏥 Healthcare
- 🛡️ High-security compliance (PCI, HIPAA)

Default is fine for normal workloads.

---

## 🎯 DevOps Best Practices

- ✔ Enable Node Auto Provisioning for dynamic workloads
- ✔ Use multiple node pools for isolation
- ✔ Enable Virtual Nodes if you expect burst traffic
- ✔ Use default encryption unless you need enterprise security

Need a PRODUCTION AKS design? I can generate it for you! 🔥
