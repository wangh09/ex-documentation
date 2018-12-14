## Prerequisties

* Kubrenetes Cluster 
* A kubectl client configured connected to Kubernetes Cluster

---

## Deploy processuer

* These deploy files could be found here.  http://gitlab.ziggurat.cn/ink-assets/devops-scripts/tree/master/k8s-deployment/monitor/dashboard
* Deploy the kubernetes dashboard 

```
#kubectl apply -f kubernetes-dashboard.yaml

OUTPUT like this

secret "kubernetes-dashboard-certs" created
serviceaccount "kubernetes-dashboard" created
role "kubernetes-dashboard-minimal" created
rolebinding "kubernetes-dashboard-minimal" created
deployment "kubernetes-dashboard" created
service "kubernetes-dashboard" created
```

* Deploy  heapster to enable container cluster monitoring and performance analysis

```
#kubectl apply -f heapster.yaml

OUTPUT like this

serviceaccount "heapster" created
deployment "heapster" created
service "heapster" created
```

* Deploy the  influxdb backend for heapster

```
#kubectl apply -f influxdb.yaml

OUTPUT like this

deployment "monitoring-influxdb" created
service "monitoring-influxdb" created
```

* Create the heapster cluster role binding for the dashboard

```
#kubectl apply -f heapster-rbac.yaml

OUTPUT like this

clusterrolebinding "heapster" created
```

* Create an eks-admin Service Account and Cluster Role Binding

```
#kubectl apply -f eks-admin-service-account.yaml

OUTPUT like this

serviceaccount "eks-admin" created
```

* Create an eks-admin-cluster-role-binding and apply it

```
#kubectl apply -f eks-admin-cluster-role-binding.yaml

OUTPUT like this

clusterrolebinding "eks-admin" created
```

* Connect to dashboard

```

#kubectl get svc -nkube-system -o wide | grep kubernetes-dashboard

#kubectl -n kube-system describe secret $(kubectl -n kube-system get secret | grep eks-admin | awk '{print $1}')
```

Get kubernetes aws dashboard domain by kubectl get svc command. and bind your dns record to kubernetes dashboard

Get token by kubectl describe secret above and paste it to Token choice

![](/assets/dashboard-token-auth.png)

* And now it works





