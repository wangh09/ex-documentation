# Zcash\(ZEC\).

`Zcash is a privacy-protecting, digital currency built on strong science.`

# Quick start.

`https://hub.docker.com/r/mahuaibo/zcash/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull mahuaibo/zcash:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

HOMEDIR=~/blockchain/zcash
mkdir -p $HOMEDIR
docker run -d --name zcash-node \
    -v $HOMEDIR:/root/.zcash \
    -p 18332:8332 \
    mahuaibo/zcash:latest
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:18332
```





