**Qtumd启动**

```
qtumd -testnet -server -rest -rpcbind=127.0.0.1 -rpcuser=qtum -rpcpassword=qtum -rpcport=3889
```

**Docker启动**

```
#! /bin/bash
docker run -d --name qtum_testnet \
    -e "QTUM_NETWORK=testnet" \
    -e "QTUM_RPC_USER=qtum" \
    -e "QTUM_RPC_PASS=testnet" \
    -v ${PWD}:/dapp \
    -p 23889:3889 \
    hayeah/qtumportal:latest
```

**测试浏览器**

[https://testnet.qtum.info](#)

**测试领币地址**

[http://testnet-faucet.qtum.info](#)

