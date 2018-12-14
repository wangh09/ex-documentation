**Geth启动**

```
geth --datadir /data/eth --nousb --testnet --syncmode fast --cache 2048 --rpc --rpcaddr 127.0.0.1 --rpcport 8545 --maxpeers 50
```

**Docker启动**

```
#! /bin/bash
mkdir -p ~/ethereum-network/ropsten/full

docker run -d --name ethereum-ropsten-full \
    -v ~/ethereum-network/ropsten/full/:/root \
    -p 28547:8545 \
    -p 20304:30303 \
    ethereum/client-go:latest \
    --testnet --syncmode fast \
    --rpc --rpcaddr 0.0.0.0 --rpcapi "eth,net,web3" --rpccorsdomain "\*"

```

**浏览器**  
[https://ropsten.etherscan.io](https://ropsten.etherscan.io/)

**领币地址**

[https://faucet.rinkeby.io](https://faucet.rinkeby.io/)

