# 🚀 Kubernetes Service Connection Notes (Azure DevOps)

## 🔗 Creating a New Kubernetes Service Connection

### 1️⃣ Open Azure DevOps Project Settings  
- Navigate to **Project Settings → Service Connections**  
- Click **New Service Connection**  
- Select **Kubernetes**

---

## 2️⃣ Choose Authentication Method  
Select:  
👉 **Azure Subscription** (recommended)

---

## 3️⃣ Select Your Azure Subscription  
- Choose: **Azure subscription 1 (9fec0e69-266b-49ff-8c88-5d0050cc08d8)**  
- Sign in when prompted 🔐  
- Azure DevOps loads your AKS clusters automatically

---

## 4️⃣ Select Your AKS Cluster  
Choose your cluster:  
🟦 **azuredevops-k8 (k8-rg)**

---

## 5️⃣ Choose Namespace  
You can select:

- `default` (recommended for first-time setup)  
OR  
- Any other namespace created later

---

## 6️⃣ Service Connection Settings  
| Setting | Value |
|--------|--------|
| **Service Connection Name** | `k8-svc-conn` |
| **Description** | `AKS connection for deployments` |
| **Grant permission to all pipelines** | ✅ Enabled |

---

## 7️⃣ Save the Connection  
Click **Save** to create the connection.

Azure DevOps will now be able to:
- Deploy to AKS  
- Run `kubectl` commands  
- Apply manifests  
- Run Helm charts  

---

## 🎉 Done!  
Your Azure DevOps → AKS integration is now ready!  
Use this in your pipeline:

```yaml
- task: KubernetesManifest@1
  inputs:
    kubernetesServiceConnection: 'k8-svc-conn'
```

---

Let me know if you want:
✅ Multi-stage CI/CD pipeline  
✅ Helm deployment pipeline  
✅ A full AKS DevOps documentation file  
