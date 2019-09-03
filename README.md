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
