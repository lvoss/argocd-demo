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
4. Click Save and then create the application.
5. Repeat the same for the `demo-prod-application.yaml`.

## Renew the sealed secrets

As the sealed secrets are created with a public key that lives in your cluster, changing a cluster leads to the sealed secret not being decryptable.
Renew them as described in `sealed-secret-setup/Readme.md`. For now, you have to renew the sealed secret file `demo-app/overlays/dev/mysealedsecret.yaml`.
