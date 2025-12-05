# 📝 Azure Artifacts – How to Create a Feed

Azure Artifacts Feeds allow you to store and share packages (Maven, npm, NuGet, Python, Universal Packages) inside your Azure DevOps project or organization.

---

# 🚀 Steps to Create a New Feed

## 1️⃣ Navigate to Azure Artifacts
- Go to your Azure DevOps project.  
- On the left menu, click **Artifacts**.

---

## 2️⃣ Click “Create Feed”
- In the top-right corner, click **➕ Create Feed**.  
- This opens the **Create New Feed** panel.

---

## 3️⃣ Configure Feed Details

### 📌 Name
Enter a unique name for your feed.  
Examples:
- `maven-feed`
- `dev-artifacts`
- `company-packages`

---

## 4️⃣ Set Feed Visibility

### 🔵 Members of organization
- Any user in your Azure DevOps organization can view/use the feed.  
- Recommended for internal teams.

### ⚪ Specific people
- Only selected users or groups can access the feed.  
- Use this for secure/private packages.

---

## 5️⃣ Upstream Sources (Optional)
Check this option if you want the feed to include packages from public registries.

### ✔ Include packages from common public sources

This enables proxying and caching from:
- NuGet.org  
- npmjs.com  
- Maven Central  
- Python Package Index (PyPI)

Useful when:
- You want caching  
- You want control over external dependencies  
- You want builds to work even if public registries go offline  

---

## 6️⃣ Choose Feed Scope

### 🔵 Project Scope (Recommended)
- Feed is available only inside this specific Azure DevOps project.  
- Best for project-based teams.

### ⚪ Organization Scope
- Feed is shared across the entire Azure DevOps organization.  
- Best for companies with multiple projects sharing libraries.

---

## 7️⃣ Click “Create”
- After configuring all options, click **Create**.  
- Your feed is now ready to store and distribute packages.

---

# 🎯 Summary Table

| Setting | Explanation |
|--------|-------------|
| **Name** | Feed name (unique) |
| **Visibility** | Organization members or specific people |
| **Upstream Sources** | Optional — pulls packages from public registries |
| **Scope** | Project-only or organization-wide |
| **Result** | A package feed you can push/pull artifacts from |

---

# ⭐ Example Use Cases

### ✔ Maven JAR Repository
Use the feed URL in your **settings.xml**.

### ✔ npm Package Hosting
Use the feed URL in your **.npmrc**.

### ✔ Python Private Packages
Use the feed URL in **pip.conf**.

### ✔ Universal Packages
Store ZIPs, binaries, configuration files, etc.

