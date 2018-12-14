# Ethereum\(ETH\).

`Ethereum is a decentralized platform that runs smart contracts, applications that run exactly as programmed without possibility of downtime, censorship, fraud or third party interference.`

# Quick start.

`https://hub.docker.com/r/mahuaibo/zcash/`

## 1、Install  Docker.

`https://download.docker.com`

## 2、Download Docker Image.

`docker pull ethereum/client-go:latest`

## 3、Launch  Docker Container.

start.sh

```
#! /bin/bash

mkdir -p ~/ethereum-network/main/full
docker run -d --name ethereum-main-full \
    -v ~/ethereum-network/main/full/:/root \
    -p 18547:8545 \
    -p 10304:30303 \
    ethereum/client-go:latest \
    --syncmode fast \
    --rpc --rpcaddr 0.0.0.0 --rpcapi "eth,net,web3" --rpccorsdomain "*" 
```

test.sh

```
#! /bin/bash

curl -X POST -H 'Content-type:application/json' --data '{"jsonrpc":"2.0","method":"help","params":[],"id":232}'http://127.0.0.1:18547
```



