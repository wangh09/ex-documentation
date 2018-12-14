**Geth启动**

```
geth --datadir /data/eth --nousb --rinkeby --syncmode fast --cache 2048 --rpc --rpcaddr 127.0.0.1 --rpcport 8545 --maxpeers 50
```

**Docker启动**

```
#! /bin/bash
mkdir -p ~/ethereum-network/rinkeby/full

docker run -d --name ethereum-rinkeby-full \
    -v ~/ethereum-network/rinkeby/full/:/root \
    -p 18547:8545 \
    -p 10304:30303 \
    ethereum/client-go:latest \
    --rinkeby --syncmode fast \
    --rpc --rpcaddr 0.0.0.0 --rpcapi "eth,net,web3" --rpccorsdomain "\*"

```

**浏览器**

[https://rinkeby.etherscan.io](https://rinkeby.etherscan.io/)

**领币地址**

[https://faucet.rinkeby.io](http://faucet.ropsten.be:3001/)

