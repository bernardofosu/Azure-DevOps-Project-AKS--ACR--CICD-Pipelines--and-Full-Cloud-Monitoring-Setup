# 📝 Azure CLI Login Notes (Ubuntu, Linux, macOS, Windows)

These notes explain **exactly how to log into Azure CLI** from any machine, including servers without a browser (EC2, VM, SSH).

---

# 🔑 1. Basic Azure CLI Login (Normal Login)

Use this when your machine **has a web browser**.

```bash
az login
```

What happens:

- A browser window opens
- You sign in with your Microsoft/Azure account
- Azure CLI becomes authenticated

---

# 🚫 When Normal Login Fails

Normal login fails on:

- Servers without GUI (Ubuntu server, EC2, Azure VM, Docker)
- SSH terminal sessions
- Headless machines

If you see messages like:

```
Operation not supported
Failed to open browser
```

You must use **device login**.

---

# 🔐 2. Device Code Login (Works Everywhere)

Use this when no browser is available on the machine.

### 👉 Command:

```bash
az login --use-device-code
```

You will see:

```
To sign in, use a web browser to open https://microsoft.com/devicelogin
Enter the code: ABCD-1234
```

### Steps:

1. On your phone or computer → open: [https://microsoft.com/devicelogin](https://microsoft.com/devicelogin)
2. Enter the code shown in the terminal
3. Sign into your Azure account
4. Terminal will show login success

---

# 🧪 3. Verify Login

After login, always check your active subscription:

```bash
az account show
```

Expected fields:

- `name`: Azure subscription name
- `id`: Subscription ID
- `tenantId`: Directory ID
- `isDefault`: true

---

# 🔄 4. List All Subscriptions

If you have more than one subscription:

```bash
az account list --output table
```

---

# 🎯 5. Set Active Subscription

If you want to use a specific subscription:

```bash
az account set --subscription <subscription-id>
```

Example:

```bash
az account set --subscription 9fec0e69-266b-49ff-8c88-5d0050cc08d8
```

---

# 🧹 6. Fix Login Problems

### ❌ If you got stuck in browser login:

```bash
pkill -f "az login"
az login --use-device-code
```

### ❌ If subscription not found:

You are not logged in → run device login again.

---

# ⚙ 7. After Login: Connect to AKS

```bash
az aks get-credentials --resource-group <rg-name> --name <cluster-name>
```

Verify:

```bash
kubectl get nodes
```

---

# 🔗 8. Connect to Your AKS Cluster (Portal + CLI)

After logging into Azure CLI, follow these steps to connect to your AKS cluster.

## **🔍 Step 1 — Go to the Azure Portal**

1. Open: [https://portal.azure.com](https://portal.azure.com)
2. Search for your AKS cluster name (example: **k8-for-azuredevops**)
3. Click the cluster to open its Overview page

## **🔗 Step 2 — Click the “Connect” Button**

On the AKS Overview page:

- Look at the top menu
- Click **Connect**
- A side panel will open showing Azure CLI commands to connect

You will see commands like:

```bash
az account set --subscription <subscription-id>
az aks get-credentials --resource-group <resource-group> --name <cluster-name>
```

## **📥 Step 3 — Download Cluster Credentials**

Copy and run the command shown:

```bash
az aks get-credentials --resource-group k8-res-group --name k8-for-azuredevops
```

This downloads the kubeconfig into:

```
~/.kube/config
```

## **🧪 Step 4 — Test Your Connection**

Verify that kubectl is talking to your cluster:

```bash
kubectl get nodes
```

Then check all pods:

```bash
kubectl get pods -A
```

If you see running pods → the connection is successful.

---

# 🎉 Summary

- Use **az login** when GUI browser exists
- Use **az login --use-device-code** for servers/SSH
- Always verify with **az account show**
- Set subscription with **az account set**
- You are ready for AKS after successful login

These notes ensure you always log into Azure CLI successfully on ANY system! 💙
