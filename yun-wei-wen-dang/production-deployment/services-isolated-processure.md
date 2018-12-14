## Prerequsite

* AWS network plugin is AWS-CNI. that needs to be changed to calico
* Run command to install calico-plugin:  kubectl apply -f [https://raw.githubusercontent.com/aws/amazon-vpc-cni-k8s/master/config/v1.2/calico.yaml](https://raw.githubusercontent.com/aws/amazon-vpc-cni-k8s/master/config/v1.2/calico.yaml)  

---

## Steps

* Check the data flow.
* Deploy the isolated networkpolicy. A example like this below

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  namespace: stars
  name: frontend-policy
spec:
  podSelector:
    matchLabels:
      role: frontend 
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              role: client
      ports:
        - protocol: TCP
          port: 80
```



