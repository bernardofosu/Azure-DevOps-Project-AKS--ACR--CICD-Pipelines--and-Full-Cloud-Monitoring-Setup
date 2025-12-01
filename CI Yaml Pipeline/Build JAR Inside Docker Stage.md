# 🟦 Build JAR Inside Docker vs Artifact Method — Notes with Emojis

This document explains the **Docker build strategy**, the **artifact issues**, and how using the **“build JAR again inside Docker”** method solves everything.

---

# 🟥 The Old Problem — Artifact COPY Errors

You kept seeing:

```
COPY failed: no source files were specified
```

This happened because:

- Maven built the JAR in the **build stage**
- Docker runs in a **different stage**
- Stages do **NOT share files**
- So Docker could not find `target/*.jar`
- You had to publish & download artifacts manually

This caused:
❌ wrong paths  
❌ wrong COPY locations  
❌ YAML indentation issues  
❌ complexity

---

# 🟩 The Simpler Solution — Build the JAR Inside Docker

Instead of:

- building the JAR in the pipeline
- publishing artifacts
- downloading artifacts
- copying from `drop/`

You simply let Docker **build the JAR again**.

This is MUCH easier.

---

# 🟦 Example Pipeline (simple)

```yaml
- stage: Docker
  displayName: "Docker Stage"
  jobs:
    - job: DockerJob
      displayName: "Docker Job"
      pool:
        name: Aditya
        demands:
          - agent.name -equals agent-1
      steps:
        - script: mvn package
          displayName: "Build-Package-Step"

        - task: Docker@2
          inputs:
            containerRegistry: "docker-svc"
            repository: "adijaiswal/santa"
            command: "buildAndPush"
            Dockerfile: "**/Dockerfile"
            tags: "latest"
```

✔ Maven builds locally → JAR appears in `target/`  
✔ Docker sees the JAR → COPY works  
✔ No artifacts required

---

# 🟦 Example Dockerfile

```dockerfile
FROM adoptopenjdk/openjdk11
EXPOSE 8080
ENV APP_HOME=/usr/src/app
WORKDIR $APP_HOME
COPY target/*.jar app.jar
CMD ["java", "-jar", "app.jar"]
```

✔ Docker copies the JAR from `target/`  
✔ No artifact problems

---

# 🟦 Benefits of This Method

### ✔ Simpler pipeline

### ✔ No artifact publishing

### ✔ No artifact downloading

### ✔ No `drop/ vs target/` issues

### ✔ No broken COPY path

### ✔ Docker builds reliably every time

---

# 🟦 When to Use This Method?

Use `mvn package` in the Docker stage when:

- Your app compiles quickly
- You want the simplest working pipeline
- You want to avoid artifact management headache

This is perfect for learning DevOps and small–medium projects.

---

# 🟩 Summary

| Method                  | Pros             | Cons                                 |
| ----------------------- | ---------------- | ------------------------------------ |
| **Artifact Method**     | Real CI/CD flow  | More complex, easy to break          |
| **Build Inside Docker** | Simple, reliable | Builds twice (optional disadvantage) |

---

# 🎉 Final Result

You now understand:

- Why artifact method broke
- Why COPY failed
- Why building inside Docker fixes everything
- How to implement the clean pipeline

Your pipeline is now **working AND simplified**. 🚀🔥
