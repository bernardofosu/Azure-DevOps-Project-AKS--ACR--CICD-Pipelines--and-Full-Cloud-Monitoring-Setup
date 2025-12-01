# 🔐 Azure Service Principal – Manual Service Connection Setup (with Emojis)

## 📌 Overview

This guide explains how to **create a manual Azure Service Connection** in Azure DevOps using a **Service Principal (SP)**. It also includes the **exact error encountered** and **how it was solved**.

---

## 🏗️ Step 1 — Create a Service Principal (App Registration)

1. Go to **Azure Portal → Microsoft Entra ID → App registrations**.
2. Click **➕ New registration**.
3. Give it a name (example: `nakodtech-sp`).
4. Click **Register**.

---

## 🔑 Step 2 — Create a Client Secret

1. Open your SP → **Certificates & secrets**.
2. Click **➕ New client secret**.
3. Copy the **Value** immediately! (You will NOT see it again.)

⚠️ **Important:** Azure shows two columns:

- **Value** → ✔️ This is the REAL password.
- **Secret ID** → ❌ This is NOT a password.

---

## 👤 Step 3 — Assign RBAC Permissions

Go to:
**Azure Portal → Subscription → Access Control (IAM)**

Add this role:

- **Role:** Contributor
- **Assign to:** Your Service Principal

---

## 🔌 Step 4 — Create Azure DevOps Service Connection

Path:
**Project Settings → Service connections → New service connection → Azure Resource Manager**

Select:

- **Identity type:** App registration or managed identity (manual)
- **Credential:** Secret
- **Scope level:** Subscription

Fill the fields:

- **Subscription ID**
- **Subscription name**
- **Application (client) ID**
- **Directory (tenant) ID**
- **Client secret → paste VALUE (not ID!)**

Click **Verify**.

---

## ❌ The Error Encountered

When creating the service connection, this error appeared:

```
Failed to obtain the Json Web Token (JWT) using service principal client ID
```

And **Verification Failed ❌**.

---

## 🛑 Root Cause

I mistakenly copied the **Secret ID** instead of the **Secret VALUE**.

Azure shows:

- **Value → the real secret (correct)**
- **Secret ID → not a password (incorrect)**

I used **Secret ID**, so Azure DevOps could not authenticate.

---

## ✅ How It Was Solved

I returned to:
**Azure Portal → App Registration → Certificates & secrets**

Then I copied:
✔️ **Value** (the long secret string)

Replaced the field in Azure DevOps → clicked **Verify**.

✔️ **Verification Succeeded** 🎉

---

## 🎉 Final Status

Your manual SP-based service connection works correctly and is ready for use in pipelines.

If you need:

- YAML pipeline examples
- How to store secrets in DevOps Library
- How to switch to Workload Identity Federation (no secrets)

Just let me know! 🚀
