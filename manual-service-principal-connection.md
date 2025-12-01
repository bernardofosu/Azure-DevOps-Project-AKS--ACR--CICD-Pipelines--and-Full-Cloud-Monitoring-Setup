
# 🟥 Azure DevOps — Create Service Connection Using Manual Service Principal (SP)

## 🟦 Step 1 — Open Service Connections
Go to:

**Project Settings → Service connections**

---

## 🟥 Step 2 — Click “New service connection”
Click the **New service connection** button.

---

## 🟦 Step 3 — Select Azure Resource Manager
Choose:

**Azure Resource Manager → Next**

---

## 🟥 Step 4 — Click the Hidden Link: “create manually”
Look under the **Subscription** dropdown.

Click:

**➡️ “create manually”**

This switches Azure DevOps to the **manual Service Principal mode**.

---

## 🟥 Step 5 — Change Credential Type to “Secret”
In the **Credential** dropdown:

Select:

**➡️ Secret**

This reveals the manual Service Principal fields.

---

## 🟦 Step 6 — Fill In Your Service Principal Details

### 🔹 Subscription ID
`9fec0e69-266b-49ff-8c88-5d0050cc08d8`

### 🔹 Subscription Name
`Azure subscription 1`

### 🔹 Application (Client) ID
`6656fb8b-b787-4fe7-bf8b-cdc85c2bdcff`

### 🔹 Directory (Tenant) ID
`2304da9f-d214-43fc-b9b9-02202e4a5e5a`

### 🔹 Secret (Service Principal key)
Paste the **Secret Value** from:
Azure Portal → App registrations → **nakodtech-sp** → Certificates & secrets.

---

## 🟥 Step 7 — Click “Verify and save”
Azure DevOps will validate and store the service connection.

---

## 🎉 Done!
Your Azure DevOps pipeline now uses **your manually created Service Principal (SP)** securely and correctly.
