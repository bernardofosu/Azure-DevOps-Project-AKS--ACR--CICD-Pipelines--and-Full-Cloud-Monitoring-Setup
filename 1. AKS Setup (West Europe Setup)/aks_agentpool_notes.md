# 🧩 AKS Agent Pool Configuration — Notes

These notes explain the meaning and best‑practice choices for each setting in your **AKS Node Pool (agentpool)** configuration.

---

## 🔹 1. Node Pool Name
```
agentpool
```
- ✔ Default and recommended name  
- ✔ Used for the **system** node pool  
- Runs core Kubernetes components (CoreDNS, Kube‑Proxy, Cilium, Metrics‑Server)

---

## 🛠 2. Mode
```
System
```
- ✔ Required for the first node pool  
- ✔ Hosts all system-critical pods  
- User workloads should go in a **User** node pool later

---

## 🐧 3. OS SKU
```
Ubuntu Linux
```
- ✔ Best and most stable OS for AKS  
- ✔ Recommended by Microsoft  
- Better compatibility and fewer issues than Windows or Azure Linux

---

## 🌍 4. Availability Zones
```
Zones 1, 2
```
### What it means:
- Nodes are distributed across **two datacenter zones**  
- Provides **High Availability (HA)**  
- Cluster remains online even if one zone fails  

### Notes:
- ✔ Good for production or learning HA  
- 🔸 For Dev/Test you may choose **None** to save cost

---

## 💰 5. Azure Spot Instances
```
Disabled
```
- ✔ Correct — system node pools **cannot** use Spot  
- Spot VMs can be evicted at any time → unsafe for system pods  
- Only use Spot for **user** node pools (optional)

---

## 🖥 6. Node Size
```
Standard_D2s_v6
2 vCPUs | 8 GiB RAM
```

### Why this is the correct choice:
- Replaces older **D2s_v3** in West Europe  
- ✔ Supported and recommended  
- ✔ Matches your quota  
- ✔ Perfect for AKS System pool  
- Balanced CPU and RAM for cost‑effective clusters

---

## 🔄 7. Scale Method
```
Autoscale (Recommended)
```
- ✔ Automatically adjusts nodes based on workload  
- ✔ Prevents resource shortages  
- ✔ Saves cost (when min < max)

---

## 🔢 8. Minimum & Maximum Node Count
```
Min = 2
Max = 2
```

### Meaning:
- Autoscaler is enabled but fixed at **2 nodes**  
- AKS always requires **at least 2 nodes** for system reliability  
- ✔ This is the correct configuration for stable operation

---

## 🧱 9. Node Pool Summary
| Setting | Value |
|--------|--------|
| Name | agentpool |
| Mode | System |
| VM Size | Standard_D2s_v6 |
| OS | Ubuntu |
| Node Count | 2–2 |
| Availability Zones | 1, 2 |

---

## ⭐ Final Verdict
Your **agentpool** configuration is:

✔ Correct  
✔ Within quota  
✔ Best practice for AKS  
✔ Highly stable  
✔ Ready for deployment  

You're good to continue to **Networking** → **Review + Create**! 🚀

