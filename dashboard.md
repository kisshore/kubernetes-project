https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/
https://www.assistanz.com/steps-to-install-kubernetes-dashboard/


- Step 1. create dashboard 
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
```
- Step 2. vim dashboard-admin.yaml
```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRoleBinding
metadata:
   name: kubernetes-dashboard
   labels:
     k8s-app: kubernetes-dashboard
roleRef:
   apiGroup: rbac.authorization.k8s.io
   kind: ClusterRole
   name: cluster-admin
subjects:
- kind: ServiceAccount
  name: kubernetes-dashboard
  namespace: kube-system
```

- Step 3.  Create clusterrole
```
kubectl create -f dashboard-admin.yaml
```
- Step 4. start proxy
```
kubectl proxy --address='10.0.2.4' --accept-hosts='^*$'
```
- Step 5. Access dashboard via 
http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy
