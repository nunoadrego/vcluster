# vcluster
Playing with vcluster

## Requirements
- minikube
- kubectl
- vcluster cli (`brew install vcluster`)

## Start a K8s cluster
```
minikube start
```

## Install and run vclusters
Install two vclusters (`cluster-1` and `cluster-2`) with helm:
```
helm upgrade --install cluster-1 vcluster \
  --values vcluster.yaml \
  --repo https://charts.loft.sh \
  --create-namespace \
  --namespace cluster-1 \
  --kube-context minikube
```
```
helm upgrade --install cluster-2 vcluster \
  --values vcluster.yaml \
  --repo https://charts.loft.sh \
  --create-namespace \
  --namespace cluster-2 \
  --kube-context minikube
```

## List and interact with both clusters
List vclusters:
```
vcluster list
```

Connect to clusters (leave each terminal open):
```
vcluster connect cluster-1 --kube-config-context-name cluster-1 --context minikube
vcluster connect cluster-2 --kube-config-context-name cluster-2 --context minikube
```

And finally, list pods in both clusters, for example:
```
kubectl get pods --context cluster-1
```
```
kubectl get pods --context cluster-2
```

## Cleanup
Delete vclusters:
```
vcluster delete --delete-namespace cluster-1 --context minikube
vcluster delete --delete-namespace cluster-2 --context minikube
```

Delete K8s cluster:
```
minikube delete -p minikube
```
