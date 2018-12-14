# Bitcoincash\(BCH\).

`Bitcoin is an innovative payment network, a new currency.`

# Quick start.

`https://hub.docker.com/r/mahuaibo/bitcoincash/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull mahuaibo/bitcoincash:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

HOMEDIR=~/blockchain/bitcoincash
mkdir -p $HOMEDIR
docker run -d --name bitcoincash-node \
    -v $HOMEDIR:/root/.bitcoin \
    -p 18332:8332 \
    mahuaibo/bitcoincash:latest
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:18332
```



