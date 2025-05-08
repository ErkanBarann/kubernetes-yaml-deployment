# Kubernetes Deployment: Flask App with MySQL and NGINX Ingress

This project demonstrates the Kubernetes-based deployment of a containerized Flask web application, backed by a MySQL database and exposed via an NGINX Ingress Controller. It is designed to transition a typical multi-container application from Docker Compose to a modular, production-grade Kubernetes setup using declarative YAML manifests.

---

## 🔧 Project Components

The architecture includes:

- **Flask Application**: Python backend web service.
- **MySQL Database**: Persistent data storage layer.
- **NGINX Ingress Controller**: Manages external HTTP traffic routing.

All components are defined and deployed using Kubernetes resources for scalability, security, and maintainability.

---

## ⚙️ Kubernetes Resources

This setup includes:

- `Deployments`: For Flask and MySQL workloads.
- `Services`: Internal networking for app and database communication.
- `Ingress`: HTTP entry point using NGINX controller.
- `PersistentVolume` and `PersistentVolumeClaim`: To persist database data.
- `ConfigMap` and `Secret`: To externalize and secure configuration.
- `Namespace`: Logical grouping of related resources.

---

## 🚀 Deployment Workflow

1. **Prepare your Kubernetes cluster** (Minikube or any cloud provider).
2. **Install the NGINX Ingress Controller**:
   ```bash
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/cloud/deploy.yaml
   ```
3. **Create a Namespace** (e.g., `flask-app`) to isolate the environment.
4. **Apply all YAML manifests** in sequence:
   ```bash
   kubectl apply -f manifest-files/
   ```
5. **Verify deployments, services, PVCs, and ingress**.
6. **Access the app** using the host defined in the `Ingress` resource.

---

## 🌐 Example Ingress Resource

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: flask-app-ingress
  namespace: flask-app
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: flask-app.erkanbaran.me
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: flask-service
            port:
              number: 8000
```

---

## 📦 Outcome

This project delivers a fully functional Kubernetes environment for a multi-tier application, showcasing secure service communication, persistent storage, external traffic routing, and clean resource organization through namespaces.

