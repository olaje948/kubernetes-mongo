# 🚀 Kubernetes + Minikube  
## Deploying MongoDB & Mongo-Express (Step-by-Step Guide)

This guide explains how to deploy **MongoDB** and **Mongo-Express** on **Minikube** using Kubernetes manifests.

---

## 📌 1. Start Fresh (Optional – Reset Minikube)

```bash
minikube delete --all
```

---

## 📌 2. Start Minikube

```bash
minikube start --driver=docker
```

---

## 📌 3. Apply MongoDB Deployment & Service

```bash
kubectl apply -f mongo.yml
```

---

## 📌 4. Apply Mongo-Express Deployment & Service

```bash
kubectl apply -f mongo-express.yml
```

---

## 📌 5. Access Mongo-Express via Minikube Service

```bash
minikube service mongo-express-service
```

This will print a URL like:

```
http://127.0.0.1:30001
```

---

## 📌 6. Optional: Port-Forward Mongo-Express Service

```bash
kubectl port-forward service/mongo-express-service 30001:8081
```

Visit:

```
http://localhost:30001
```

---

## 📌 7. Check Pods

```bash
kubectl get pods
```

---

## 📌 8. Check Services

```bash
kubectl get service
# or
kubectl get svc
```

---

## 📌 9. Check Deployments

```bash
kubectl get deployment
```

---

## 📌 10. Debugging / Troubleshooting

### Describe a Pod

```bash
kubectl describe pod <pod-name>
```

### Describe a Service

```bash
kubectl describe service mongo-express-service
```

### Describe a Deployment

```bash
kubectl describe deployment mongo-express-deployment
```

---

# ⚡ Notes & Tips

- Use:

```bash
kubectl get pods -o wide
```

to see node assignments and Pod IPs.

- Minikube uses the **Docker** driver by default; you can change it if needed.

- **Production Warning:**  
  Avoid storing passwords directly in YAML files.  
  Use Kubernetes Secrets:

```bash
kubectl create secret generic mongo-secret   --from-literal=username=admin   --from-literal=password=pass123
```