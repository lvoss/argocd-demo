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

Create an argo-application via the ui.

1. Click `new app`.
2. In the top right select `Edit as yaml`.
3. Paste in the content of `demo-dev-application.yaml` located in `argocd-setup/`.
4. Create the application.
5. Repeat the same for the `demo-prod-application.yaml`.
