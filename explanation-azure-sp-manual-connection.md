
# 🔧 Azure DevOps Manual Service Connection Using Your Own Service Principal (SP)

When you create a Service Principal (SP) **yourself** in Azure — Azure DevOps cannot automatically detect or configure it.  
That is why you must use the **manual** option.

---

## 🚀 Why Use *Manual* Mode?

Azure DevOps offers **two ways** to create Azure connections:

### 1️⃣ Automatic (Azure DevOps Creates the SP)
- Azure DevOps creates an SP for you  
- Assigns roles  
- Generates secret  
- Fills IDs automatically  
✔ Easiest  
❌ Not applicable because **you created the SP manually**

---

### 2️⃣ Manual (You Created the SP Yourself)

You manually created:
- ✔ App Registration  
- ✔ Client Secret  
- ✔ Assigned RBAC role  
- ✔ Copied Client ID + Tenant ID  

Therefore Azure DevOps needs you to input these fields manually.

---

## ⚠️ Why Verification Failed Earlier

You mistakenly used:

❌ **SECRET ID**  
instead of  
✔ **SECRET VALUE**

Azure DevOps only accepts the *secret value* for authentication.

After correcting this, verification succeeded. 🎉

---

## 🧾 Required Values for Manual Connection

You must enter:

| Field | Value From Azure |
|------|------------------|
| Subscription ID | 💠 Subscription page |
| Subscription Name | 💠 Subscription page |
| Tenant ID | 💠 App Registration → Overview |
| Client ID | 💠 App Registration → Overview |
| Client Secret (Value) | 💠 Certificates & secrets |

⚠️ **Secret ID is NOT used. Only Secret VALUE works.**

---

## 🟢 Final Result

After correcting the secret value:
- Verification ✔️ Succeeded  
- Service connection ✔️ Created  
- Pipelines ✔️ Can authenticate to Azure  

🎉 You solved it correctly!

---

## 📌 Conclusion  

You must choose **manual** mode **because you created the SP yourself**, not Azure DevOps.

If you'd like, I can create a diagram version too!  
