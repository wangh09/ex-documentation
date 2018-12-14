## Computation Requirement

The k8s credential is needed for service management.

The app system requirement:

| module | name | cpu \(vCPUs\) | memory | storage | replica |
| :--- | :--- | :--- | :--- | :--- | :--- |
| matching | crypto-api | 0.8, 1 | 0.8G, 1.6G |  | 1-2 |
|  | crypto-sequence | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | crypto-match | 0.3, 0.5 | 1G, 8G | 10G | 1 master, 1 slave |
|  | crypto-config | 0.3, 0.5 | 0.8G, 0.8G |  | 1 |
|  | crypto-quotation | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | crypto-clearing | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | crypto-notification | 0.3, 0.5 | 0.1G, 0.5G |  | 1-2 |
|  | wallet-sending | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | wallet-signing | 0.1, 0.5 | 0.1G, 0.1G |  | 1 |
| app | backend-ex-service-ui | 0.3, 0.5 | 0.8G, 1.6G |  | 1-2 |
|  | backend-ex-service-ui | 0.3, 0.5 |  |  | 1-2 |
|  | backend-ex-service-mapi | 0.3, 0.5 | 0.8G, 1.6G |  | 1-2 |
|  | backend-ex-gateway-ui | 0.3, 0.5 | 0.8G, 1.6G |  | 1-2 |
|  | backend-ex-gateway-api                \(optional\) | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | backend-ex-gatewy-manage | 0.3, 0.5 | 0.8G, 1.6G |  | 1 |
|  | frontend-web | 0.1, 0.2 | 0.1G, 0.2G |  | 2-4 |
|  | manage-backend | 0.1, 0.2 | 0.6G, 0.8G |  | 1 |
|  | manage-frontend | 0.1, 0.2 | 0.1G, 0.1G |  | 1 |
|  | registry | 0.2, 0.4 | 1.2G, 1.6G |  | 2 |
| blockchain | btc \(optional\) | 1,2 | 2G, 2G | 360G \(200G\) | 1 |
|  | usdt \(optional\) | 1,2 | 2G, 2G | 360G \(215G\) | 2 |
|  | eth \(optional\) | 1,2 | 2G, 2G | 360G \(150G\) | 1 |
|  | ltc \(optional\) | 1,2 | 2G, 2G | 200G \(18G\) | 1 |
|  | qtum \(optional\) | 1,2 | 2G, 2G | 200G \(4.5G\) | 1 |
| total |  | ~6, 11 | ~17.8G,35G |  |  |

The monitoring system requirement:

| group | service | cpu | memory | storage | replica |
| :--- | :--- | :--- | :--- | :--- | :--- |
| log management | logstash | 0.1,0.2 | 0.8G, 1G |  | 1 |
|  | es-master | 0.1, 0.2 | 1.6G, 1.8G |  | 1-2 |
|  | es-client | 0.1, 0.2 | 1.6G, 1.8G |  | 1-2 |
|  | es-data | 0.1, 0.2 | 1.6G, 1.8G | 50G | 1-2 |
|  | kibana | 0.1, 0.2 | 0.2G, 0.4G |  | 1 |
| monitoring |  |  |  |  |  |

* On test env, 2c8g \* 4 is recommanded, and can be extended according to the real needs.

* The storages can be attached by the local storage of the nodes or by network attached storage.



