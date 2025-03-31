
# infra-nginx-ingress-trial

This Helm chart deploys a custom NGINX Ingress Controller with specific configurations to meet the requirements outlined in the engineering task.

## ✅ Project Summary

This chart:
- Deploys the latest NGINX Ingress Controller (`v1.12.1`)
- Is configured to **only watch ingresses** with annotation `nginx-trial`
- Includes custom values to configure the controller, admission webhook, service, and backend

## 📦 Chart Structure

```
infra-nginx-ingress-trial/
│
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── controller-deployment.yaml
│   ├── service.yaml
│   ├── admission-webhooks/
│   └── ...
└── README.md
```

## 🚀 How to Deploy

Make sure your local Kubernetes environment (e.g., Docker Desktop) is running.

1. **Install cert-manager** (if not already):
```bash
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install cert-manager jetstack/cert-manager --namespace cert-manager --create-namespace --version v1.13.2
```

2. **Install the chart**:
```bash
helm install infra-nginx-ingress-trial ./infra-nginx-ingress-trial
```

3. **Check the services**:
```bash
kubectl get svc -n default -l app.kubernetes.io/component=controller
```

4. **Port forward to access from localhost**:
```bash
kubectl port-forward svc/infra-nginx-ingress-trial-controller 8080:80
```

5. **Apply the sample ingress**:
```bash
kubectl apply -f demo-ingress.yaml
```

## 🧪 Sample Ingress

See the `demo-ingress.yaml` file for a sample ingress using annotation:

```yaml
metadata:
  annotations:
    kubernetes.io/ingress.class: nginx-trial
spec:
  ingressClassName: nginx
```

## 📷 Screenshots

You can find screenshots attached, showing:
- Working NGINX Ingress (`default backend - 404`)
- Controller pod running
- Exposed services

## ✅ Status

- [x] Custom Helm chart working
- [x] Only watches annotated ingresses (`nginx-trial`)
- [x] Tested on local Kubernetes
- [x] Screenshot proofs included
