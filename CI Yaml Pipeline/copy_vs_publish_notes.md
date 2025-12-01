
# 🟦 CopyFiles@2 vs PublishBuildArtifacts@1 — Azure DevOps Explained 💡

Understanding the difference between **CopyFiles@2** and **PublishBuildArtifacts@1** is crucial when building multi‑stage CI/CD pipelines.  
They may look similar, but they serve *very* different purposes.

---

## 🟦 1️⃣ CopyFiles@2 — LOCAL Copy Inside the Build Agent

This task **only moves files inside the build machine** (the running agent).  
It does **NOT** send anything to Azure DevOps storage.

### ✔ Example
```yaml
- task: CopyFiles@2
  inputs:
    SourceFolder: '$(Build.SourcesDirectory)/target'
    Contents: '**'
    TargetFolder: '$(Build.ArtifactStagingDirectory)'
```

### ✔ What it really does
- Copies files from folder **A → B**
- Only inside the **current agent machine**
- Files cannot be downloaded by future stages unless published

### 🔥 Use Case
- Preparing a folder before publishing  
- Organizing files locally  
- Preparing temp files for packaging

### ❌ Not for:
- Multi-stage pipelines  
- Docker build stage  
- Deployment

---

## 🟩 2️⃣ PublishBuildArtifacts@1 — Upload to Azure DevOps Artifacts Storage

This task **uploads** your files to Azure DevOps so other stages can download them.

### ✔ Example
```yaml
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: 'target'
    artifactName: 'drop'
  displayName: 'Publish JAR Artifact'
```

### ✔ What it really does
- Takes files from `target/`
- Uploads them to **Azure DevOps Artifacts**
- Creates an artifact called **drop**
- Available to:
  - later stages (Docker)
  - release pipelines
  - manual download in the UI

### ⭐ Required for:
- Multi-stage builds  
- Docker image builds  
- Deployments  
- Release pipelines  

---

## 🟧 3️⃣ Why Both Tasks Exist

| Purpose | CopyFiles@2 | PublishBuildArtifacts@1 |
|---------|-------------|--------------------------|
| Move files locally | ✔ Yes | ❌ No |
| Upload to DevOps | ❌ No | ✔ Yes |
| Used by other stages | ❌ No | ✔ Yes |
| Required for Docker stage | ❌ No | ✔ Yes |
| Temporary inside agent | ✔ Yes | ❌ No |
| Creates downloadable artifact | ❌ No | ✔ Yes |

---

## 🟦 4️⃣ Correct Pipeline Flow Example

### 🏗 Build Stage
```yaml
- script: mvn package
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: 'target'
    artifactName: 'drop'
```

### 🐳 Docker Stage
```yaml
- task: DownloadBuildArtifacts@0
  inputs:
    artifactName: 'drop'
    downloadPath: '$(Build.SourcesDirectory)'
- task: Docker@2
  inputs:
    command: buildAndPush
```

---

## 🟢 Final Summary

### ✔ Use **CopyFiles@2**  
➡ Only when you want to prepare or rearrange files *locally* inside the same stage.

### ✔ Use **PublishBuildArtifacts@1**  
➡ When you need the file in **another stage**, **another job**, **Docker**, or **release pipeline**.

### 🚀 Publish = Save to Azure  
### 📁 Copy = Move inside agent

---

If you want, I can also create a **diagram** showing artifact flow through Azure DevOps stages!
