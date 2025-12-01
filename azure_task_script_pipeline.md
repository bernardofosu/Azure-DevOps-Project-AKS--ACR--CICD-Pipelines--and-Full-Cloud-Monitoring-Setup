# 🟦 There Are 2 Types of Steps in Azure DevOps Pipelines

## 🔵 1️⃣ TASK-BASED STEPS (Pre-Built Tasks)

### ✔️ What They Are
Tasks are ready‑made Azure DevOps extensions (Microsoft or marketplace).

Examples:
- Maven@4
- CmdLine@2
- SonarQubePrepare@7
- SonarQubeAnalyze@7
- PublishBuildArtifacts@1

### ✔️ Characteristics
- Use `task:` keyword  
- Require `inputs:`  
- Provide automation features  
- Tool setup handled for you  

### ✔️ When to Use
- When the tool has a built‑in task  
- When you want automatic configuration  
- When you want clean, safe pipelines  

---

## 🔵 2️⃣ SCRIPT-BASED STEPS (Raw Shell Commands)

### ✔️ What They Are
Direct shell commands executed in the agent terminal.

### ✔️ Example
```
- script: mvn package
  displayName: "Package App"
```

### ✔️ Characteristics
- No inputs  
- Raw CLI execution  
- Requires tools installed on the agent  

### ✔️ When to Use
- No Azure DevOps task exists  
- Running custom tools (Trivy, Terraform, Helm)  
- Full manual control required  

---

# 🟩 Quick Comparison

| Feature | Task-Based Step | Script Step |
|--------|------------------|-------------|
| Syntax | task: | script:/bash: |
| Needs Inputs? | ✔ Yes | ❌ No |
| Needs tool installed? | ❌ Often No | ✔ Yes |
| Azure DevOps auto‑config | ✔ Yes | ❌ No |
| Best for beginners | ✔ Yes | ⚠️ Moderate |

---

# 🟦 Let me confirm it clearly so there is zero confusion:

## 🟦 ✔️ If you do NOT use a Maven task…
Example:
```
- script: mvn package
```

### This means:
- Runs as a normal shell command  
- Requires Maven installed on the agent  
- Requires Java installed  
- No automatic features  
- If Maven missing → ❌ `mvn: command not found`

---

## 🟦 ✔️ If you DO use the Maven task…
Example:
```
- task: Maven@4
  inputs:
    goals: 'package'
```

### This means:
- No need to install Maven manually  
- Azure DevOps handles Java version  
- Built‑in support for JUnit, coverage, authentication  
- Fully automated & best practice  

---

# 🟩 Memory Trick

### **TASK = TOOL**
Azure DevOps handles configuration.

### **SCRIPT = SHELL**
You must install & configure everything yourself.
