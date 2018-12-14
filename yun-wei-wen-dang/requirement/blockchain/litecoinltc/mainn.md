**Bitcoincashd启动**

shell script

```
#!/bin/bash

blockchain=litecoin
rpcuser=bitcoin
rpcpassword=bitcoin
HOMEDIR=~/blockchain/$blockchain
DATADIR=$HOMEDIR/data
dbcache=1000
maxmempool=500
maxconnections=50
rpcbind=127.0.0.1
rpcallowip=127.0.0.1
rpcport=10007
port=10006
log=$HOMEDIR/log/mainnet.log

nohup litecoind -daemon=0 -disablewallet -rpcuser=$rpcuser -rpcpassword=$rpcpassword \
                -datadir=$DATADIR  -dbcache=$dbcache -maxmempool=$maxmempool -maxconnections=$maxconnections \
                -server -rest -rpcbind=$rpcbind -rpcallowip=$rpcallowip -rpcport=$rpcport \
                -printtoconsole > $log &
```



