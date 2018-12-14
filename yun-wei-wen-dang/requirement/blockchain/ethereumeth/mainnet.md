**Geth启动**

```
geth --datadir /data/eth --nousb --syncmode fast --cache 2048 --rpc --rpcaddr 127.0.0.1 --rpcport 8545 --maxpeers 50
```

**Docker启动**

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



