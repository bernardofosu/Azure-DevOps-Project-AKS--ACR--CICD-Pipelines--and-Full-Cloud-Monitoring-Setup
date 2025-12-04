## 🚀 Deploying NGINX on Kubernetes (Imperative + Declarative)

### **1️⃣ Imperative Deployment (quick commands)**

#### **Create Deployment**

```bash
kubectl create deployment nginx --image=nginx
```

#### **Expose Deployment using LoadBalancer**

```bash
kubectl expose deployment nginx --port=80 --type=LoadBalancer
```

#### ⭐ What happens?

- A Deployment is created
- A Pod running NGINX starts
- A LoadBalancer service assigns a **public IP**

---

### **2️⃣ Declarative Deployment (YAML)**

Create a file:

`nginx-deploy.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx
          ports:
            - containerPort: 80
```

Apply it:

```bash
kubectl apply -f nginx-deploy.yaml
```

Create service:

`nginx-svc.yaml`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  type: LoadBalancer
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
```

Apply:

```bash
kubectl apply -f nginx-svc.yaml
```

---

## 🔍 Basic Commands to Check Status

### **Check Pods**

```bash
kubectl get pods
kubectl get pods -A
```

### **Check Services**

```bash
kubectl get svc
```

### **Describe Pod/Service**

```bash
kubectl describe pod nginx-xxxx
kubectl describe svc nginx
```

### **Check Deployment**

```bash
kubectl get deploy
```

### **Check LoadBalancer EXTERNAL-IP**

```bash
kubectl get svc nginx
```

You will see:

```
EXTERNAL-IP   4.246.235.246
```

---

## 🗑️ How to Delete Everything

### **Delete Imperative Deployment + Service**

```bash
kubectl delete deployment nginx
kubectl delete svc nginx
```

### **Delete Declarative Resources**

```bash
kubectl delete -f nginx-deploy.yaml
kubectl delete -f nginx-svc.yaml
```

### **Delete ALL resources in namespace**

```bash
kubectl delete all --all
```

⚠️ This deletes pods, services, deployments — everything.

---

If you'd like, I can add diagrams or flowcharts for the whole process!
