
# 🟦 Search for Publish → Publish Build Artifacts  
# 🟦 Search for Download → Download Build Artifacts  

---

# 🟦 1️⃣ Publish Build Artifacts Task (Uploads files for next stages)

🔍 **Search keyword:** `publish`  
🧰 **Task name:** **Publish build artifacts**

This task is used in the **build stage** to upload the JAR or any files so the **Docker stage** (or any later stage) can download them.

---

## 📝 What this task does
- 📤 Takes files from a folder (ex: `target/`)
- ☁ Uploads them to **Azure DevOps Artifacts Container**
- 🔗 Makes them available to later stages

---

## 🟦 UI Fields Explained

| Field | Meaning |
|------|---------|
| **Path to publish** | The folder that will be uploaded (ex: `target/`) |
| **Artifact name** | The name Azure DevOps gives to the artifact (ex: `drop`) |
| **Artifact publish location** | Default = `Azure Pipelines (Container)` |

---

## 🟦 YAML Generated

```yaml
- task: PublishBuildArtifacts@1
  inputs:
    PathtoPublish: '$(Build.ArtifactStagingDirectory)'
    ArtifactName: 'drop'
    publishLocation: 'Container'
```

---

# 🟦 2️⃣ Download Build Artifacts Task (Downloads the artifact for next stage)

🔍 **Search keyword:** `download`  
🧰 **Task name:** **Download build artifacts**

This task is used in the **Docker stage** to pull the artifact built previously.

---

## 📝 UI Fields Explained

| Field | Meaning |
|------|---------|
| **Download artifacts produced by** | Usually `Current build` |
| **Download type** | `Specific artifact` |
| **Artifact name** | Use the same name you published earlier → `drop` |
| **Matching pattern** | `**` (download everything) |
| **Destination directory** | Where to put the downloaded files |

---

## 🔥 Best Destination Choices

| Variable | Meaning |
|----------|---------|
| `$(System.ArtifactsDirectory)` | ✔ Best practice — clean location for artifacts |
| `$(Build.SourcesDirectory)` | Downloads into the repo folder |

Both work — but **System.ArtifactsDirectory** is recommended.

---

## 🟦 YAML Generated

```yaml
- task: DownloadBuildArtifacts@0
  inputs:
    artifactName: 'drop'
    downloadPath: '$(System.ArtifactsDirectory)'
```

---

# 🟩 FINAL SUMMARY

| Step | Task | Purpose |
|------|------|---------|
| **1. Build stage** | 🟦 Publish Build Artifacts | Upload JAR → Azure Artifacts |
| **2. Docker stage** | 🟦 Download Build Artifacts | Download JAR → Used in Dockerfile |

---

If you want, I can add diagrams or combine all DevOps notes into one file.
