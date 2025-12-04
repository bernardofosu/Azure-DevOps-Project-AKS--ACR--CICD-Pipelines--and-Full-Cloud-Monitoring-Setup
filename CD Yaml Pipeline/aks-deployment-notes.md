# 🚀 AKS Deployment Notes (Azure DevOps CI/CD)

## 1️⃣ Add `deploy_to_k8` Stage  
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
```

---

## 2️⃣ Install Kubectl in Your Pipeline  
Add the **Kubectl Installer** task under `steps`:

```yaml
    steps:
    - task: KubectlInstaller@0
      inputs:
        kubectlVersion: 'latest'
```

---

## 3️⃣ Update Your Docker Image Before Deployment  
Whenever you push a new image to Docker Hub:

- Update the tag in your `deployment-service.yaml`

Example:
```yaml
image: bofosu1/bankapp2:19
```

---

## 4️⃣ Deploy to AKS Using Your Kubernetes Service Connection (NO SECRETS)

In Azure DevOps → Pipeline UI, configure:

| Field | Value |
|-------|--------|
| Kubernetes service connection | `k8-svc-conn` |
| Namespace | `default` |
| Command | `apply` |
| Configuration type | File path |
| File path | `deployment-service.yaml` |

Equivalent YAML:
```yaml
- task: Kubernetes@1
  inputs:
    connectionType: 'Kubernetes Service Connection'
    kubernetesServiceConnection: 'k8-svc-conn'
    namespace: 'default'
    command: 'apply'
    useConfigurationFile: true
    configuration: 'deployment-service.yaml'
```

---

## 🎉 Final Notes  
- No Docker secrets are added in the pipeline.  
- Authentication is handled entirely by the **Service Connection (k8-svc-conn)**.  
- You only update:
  ✔ Docker image tag  
  ✔ YAML file  
  ✔ Run the pipeline  

This keeps the workflow clean and secure.
