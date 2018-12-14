**Geth启动**

```
parity
```

**Docker启动**

```
#! /bin/bash
mkdir -p ~/ethereum-network/kovan/full

docker run -d --name ethereum-kovan-full \
    -v ~/ethereum-network/kovan/full:/root/.local/share/io.parity.ethereum/ \
    -p 38547:8545 \
    -p 38548:8546 \
    -p 30304:30303 \
    -p 30304:30303/udp \
    parity/parity:latest \
    --chain kovan --mode active --port 30303 \
    --base-path /root/.local/share/io.parity.ethereum/ \
    --no-dapps --no-ui \
    --jsonrpc-port 8545 \
    --jsonrpc-interface "all" \
    --jsonrpc-cors "all" \
    --jsonrpc-hosts "all" \
    --ipc-apis "all"

```

**浏览器**

[https://kovan.etherscan.io/](https://kovan.etherscan.io/)

**领币地址**

[https://gitter.im/kovan-network/faucet](https://gitter.im/kovan-network/faucet)

