**Bitcoincashd启动**

shell script

```
#!/bin/bash

blockchain=omnicore
rpcuser=bitcoin
rpcpassword=bitcoin
HOMEDIR=~/blockchain/$blockchain
DATADIR=$HOMEDIR/data
dbcache=1000
maxmempool=500
maxconnections=50
rpcbind=127.0.0.1
rpcallowip=127.0.0.1
rpcport=10005
port=10004
log=$HOMEDIR/log/mainnet.log

nohup omnicored -daemon=0 -disablewallet -rpcuser=$rpcuser -rpcpassword=$rpcpassword \
                -datadir=$DATADIR  -dbcache=$dbcache -maxmempool=$maxmempool -maxconnections=$maxconnections \
                -server -rest -rpcbind=$rpcbind -rpcallowip=$rpcallowip -rpcport=$rpcport \
                -printtoconsole > $log &
```



