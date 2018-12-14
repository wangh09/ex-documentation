# Deploy the app system

Before you proceed the deployment, pls read the step-by-step configuration first to configure your exchange.

## 1. Init the namespace

```
 bash init-namespace.sh
```

## 2. Deploy the registry

```
kubectl apply -f registry/jhipster-registry.yml
```

You don't need the jhipster-ingress.yml if you are don't want to expose registry on public network.

There may be errors before the registries ready, but don't worry, it is because the registries can not contact each other before they are all up.

After the registry startup and produces:

![](/assets/registry.png)One can login to the registry by username=admin and password set in registry-admin-password. \(You will not see the following page if you don't expose registry to public.\)

![](/assets/registry-panel.png)

You can check if there is format error of the config files through Configuration-&gt;Cloud config.

\(In production deployment, the ingress for registry should be disabled.\)

## 3. Deploy the UAA \(User Account and Authentication\)

```
 kubectl apply -f backend-uaa/backend-uaa.yml
```

## 4. Deploy services

```
 kubectl apply -f backend-ex-service-mapi/backend-ex-service-mapi.yml
 kubectl apply -f backend-ex-service-ui/backend-ex-service-ui.yml
```

## 5. Deploy the gateways

```
kubectl apply -f backend-ex-gateway-ui/backend-ex-gateway-ui.yml
```

After the gateway-ui startup, it can be accessed from the web. \(also, you need to ingress or loadbalancer to expose it\)

![](/assets/gateway-ui.png)

it can be seen from the gateway page that all the three paths are up, then the backend for the ui frontend is up.

In production deployment, the ingress for gateway should be disabled.

## 6. Deploy the frontend

```
kubectl apply -f backend-ex-gateway-ui/frontend-web.yaml
```

It should be pointed out that the frontend-web is exposed by using NodePort, so the LoadBalance to access the exchange system should be configured correctly. See more information in Configure LoadBalancer. 

## 7. Deploy the api gateway \(Optional\)

If you want to enable api trading, then the api gateway needs to be deployed.

```
kubectl apply -f backend-ex-gateway-api
```

## 8. Deploy the admin panel

```
kubectl apply -f manage-ex-whole/manage-ex-gateway.yml
[after manage gateway run up]
kubectl apply -f manage-ex-whole/manage-ex-backend.yml
kubectl apply -f manage-ex-whole/manage-web.yml
```



