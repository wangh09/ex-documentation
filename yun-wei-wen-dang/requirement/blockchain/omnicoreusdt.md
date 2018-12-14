# Omni Layer\(USDT\).

`An open-source, fully-decentralized asset platform on the Bitcoin Blockchain`

# Quick start.

`https://hub.docker.com/r/mahuaibo/omnicore/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull mahuaibo/omnicore:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

HOMEDIR=~/blockchain/omnicore
mkdir -p $HOMEDIR
docker run -d --name omnicore-node \
    -v $HOMEDIR:/root/.bitcoin \
    -p 18332:8332 \
    mahuaibo/omnicore:latest
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:18332
```



