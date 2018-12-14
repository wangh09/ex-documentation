* Login to the jump server that can access the k8s cluster.
* List the pods:

```
kubectl get pods -n ex
```

![](/assets/ex_pods.png)

* Login to the centos pod

```
kubectl exec -it -n ex centos-c59bdc875-kxks9 /bin/bash
```

where the pod name is in the above picture.

* test if the wallet service can be accessed:

```
curl http://wallet-signing-service:3000
```

```
<html><body><form method="post" action="/init">
    <input name="password" placeholder="startup password" type="password" maxlength="32">
    <input name="ga" placeholder="GA code" type="text" maxlength="6">
    <button type="submit">OK</button>
</form></body></html>
```

* activate it by using the following command:

```
curl -d "password=123456&ga=123456" http://wallet-signing-service:3000/init
```

replace the password and ga by the startup password that you type when generating the wallet, and the GA code from your google authentication app. This GA is also configured when you generate the wallet.

