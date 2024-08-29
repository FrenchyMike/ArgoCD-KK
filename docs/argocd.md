# ArgoCD

## Installation

### Using manifest

* Requirement: create a dedicated namespace: `kuebctl create ns argocd`

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### Using helm

```bash
## Install chart
helm repo add argo https://argoproj.github.io/argo-helm 

## Install repository
helm install my-argo-cd argo/argo-cd --version 4.8.0
```


## ArgoCD GUI

Once everythings is installed you can browse the ArgoCD GUI:

Expose your service:

1. Using `kubectl` command
    ```bash
    kubectl port-forward -n argocd services/argocd-server 8080:80
    ```

2. If you are using minikube:
    ```bash
    minikube service argocd-server --url --namespace argocd
    ```
## Get admin password

Get the admin password
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" base64 -d
```

### CLI

#### Download and install binary

```bash
curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64

chmod +x /usr/local/bin/argocd
```

#### Configure

```bash
export ADMIN_USER="admin"
export ADMIN_PASSWORD=$(kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d)
export 

argocd login --insecure --username ${ADMIN_USER} --password ${ADMIN_PASSWD} ${ARGOCD_SERVER_URL}:${ARGOCD_SERVER_PORT}
```
