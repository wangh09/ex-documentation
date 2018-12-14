# Blockchain Deployment

## 1. Introduction

Blockchain node deployment.

## 2. Operation

### 2.1. Install blockchain software

...

### 2.2. Configure script startup parameters

**Mainnet**

shell script（Bitcoin、Bitcoincash、Litecoin、Omnilayer）

```bash
#!/bin/bash

blockchain=bitcoin
rpcuser=bitcoin
rpcpassword=bitcoin
HOMEDIR=~/blockchain/$blockchain
DATADIR=$HOMEDIR/data
dbcache=1000
maxmempool=500
maxconnections=50
rpcbind=127.0.0.1
rpcallowip=127.0.0.1
rpcport=10001
port=10000
log=$HOMEDIR/log/mainnet.log

mkdir -p $HOMEDIR/data
mkdir -p $HOMEDIR/log

APP=bitcoind

nohup $APP -port=$port -daemon=0 -disablewallet -rpcuser=$rpcuser -rpcpassword=$rpcpassword \
                -datadir=$DATADIR  -dbcache=$dbcache -maxmempool=$maxmempool -maxconnections=$maxconnections \
                -server -rest -rpcbind=$rpcbind -rpcallowip=$rpcallowip -rpcport=$rpcport \
                -printtoconsole > $log &
```

shell script（Qtum）

```
#! /bin/bash

HOMEDIR=~/blockchain/qtum
DATADIR=$HOMEDIR/data
log=$HOMEDIR/log/mainnet.log

nohup qtumd --datadir $DATADIR -server -rest -rpcbind=127.0.0.1 -rpcuser=qtum -rpcpassword=qtum -rpcport=3889 > $log &
```

Or Docker

```
#! /bin/bash
docker run -d --name qtum_mainnet \
    -e "QTUM\_NETWORK=mainnet" \
    -e "QTUM\_RPC\_USER=qtum" \
    -e "QTUM\_RPC\_PASS=mainnet" \
    -v ${PWD}:/dapp \
    -p 13889:3889 \
    hayeah/qtumportal:latest
```

shell script（Ethereum 、Ethereum Classic）

```
#! /bin/bash

HOMEDIR=~/blockchain/ethereum
DATADIR=$HOMEDIR/data

nohup geth --datadir $DATADIR --nousb --syncmode fast --cache 2048 --rpc --rpcaddr 127.0.0.1 --rpcport 8545 &
```

Or Docker

```
#! /bin/bash
mkdir -p ~/ethereum-network/main/full

docker run -d --name ethereum-main-full \
    -v ~/ethereum-network/main/full/:/root \
    -p 48547:8545 \
    -p 40304:30303 \
    ethereum/client-go:latest \
    --syncmode fast \
    --rpc --rpcaddr 0.0.0.0 --rpcapi "eth,net,web3" --rpccorsdomain "\*"
```

### 2.3. Configure the nginx script

$server\__name domain or _\_ ；Example：domain.com

$port Port; Example: 80

$blockchain blockchain name; Example: bitcoin

$proxy\_pass proxy pass; Example: [http://127.0.0.1:8999](http://127.0.0.1:8999)

$Authorization\_Basic BASE64 encrypt\(username & password\); Example: "Basic Yml0Y29pbjpiaXRjb2lu"

```
server {
    listen 80;
    listen [::]:80;

    server_name _;

    set $blockchain bitcoin;
    set $proxy_pass http://127.0.0.1:8999;
    set $Authorization_Basic "Basic Yml0Y29pbjpiaXRjb2lu";

    keepalive_timeout 90;
    client_max_body_size 1m;
    sendfile  on;
    root  /srv/empty;
    access_log /var/log/nginx/$blockchain/access_log;
    error_log /var/log/nginx/$blockchain/error_log;

    location / {
        proxy_pass $proxy_pass;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Authorization $Authorization_Basic;
    }
}
```

Note：need mkdir -p /var/log/nginx/$blockchain.

