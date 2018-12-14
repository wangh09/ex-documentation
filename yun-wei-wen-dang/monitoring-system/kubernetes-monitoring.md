## Prerequisties

* Kubrenetes Cluster

* A kubectl client configured connected to Kubernetes Cluster

---

## Deploy processuer

* ###### Prepare monitor yaml files located by : [http://gitlab.ziggurat.cn/ink-assets/devops-scripts/tree/master/k8s-deployment/monitor/fullstack-monitor](http://gitlab.ziggurat.cn/ink-assets/devops-scripts/tree/master/k8s-deployment/monitor/fullstack-monitor)
* ###### Because heapster is deprecated.  metric-server will be applied. And run the command to deploy metic-server: kubectl create -f metric-server/deploy/1.8+/
* ###### cd k8s-monitor
* ###### kubectl apply -f monitoring-namespace.yaml
* ###### kubectl apply -f prometheus-operator.yaml
* ###### kubectl get pods/svc -n monitoring   \#Check the pods or services
* ###### kubectl apply -f node\_exporter.yaml  \#Deploy node exporter
* ###### kubectl get pods/svc -n monitoring    \#Check node exporter status
* ###### kubectl apply -f kube-state-metrics.yaml
* ###### kubectl get pods/svc -n monitoring            \#Check state-metrics status
* ###### kubectl apply -f prometheus.yaml
* ###### kubectl get pods/svc -n monitoring           \#Check prometheus status
* ###### kubectl apply -f kube-servicemonitor.yaml
* ###### kubectl get pods/svc -n monitoring           \#Check servicemonitor status
* ###### kubectl apply -f grafana.yaml
* ###### kubectl get pods/svc -n monitoring
* ###### kubectl apply -f alertmanager.yaml
* ###### kubectl get pods/svc -n monitoring

## Grafana show

* Cluster status![](/assets/20180812204200.jpg)

* Cluster status from namespace![](/assets/20180812204208.jpg)

* Pod status![](/assets/20180812204217.jpg)



