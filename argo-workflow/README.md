
## Setup

```bash
$ brew install argoproj/tap/argo
$ kubectl create namespace argo
$ kubectl create rolebinding default-admin --clusterrole=admin --serviceaccount=argo:default --namespace=argo
```

https://github.com/argoproj/argo/blob/master/docs/configure-artifact-repository.md

```bash
$ brew install helm # mac, helm 3.x
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com/ # official Helm stable charts
$ helm repo update
```

## 起動

```bash
$ helm install argo-artifacts stable/minio \
    --namespace argo \
    --set service.type=LoadBalancer \
    --set defaultBucket.enabled=true \
    --set defaultBucket.name=argo-workflow-example \
    --set persistence.enabled=false \
    --set fullnameOverride=argo-artifacts
$ kubectl apply -n argo -f install.yaml -f workflow-controller-configmap.yaml
```

## 停止

```bash
$ kubectl delete -n argo -f install.yaml
$ helm uninstall argo-artifacts --namespace argo
```

## Workflowの実行

```bash
$ argo submit tasks/artifacts.yaml -n argo
```