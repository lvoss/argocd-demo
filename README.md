# ArgoCD Demo

## Install ArgoCD

```bash
kubectl create ns argocd
kubectl apply -k argocd-setup

kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data['password']}" | base64 -d
kubectl port-forward svc/argocd-server 8080:80 -n argocd
```

Open `http://localhost:8080` and login as admin:password-from-secret

## Configure
