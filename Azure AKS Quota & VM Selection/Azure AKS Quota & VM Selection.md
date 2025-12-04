# 📝 Azure AKS Quota & VM Selection Cheat Sheet

## 🔍 1. How to Check Azure Quotas

1. Go to **Azure Portal**
2. Search for **Usage + quotas**
3. Select your **subscription**
4. Set **Provider = Compute**

---

## 🎯 2. Filter VM Families

In the search box, type:

- **D**
- **Dv3**
- **Dv4**
- **Dv5**
- **Dsv3**
- **Dsv4**

👉 AKS works best with **D-series**.

---

## 📊 3. Understand Quota Values

### ✔ "0 of 10"

- You are using 0
- You have **10 usable vCPUs**
- You CAN deploy VMs from this family

### ❌ "0 of 0"

- No quota available
- You CANNOT use this VM family

---

## 🧮 4. Calculate Required vCPU for AKS

AKS needs **minimum 2 nodes**.

Formula:

```
Required quota = VM vCPU × node count
```

### Example:

- VM: **D2s_v3 (2 vCPU)**
- Nodes: **2**

```
2 × 2 = 4 vCPUs needed ✔
```

---

## 🚫 5. VM Families You Cannot Use for AKS

- ❌ B-Series (B2s, B4ms, B4ps_v2)
- ❌ VM families showing **0 of 0**

Reason: B-series are **burstable** and not allowed for AKS system node pools.

---

## ⭐ 6. Best VM Families for AKS

### General Purpose (Recommended)

- 🔵 **D2s_v3** (2 vCPU, 8GB RAM)
- 🔵 **D4s_v3** (4 vCPU, 16GB RAM)
- 🔵 **D2as_v5** / **D4as_v5**
- 🔵 **D2s_v4** / **D4s_v4**

### Memory Heavy

- 🟣 E-Series (expensive)

---

## 📌 7. Choosing the Right VM (Easy Steps)

1. **Filter for D-series**
2. **Check quota** → choose the family with “0 of 10” or more
3. **Pick a VM** where:

```
VM vCPU × 2 nodes ≤ your quota
```

---

## 🧠 8. Quick Decision Guide

```
If quota ≥ 4  → choose D2s_v3
If quota ≥ 8  → choose D4s_v3
If quota ≥ 16 → choose D8s_v3
If quota = 0  → request quota increase
Never choose B-series for AKS ❌
```

---

## 🎉 Summary

- Always check **Usage + quotas**
- Focus on **D-series** for AKS
- Confirm quota before choosing VM
- Avoid **B-series**
- Use the formula to ensure you have enough vCPU

🔥 With these steps, you can ALWAYS pick the right VM size for AKS!

# 📘 Azure AKS Quota & VM Selection Cheat Sheet

## 🔍 1. How to Check Azure Quotas

1. Go to **Azure Portal**
2. Search for **Usage + quotas**
3. Choose your **Subscription**
4. Set **Provider = Compute**
5. Search using VM **family names**, not specific SKUs  
   Examples: `Dv3`, `Dsv3`, `Dv4`, `Dsv4`, `Dasv5`

---

## 🎯 2. Filter VM Families (Correct Way)

Use these keywords:

- **Dv3**
- **Dv4**
- **Dv5**
- **Dsv3**
- **Dsv4**
- **Dasv5**

❗ _Do NOT search using "D2s", "D4s", etc.—Azure will show no results._

---

## 📊 3. Understanding Quota Values

### ✔ "0 of 10"

- Using **0 vCPUs**
- Allowed **10 vCPUs**
- VM family is **available**

### ❌ "0 of 0"

- No quota assigned
- VM family **cannot be used**

---

## 🧮 4. AKS Required vCPU Formula

AKS requires **minimum 2 nodes**.

```
Required quota = VM vCPU × number of nodes
```

### Example:

- VM: **D2s_v3 (2 vCPU)**
- Nodes: **2**

```
2 × 2 = 4 vCPUs needed ✔
```

---

## 🚫 5. VM Families You CANNOT Use for AKS

- ❌ **B-Series** (B2s, B4ms, B4ps_v2)
- ❌ VM families showing **0 of 0**
- ❌ **Dv2 series** (old, often unavailable)

Reason: B-Series are **burstable** → not supported for system node pools.

---

## ⭐ 6. Best VM Families for AKS

### Recommended (General Purpose)

- 🔵 **D2s_v3**
- 🔵 **D4s_v3**
- 🔵 **D2as_v5 / D4as_v5**
- 🔵 **D2s_v4 / D4s_v4**

### Memory Optimized

- 🟣 **E-Series** (more expensive)

---

## 🧠 7. Quick VM Selection Steps

1. Filter quotas using **Dv3, Dv4, Dv5, Dsv3, Dsv4, Dasv5**
2. Pick a family showing **"0 of 10", "0 of 20", etc."**
3. Apply the formula:

```
VM vCPU × node count ≤ quota
```

---

## ⚡ 8. Fast Decision Guide

```
If quota ≥ 4 vCPU  → use D2s_v3
If quota ≥ 8 vCPU  → use D4s_v3 or D4as_v5
If quota ≥ 16 vCPU → use D8s_v3
If quota = 0       → request quota increase
Never use B-series ❌
Never use Dv2 ❌
```

---

## 🎉 Summary

- Always search quotas using **family names** (Dv3, Dsv3, Dv4…)
- Use **D-Series** for AKS system node pools
- Avoid **B-series** and **Dv2**
- Use the vCPU formula to confirm available quota
