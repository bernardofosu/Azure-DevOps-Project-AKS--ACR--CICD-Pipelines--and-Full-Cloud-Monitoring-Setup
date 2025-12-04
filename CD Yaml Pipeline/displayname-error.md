
# 🚀 AKS Deployment Error Notes

## ❌ Error in Deploy Stage

The pipeline failed due to **incorrect placement of `displayName` inside the script block**.

### 🧨 Error Output

```bash
/home/ubuntu/myagent/_work/_temp/943e...sh: line 3: displayName:: command not found
##[error]Bash exited with code '127'.
```

This happened because `displayName` was written **inside** the multi‑line script block, causing bash to treat it as a command.

---

## ✅ Correct Fix

Move `displayName` *outside* the script block:

```yaml
- script: |
    echo "Updating image tag in deployment YAML..."
    sed -i "s|image: bofosu1/bankapp2:.*|image: bofosu1/bankapp2:$(Build.BuildId)|" deployment-service.yaml
  displayName: "Update Image Tag in YAML"
```

---

## 🎯 Why This Fix Works

- The `script:` block only accepts **shell commands**.
- Anything inside the block is executed by `bash`.
- `displayName` is not a bash command → error.
- Placing `displayName` at the correct YAML level fixes the issue.

---

## 🔧 Final Working Deploy Stage

```yaml
- stage: deploy_to_k8
  displayName: 'Deploy To K8'
  jobs:
  - job: deploy_k8_job
    displayName: 'Deploy To K8 Job'
    pool:
      name: nakodtech
      demands:
      - agent.name -equals Agent-1
    steps:
      - task: KubectlInstaller@0
        inputs:
          kubectlVersion: 'latest'

      - script: |
          echo "Updating image tag in deployment YAML..."
          sed -i "s|image: bofosu1/bankapp2:.*|image: bofosu1/bankapp2:$(Build.BuildId)|" deployment-service.yaml
        displayName: "Update Image Tag in YAML"

      - task: Kubernetes@1
        inputs:
          connectionType: 'Kubernetes Service Connection'
          kubernetesServiceEndpoint: 'k8-svc-conn'
          namespace: 'default'
          command: 'apply'
          useConfigurationFile: true
          configuration: 'deployment-service.yaml'
          secretType: 'dockerRegistry'
          containerRegistryType: 'Container Registry'
          dockerRegistryEndpoint: 'docker-conn'
```

---

## 🎉 You're now fully set for automated AKS image updates!
