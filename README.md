# argocd-two-clusters

## ArgoCD Helm <https://github.com/argoproj/argo-helm/tree/main/charts/argo-cd>

```sh
helm repo add argo https://argoproj.github.io/argo-helm
helm repo update argo 
helm search repo argo 
```

## Kind

```sh
kind create cluster --name=maestro --config ./kind.yaml
kubectl cluster-info --context kind-maestro
```

## argocd

```sh
kubectl create namespace argocd
helm install argocd argo/argo-cd --namespace argocd
```

### argocd cli

```sh
curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd
rm argocd-linux-amd64
```

```txt
PS C:\Users\Dell\Documents\Projetos\argocd-two-clusters> helm install argocd argo/argo-cd --namespace argocd
NAME: argocd
LAST DEPLOYED: Tue May 16 17:21:32 2023
NAMESPACE: argocd
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
In order to access the server UI you have the following options:

1. kubectl port-forward service/argocd-server -n argocd 8080:443

    and then open the browser on http://localhost:8080 and accept the certificate

2. enable ingress in the values file `server.ingress.enabled` and either
      - Add the annotation for ssl passthrough: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-1-ssl-passthrough
      - Set the `configs.params."server.insecure"` in the values file and terminate SSL at your ingress: https://argo-cd.readthedocs.io/en/stable/operator-manual/ingress/#option-2-multiple-ingress-objects-and-hosts


After reaching the UI the first time you can login with username: admin and the random password generated during the installation. You can find the password by running:

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | ForEach-Object { [System.Text.Encoding]::Utf8.GetString([System.Convert]::FromBase64String($_)) }

gpLUiYpmzjFdB9Wo

(You should delete the initial secret afterwards as suggested by the Getting Started Guide: https://argo-cd.readthedocs.io/en/stable/getting_started/#4-login-using-the-cli)
```

```txt
kubectl get crds -l app.kubernetes.io/part-of=argocd     
>>
NAME                          CREATED AT
applications.argoproj.io      2023-05-16T20:21:34Z
applicationsets.argoproj.io   2023-05-16T20:21:34Z
appprojects.argoproj.io       2023-05-16T20:21:34Z
```

## 201 App of Apps

## apprentice

kubectl apply -f <https://raw.githubusercontent.com/afonsoaugusto/argocd-two-clusters/main/gitops-cert-level-2-examples/app-of-apps/root-app/my-application.yml> -n argocd



