## Prerequire

* Match module needs  a slave as backup. 
* The slave ip is from configuration. the match module will check its ip and host. once the slave ip is the same with host. then it will start later maybe and being a slave module.

---

## Solution

* Add a label to a node to specify the node as a slave match host.

* Label **nodeSelector** to slave match configuration yaml and flag **hostNetwork** to true to switch  network to host, then the slave module could use host IP.

---

## Test

* Run the command below to labe node

```
kubectl label node ip-192-168-216-84.us-west-2.compute.internal node=match-slave
```

* Run the test deployment below

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      hostNetwork: true  //specify network method
      nodeSelector:      //bind to label node
        node: match-slave
      containers:
      - name: nginx
        image: nginx:1.15.4
        ports:
        - containerPort: 80
```

* Run command 'kubectl get pod -o wide  ' to check pod ip address. you will see the node ip is the same with node ip.



