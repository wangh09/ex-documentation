# Litecoin\(LTC\).

`Litecoin is a peer-to-peer Internet currency that enables instant, near-zero cost payments to anyone in the world. Litecoin is an open source, global payment network that is fully decentralized without any central authorities. Mathematics secures the network and empowers individuals to control their own finances. Litecoin features faster transaction confirmation times and improved storage efficiency than the leading math-based currency. With substantial industry support, trade volume and liquidity, Litecoin is a proven medium of commerce complementary to Bitcoin.`

# Quick start.

`https://hub.docker.com/r/mahuaibo/litecoin/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull mahuaibo/litecoin:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

HOMEDIR=~/blockchain/litecoin
mkdir -p $HOMEDIR
docker run -d --name litecoin-node \
    -v $HOMEDIR:/root/.litecoin \
    -p 19332:9332 \
    mahuaibo/litecoin:latest
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:19332
```



