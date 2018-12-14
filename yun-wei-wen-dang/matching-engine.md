# Deploy the matching engine

This guide is for initial setup of the matching engine, which describes the steps of the deployment as well as the check for each step. This guide should be used together with the devops-scripts project.

## 1. Settings

* 1.1 Setup gitlab configuration repo
  * Put the config repo onto the gitlab \(that has app/ for the App System, and match/ for the Matching Engine\), and generate a dedicated account to access it.
  * Change the git settings and encrypt key for the config server in the secrets.yaml. These settings need to be BASE64 encrypted.
* 1.2 Change the settings
  * Follow the step-by-step configuration to change the settings in the repo.
* 1.3 Prepare resources
  * Clean the rocketmq and redis if there is data in them.
  * Generate ex.sql, init-ex.sql by running the CryptoApiSchemaBuilder.java, and hd.sql by running the CryptoHDWalletSchemaBuilder.java. Run the sql files to initialize the db.
  * Change the endpoints in resource-\*.yaml.

## 2. Private-key generation

* 2.1 Into gen-hd-cold-wallet/src
* 2.2 Run 

```
npm install
```

* 2.3 Run the following command, and follow the instructions to generate private keys.

```
node app.js
```

* 2.4 write down the startup password, and add the GA secret to the google authenticator APP.
* 2.5 Copy the generated config\_hd.js and xpubkeys.json to k8s-development/matching/wallet/keys.

## 3. Setup the namespace

```
 kubectl apply -f ex-namespace.yaml
```

If you are using a private docker registry, you need to add the docker credential as follows.

```
 kubectl create secret docker-registry harbor-secret --docker-server=opsdocker.ziggurat.cn --docker-username=inkex-builder --docker-password=xxxx --docker-email=inkex-builder@ink.one -n ex
```

## 3. Setup and test the config server

* 3.1 Run the config server and test.

```
 kubectl apply -f secrets.yaml
 kubectl apply -f crypto-config.yaml
```

Check the log of the server.

```
 kubectl get pods -n ex
 kubectl logs -n ex -f crypto-config-***
```

go into the pod and test if it works:

```
kubectl exec -it -n ex crypto-config-*** /bin/bash
curl localhost:8888/api/test
```

curl [http://crypto-config-service:8888/api/test](http://crypto-config-service:8888/api/test)

If git is configured correctly, the configurations for crypto-api will be shown on the screen.

It should be pointed out that the BASE64 encryption of the secrets in k8s does not support special characters, so a better way is to encrypt the credentials by the encryption feature of spring config. See Encrypt Settings for more information.

## 4. Deploy the Api

* Deploy the resources \(mq, mysql, redis\)

```
kubectl apply -f resource
```

* Deploy and test the Api

```
bash init-api.sh
```

The api will be exposed on the web, and three things need to be checked before proceed:

1. Check the log of the api to make sure that no error occurs, and no order related logs after it started up. There should be no log after the CryptoApiApplication started:![](/assets/nolog-api.png)
2. you can expose the api service by ingress, loadbalancer, or nodePort.
3. Check the swagger documentation from the explorer: [http://xxxx:8088/swagger-ui.html](https://xxxx/swagger-ui.html)

## 5. Deploy the sending machine

* Configure the main currencies

The main currencies that are enabled in the hd-hot-wallet-\*.yml should be configured in the ex database. There are two ways to configure them:

1. Put the keys in xpubkeys.json to CryptoApiSchemaBuilder.java and generate a corresponding init-ex.sql, then run the sql manually.

2. Call the APIs to set them.

3. Bring up the sending machine

```
 bash init-sending.sh
```

* Check if the sending machine works correctly.

If everything goes well, the sending machine will start to query the blockchain to fetch blocks, and logs will appear like:

![](/assets/logs_sending.png)

## 6. Deploy the signing machine

* Deploy the signing machine

```
bash init-signing.sh
```

Then check the logs to make sure no error occurs.

* Init the signing machine

Go into the wallet-signing pod, you can first check the info by

```
curl localhost:8100
```

To init the wallet, run

```
curl localhost:8100/init -d 'password=xxxx&ga=xxxx'
```

## 7. Deploy the matching engine

If the Api starts up correctly, then the other parts should function as well. Bring up the other modules by running the scripts:

```
 bash init-match.sh
```

It should be pointed out that in production environments, the matching snapshots should be stored reliably, in which case the last line of the above script is supposed to be changed to use a local storage on the worker nodes or external storage, one can refer to Step-by-step Configuration for more information.

After all the services startup, check the logs of the each module, there should be no error and no order related logs as well. There should be no data in the database except for the init data and the locks table.

## 8. Expose the websocket

websocket is the only service that needs to be exposed to the public in prod env.

```
bash init-ws.sh
```

Then you can test it through online test tools:

```
ws://WS_URL/v1/market/?transport=websocket
```



