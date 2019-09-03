# Helm-Cheat-Sheet

## Install Helm and Tiller RBAC configuration
```
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > get_helm.sh

chmod +x get_helm.sh

./get_helm.sh
```
```
cat <<EoF > ~/rbac.yaml
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: tiller
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
  name: tiller
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
  - kind: ServiceAccount
    name: tiller
    namespace: kube-system
EoF
```
```
kubectl apply -f ~/rbac.yaml
```
```
helm init --service-account tiller
```

## Update Chart Repo
```
helm repo update
```
## Search Repo 

```
helm search 

ex: helm search nginx

```
## Install nginx Application
```
helm install --name nginxserver stable/nginx

```
## List nginx Application
```
helm list
```
## Delete nginx Application
```
helm delete --purge nginxserver

```
## To create new chart
```
helm create demo
```
## Upgrade nginx from demo chart
```
helm upgrade nginxserver ~/demo

```
## To check the status of upgrade
```
helm status nginxserver
```
## To check the history
```
helm histroy nginxserver
```
## To rollback to prevision version
```
helm rollback nginxserver 1
```

