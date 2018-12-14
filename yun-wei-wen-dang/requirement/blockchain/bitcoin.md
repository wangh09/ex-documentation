# Bitcoin\(BTC\).

`Bitcoin is an innovative payment network, a new currency.`

# Quick start.

`https://hub.docker.com/r/mahuaibo/bitcoin/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull mahuaibo/bitcoin:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

HOMEDIR=~/blockchain/bitcoin
mkdir -p $HOMEDIR
docker run -d --name bitcoin-node \
    -v $HOMEDIR:/root/.bitcoin \
    -p 18332:8332 \
    mahuaibo/bitcoin:latest
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:18332
```



