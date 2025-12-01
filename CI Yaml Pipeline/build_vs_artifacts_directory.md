
# 🟦 Build.SourcesDirectory vs System.ArtifactsDirectory — Explained with Emojis 🚀

Understanding the difference between these two Azure DevOps paths is critical, especially when working with **Docker builds**, **artifact downloads**, and **multi-stage pipelines**.

---

# 🟦 1️⃣ `$(Build.SourcesDirectory)`  
### 📌 **This is your repository folder — where your code lives**

Example path on the agent:
```
/home/vsts/work/1/s
```

### ✔ Contains:
- Your repo files  
- Your `Dockerfile`  
- Your Maven/Node/Python project  
- Your YAML pipeline  

### ⭐ Best used when:
You want downloaded artifacts (like JARs) available **next to your Dockerfile**.

### 🔥 Ideal for Docker builds:
```
downloadPath: '$(Build.SourcesDirectory)'
```

---

# 🟩 2️⃣ `$(System.ArtifactsDirectory)`  
### 📌 **This is Azure DevOps artifact storage folder on the agent**

Example path:
```
/home/vsts/work/1/a
```

### ✔ Contains:
- Artifacts downloaded from previous stages  
- Files published using `PublishBuildArtifacts@1`  

### ⭐ Best used for:
- Deployment stages  
- Storing build outputs separate from source code  
- Multi-artifact pipelines  

⚠️ **Not ideal for Docker builds** unless Dockerfile is adjusted.

---

# 🟥 Why Docker Build Fails When Using System.ArtifactsDirectory

If your Dockerfile expects:

```dockerfile
COPY drop/*.jar app.jar
```

And your downloaded JAR is here:

```
/home/vsts/work/1/a/drop/*.jar
```

But Dockerfile is here:

```
/home/vsts/work/1/s/Dockerfile
```

👉 Docker **cannot find** the `.jar` file  
👉 `COPY failed: no source files were specified`  
👉 Docker build fails ❌

---

# 🟦 Summary Table

| Feature | `$(Build.SourcesDirectory)` | `$(System.ArtifactsDirectory)` |
|--------|------------------------------|--------------------------------|
| Contains repo code | ✔ Yes | ❌ No |
| Contains Dockerfile | ✔ Yes | ❌ No |
| Good for Docker builds | ⭐ YES | ⚠️ No |
| Good for artifact downloads | ✔ Yes | ✔ Yes |
| Isolated from repo | ❌ No | ✔ Yes |
| Example path | `/home/vsts/work/1/s` | `/home/vsts/work/1/a` |

---

# 🟢 Final Recommendation

### 🟩 For Docker build stage:
Use:
```
downloadPath: '$(Build.SourcesDirectory)'
```

### 🟦 For Deployment stages:
Use:
```
downloadPath: '$(System.ArtifactsDirectory)'
```

---

# 🎯 In Simple Terms

| Path | Meaning |
|------|---------|
| **Build.SourcesDirectory** | “My code folder” |
| **System.ArtifactsDirectory** | “My artifacts folder” |

---

If you want, I can also generate a **diagram** showing how artifacts flow from Build → Publish → Download → Docker. 😎
