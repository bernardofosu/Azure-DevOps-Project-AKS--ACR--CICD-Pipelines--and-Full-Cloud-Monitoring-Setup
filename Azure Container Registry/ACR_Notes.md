# 📝 Azure Container Registry (ACR) – Clean Notes

## 📌 1. Project Details
- **Subscription:** Azure subscription 1  
- **Resource Group:** Recommended: `rg-container-registry`

## 📌 2. Instance Details
### **Registry Name:** `nakodtec-cr`  
- Must be globally unique  
- Final URL → **nakodtec-cr.azurecr.io**

### **Region:**  
- **West Europe**

### **Pricing Plan (SKU):**

| SKU | When to Use | Supports Private Access? |
|------|-------------|--------------------------|
| **Basic** | Small testing, learning | ❌ No |
| **Standard** | Normal DevOps workloads, AKS deployments | ❌ No |
| **Premium** | Production security: Private Link, CMK, Zones | ✔ Yes |

### ❗ IMPORTANT  
To enable **PRIVATE ACCESS (Private Endpoint)**, you **must choose Premium SKU**.

---

## 📌 3. Domain Name Label Scope
- Select: **Unsecure** (default)

## 📌 4. Networking Settings
- **Connectivity:** Public access (all networks)  
  → Private access requires **Premium**

## 📌 5. Encryption
- **Customer Managed Key (CMK):** Disabled  
  → Requires Premium

---

## ✔ 6. Summary for Your Setup (Standard SKU)

| Setting | Value |
|--------|--------|
| Registry Name | nakodtec-cr |
| Region | West Europe |
| SKU | **Standard** |
| Access | **Public access only** |
| Encryption | Platform-managed |
| Private Endpoint | ❌ Not available |
| Registry URL | nakodtec-cr.azurecr.io |

---

## ⭐ 7. When to Use Each SKU

### **Basic**
- Learning  
- Small projects  
- Cheapest  

### **Standard**
- Most CI/CD pipelines  
- Works with AKS  
- Good performance  
- No private link

### **Premium**
- Private access  
- CMK  
- Geo-replication  
- Availability zones  
- Enterprise workloads
