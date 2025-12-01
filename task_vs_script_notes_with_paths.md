
# 🟦 Task vs Script in Azure DevOps — Notes with Emojis + Tool Paths

Azure DevOps Pipelines support two major step types: **TASK-BASED STEPS** and **SCRIPT-BASED STEPS**.  
This document explains the difference AND shows **where the actual tools live on the agent**.

---

# 🟦 1️⃣ TASK-BASED STEPS (High‑Level Azure Tasks)

Azure tasks are **pre‑installed tools** managed by Azure DevOps.

Example:
```yaml
- task: Docker@2
  inputs:
    containerRegistry: 'docker-conn'
    repository: 'bofosu1/bankapp2'
    command: 'buildAndPush'
    Dockerfile: '**/Dockerfile'
```

### ⭐ What Azure DevOps Does Automatically
- Installs and manages Docker, Maven, Node, Java, etc.
- Handles login (docker login, npm login)
- Handles tagging and metadata
- Runs validated, safer commands
- Provides consistent logging
- Adds retry and error handling

### 📦 Typical Tool Paths (Microsoft‑Hosted Agents)

| Tool | Path |
|------|------|
| Docker | `/usr/bin/docker` |
| Maven | `/usr/share/apache-maven-*` |
| Java JDK | `/usr/lib/jvm/msopenjdk-*` |
| Node.js | `/usr/local/bin/node` |
| npm | `/usr/local/bin/npm` |
| Python | `/usr/bin/python3` |
| Git | `/usr/bin/git` |
| Azure CLI | `/usr/bin/az` |
| Tool Cache | `/opt/hostedtoolcache/` |

Azure Pipelines inject these tools into the `$PATH` automatically.

### ⭐ Summary  
**TASK = Azure-managed tool**  
✔ Safer  
✔ Pre-installed  
✔ Auto-authentication  
✔ Recommended when available  

---

# 🟦 2️⃣ SCRIPT-BASED STEPS (Raw Shell Commands)

Example:
```yaml
- script: |
    docker build -t bofosu1/bankapp2 .
    docker push bofosu1/bankapp2
```

### ⭐ What YOU must handle manually
- Install tools
- Authenticate (docker login)
- Write Docker commands yourself
- Manage errors
- Manage tags
- Setup environment variables

### 📦 Tool Paths (Self‑Hosted Agents)

Self‑hosted tools depend on YOUR installation.  
Typical Linux agent paths:

| Tool | Possible Path |
|------|---------------|
| Docker | `/usr/bin/docker` |
| Java | `/usr/lib/jvm/java-11-openjdk/` |
| Maven | `/usr/share/maven/` or `/opt/maven/` |
| Trivy | `/usr/local/bin/trivy` |
| Helm | `/usr/local/bin/helm` |
| kubectl | `/usr/local/bin/kubectl` |
| Node.js | `/usr/bin/node` |
| Python | `/usr/bin/python3` |
| Git | `/usr/bin/git` |

### ⭐ Summary  
**SCRIPT = raw manual commands**  
✔ More flexible  
✔ Needed for tools without tasks (Trivy, Helm)  
❌ Must manage installs, auth, errors  

---

# 🟦 Task vs Script — Quick Comparison

| Feature | Task-Based Step | Script-Based Step |
|--------|------------------|-------------------|
| Installation | ✔ Automatic | ❌ Manual |
| Auth (Docker/NPM/etc.) | ✔ Automatic | ❌ Must write login |
| Error Handling | ✔ Built-in | ❌ Manual |
| YAML Cleanliness | ✔ Clean | ❌ More complex |
| Flexibility | Moderate | ⭐ Maximum |
| Preferred For | Docker, Maven, Sonar | Trivy, Helm, custom tools |

---

# 🟦 Memory Trick  
### 🟩 **TASK = Azure handles everything**  
Tools live in the agent’s tool cache and system paths.

### 🟥 **SCRIPT = You handle everything**  
You must install the tool and ensure PATH is correct.

---

# 📁 File Created  
This file contains all comparison notes, tool path references, and explanations.

