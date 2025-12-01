
# 🟦 Azure DevOps Pipeline Errors & Fixes (Complete Notes)

This document explains **all the errors**, **error snippets**, and **how we solved each one** in your Azure DevOps pipeline.

---

## 🟥 ERROR #1 — COPY failed: no source files were specified

### 🔻 Error Snippet
```
COPY failed: no source files were specified
```

### 🔻 Cause  
Dockerfile expected the JAR in:
```
target/*.jar
```
But Azure DevOps stages do **not share files**, so the Docker stage could NOT find the JAR.

### 🟩 Fix  
1️⃣ **Publish artifact:**  
```yaml
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: 'target'
    artifactName: 'drop'
```

2️⃣ **Download artifact:**  
```yaml
- task: DownloadBuildArtifacts@0
  inputs:
    artifactName: 'drop'
    downloadPath: '$(Build.SourcesDirectory)'
```

3️⃣ **Fix Dockerfile COPY path:**  
```dockerfile
COPY drop/*.jar $APP_HOME/app.jar
```

---

## 🟥 ERROR #2 — YAML Indentation Problems

### 🔻 Wrong
```yaml
inputs:
artifactName: 'drop'
```

### 🟩 Correct
```yaml
inputs:
  artifactName: 'drop'
  downloadPath: '$(Build.SourcesDirectory)'
```

---

## 🟥 ERROR #3 — Missing Docker Repository Name

### 🔻 Cause
Docker@2 requires a repository name.

### 🟩 Fix
```yaml
repository: 'bofosu1/bankapp2'
```

---

## 🟥 ERROR #4 — No Artifact in Docker Stage

### 🔻 Cause
`mvn package` ran but was never published.

### 🟩 Fix
```yaml
- task: PublishBuildArtifacts@1
  inputs:
    pathToPublish: 'target'
    artifactName: 'drop'
```

---

## 🟥 ERROR #5 — Wrong Docker Build Context

### 🟩 Fix
```yaml
buildContext: '$(Build.SourcesDirectory)'
```

---

# 🟦 Final Working Dockerfile

```dockerfile
FROM adoptopenjdk/openjdk11

EXPOSE 8080
ENV APP_HOME=/usr/src/app

COPY drop/*.jar $APP_HOME/app.jar

WORKDIR $APP_HOME
CMD ["java", "-jar", "app.jar"]
```

---

# 🟩 Final Working Pipeline (Build + Docker)

```yaml
- stage: build
  jobs:
  - job: build_job
    steps:
      - script: mvn package
      - task: PublishBuildArtifacts@1
        inputs:
          pathToPublish: 'target'
          artifactName: 'drop'

- stage: docker_build_push
  dependsOn: build
  jobs:
  - job: build_push_job
    steps:
      - task: DownloadBuildArtifacts@0
        inputs:
          artifactName: 'drop'
          downloadPath: '$(Build.SourcesDirectory)'

      - task: Docker@2
        inputs:
          containerRegistry: 'docker-conn'
          repository: 'bofosu1/bankapp2'
          command: 'buildAndPush'
          Dockerfile: '**/Dockerfile'
          buildContext: '$(Build.SourcesDirectory)'
```

---

# 🎉 End of Notes
Everything is now documented and solved.
