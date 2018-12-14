## Prerequisit

* Match module HA mechanism. configure match configuration slave ip and match application will check this ip and slave ip. if slave ip is the same with its host IP. then the match role will be slave match application
* Method to get slave IP by kubernetes. label node as a match host and configure slave match application hostNetwork to be true

---

## Test processure

1 Label node   kubectl label nodes match-node node=match-slave

2 configure nginx example yaml

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
      hostNetwork: true
      nodeSelector:
        node: match-slave
      containers:
      - name: nginx
        image: nginx:1.15.4
        ports:
        - containerPort: 80
```

Notice 'nodeSelector' and 'hostNetwork'. nodeSelector will locate application to the specified host. and hostNetwork will grant application to hostwork.

3 kubectl get node -owide   you will see that the application IP is the same with the specified node



