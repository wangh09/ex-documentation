

| type | data | example | description |
| :--- | :--- | :--- | :--- |
| db sql | ex.sql |  | the structure of trading engine db |
|  | init-ex.sql |  | the initial data of the ex db.Depends on the initial token listing plan |
|  | hd.sql |  | the structure of the wallet db |
| config application | crypto.redis.password |  | the redis password |
|  | crypto.redis.nodes |  | redis endpoints |
|  | crypto.messaging.namesrv |  | RocketMQ endpoint |
| config api | UI\_TOKEN\_KEY | UITokenKey | for app to access trading APIs \(orders\). |
|  | UI\_TOKEN\_SECRET | UITokenSecret |  |
|  | UI\_API\_KEY | UIAPIKey | for app to access other APIs \(withdraw, deposit, balances, etc\) |
|  | UI\_API\_SECRET | UIAPISecret |  |
|  | MANAGE\_API\_KEY | ManageApiKey | for accessing manage APIs |
|  | MANAGE\_API\_SECRET | ManageApiSecret |  |
|  | WALLET\_API\_KEY | WalletApiKey | for accessing wallet APIs, will only be needed by the wallet |
|  | WALLET\_API\_SECRET | WalletApiSecret |  |
| config hd hot wallet | WALLET\_API\_KEY |  |  |
|  | BTC\_ENDPOINT | [http://1.1.1.1:18547](http://1.1.1.1:18547) | the btc endpoint. can also assign the start height setting:                                            crypto.wallet.eth.start-block-height;                                 crypto.wallet.eth.start-block-hash |
|  | ETH\_ENDPOINT |  |  |
|  | USDT\_ENDPOINT |  |  |
|  | LTC\_ENDPOINT |  |  |
|  | ETC\_ENDPOINT |  |  |
|  | QTUM\_ENDPOINT |  |  |
|  | WALLET\_RW\_DATABASE |  |  |
| config match | SLAVE\_IP | 172.16.1.40 | which one is to be the slave matching engine |



### 4.2 config the app



