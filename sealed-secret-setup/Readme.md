# Sealed Secret Installation

The latest instructions can be found [here](https://github.com/bitnami-labs/sealed-secrets).

```bash
helm repo add sealed-secrets https://bitnami-labs.github.io/sealed-secrets
helm install sealed-secrets -n kube-system --set-string fullnameOverride=sealed-secrets-controller sealed-secrets/sealed-secrets
```

Install the kubeseal cli. The latest instructions can be found [here](https://github.com/bitnami-labs/sealed-secrets?tab=readme-ov-file#linux).

```bash
KUBESEAL_VERSION='0.25.0' # Set this to, for example, KUBESEAL_VERSION='0.23.0'
wget "https://github.com/bitnami-labs/sealed-secrets/releases/download/v${KUBESEAL_VERSION:?}/kubeseal-${KUBESEAL_VERSION:?}-linux-amd64.tar.gz"
tar -xvzf kubeseal-${KUBESEAL_VERSION:?}-linux-amd64.tar.gz kubeseal
sudo install -m 755 kubeseal /usr/local/bin/kubeseal
```  

## Usage

Seal a secret. The command uses the public key that lives as a resource within the cluster to encrypt the secret. The resulting sealed secret can only be decrypted using the private key.
Make sure the access to the private key is restricted! The sealed secret can be made public / be commited. See [this](https://github.com/bitnami-labs/sealed-secrets?tab=readme-ov-file#usage) section of the readme for further information.

```bash
kubeseal -f mysecret.yaml -w mysealedsecret.yaml 
```

You will have to run this after installing/resetting the sealed secret operator in order to replace the sealed secret file under `demo-app/overlays/dev/mysealedsecret.yaml`.

> **_NOTE:_** Of course you do not want to commit the secret itself, like `mysecret.yaml` here. You can though savely commit the sealed secret.
