## Setup

```bash
kubectl create namespace argocd
brew install argoproj/tap/argocd
```


## Start

```bash
kustomize build manifests/overlays/ | kubectl apply -n argocd -f -
```

## Stop

```bash
kustomize build manifests/overlays/ | kubectl delete -n argocd -f -
```

## APIサーバーへのアクセス

参考) https://argoproj.github.io/argo-cd/getting_started/#3-access-the-argo-cd-api-server

ローカルで動かすにはargo-serverに対して 8080:443 でPortForwardingすれば十分。ただし、serviceに対してPortForwardingする必要があるためk9sが使えないことに注意


```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

### TODO:
- Ingress Configuration
  - https://argoproj.github.io/argo-cd/operator-manual/ingress/


## パスワードの取得

Argo CDデフォルトでローカルユーザーadminが作成される｡パスワードはargocd-serverのPod名なので確認する｡

```bash
kubectl get pods -n argocd -l app.kubernetes.io/name=argocd-server -o name | cut -d'/' -f 2
```

## ログイン

`https://localhost:8080/` にアクセスしユーザー名とパスワードを入力する

user: admin
password: 先ほど取得したパスワード


## Appの作成


### TODO
- Declarative Setup


