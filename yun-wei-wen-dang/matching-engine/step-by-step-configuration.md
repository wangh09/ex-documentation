# Change the setting

This guide will tell us which parameters need to be modified, including gitlab, database, secret.yaml, kubernetes IP Intranet address mapping \(endpoint: mysql. Redis\)

### 1、mysql

If you already have mysql in your environment, you can import the SQL directly. Or you need to create a mysql instance and You need to pay special attention to delegation.

* 1.2 Import SQL into mysql

```
#login k8s-master and import sql
$ cd /root/init_data/mysql
$ mysql -uroot -h35.221.102.115 -p < ex.sql
$ mysql -uroot -h35.221.102.115 -p < hd.sql
$ mysql -uroot -h35.221.102.115 -p < init-ex.sql
```

### 2、Change the address of mysql, redis, rocketmq in k8s-ex-config

[http://35.200.101.254/](http://35.200.101.254/) ![](/assets/WX20180910-155510@2x.png)![](/assets/WX20180910-155510@2x.png)![](/assets/WX20180910-155530@2x.png)![](/assets/WX20180910-155554@2x.png)![](/assets/WX20180910-155615@2x.png)![](/assets/WX20180910-155632@2x.png)![](/assets/WX20180910-155651@2x.png)![](/assets/WX20180910-155708@2x.png)

### 3、Change the git data in secrets.yaml

These settings need to be BASE64 encrypted.

```
$ cd /root/k8s/match
$ echo "http://35.200.101.254/ink/k8s-ex-config.git"|base64
aHR0cDovLzM1LjIwMC4xMDEuMjU0L2luay9rOHMtZXgtY29uZmlnLmdpdAo=
$ echo "ink"|base64
aW5rCg==
$ echo "lR4Mu8hD1bnEppK0"|base64
bFI0TXU4aEQxYm5FcHBLMAo=
```

Update git-url and git-username and git-password in secrets.yaml

```
$ cat secrets.yaml
...
data:
  git-uri: aHR0cDovLzM1LjIwMC4xMDEuMjU0L2luay9rOHMtZXgtY29uZmlnLmdpdAo==
  git-username: aW5rCg==
  git-password: bFI0TXU4aEQxYm5FcHBLMAo==
...
```

### 4、Change the endpoints in resource-\*.yaml

**resource-ex-mysql.yaml**

```
$ cat resource-ex-mysql.yaml
apiVersion: v1
kind: Service
metadata:
  namespace: ex
  name: ex-mysql
spec:
  type: ClusterIP
  ports:
  - port: 3306
    targetPort: 3306

---
apiVersion: v1
kind: Endpoints
metadata:
  namespace: ex
  name: ex-mysql
subsets:
 - addresses:
     - ip: 35.221.102.115        # mysql addresses
   ports:
     - port: 3306
```

**resource-ex-redis.yaml**

```
$ cat resource-ex-redis.yaml
apiVersion: v1
kind: Service
metadata:
  namespace: ex
  name: ex-redis
spec:
  type: ClusterIP
  ports:
  - port: 6379
    targetPort: 6379

---
apiVersion: v1
kind: Endpoints
metadata:
  namespace: ex
  name: ex-redis
subsets:
  - addresses:
      - ip: 10.146.0.6        #redis addresses
    ports:
      - port: 6379
```

**resource-ex-rocketmq.yaml**

```
$ cat resource-ex-rocketmq.yaml
apiVersion: v1
kind: Service
metadata:
  namespace: ex
  name: ex-rocketmq
spec:
 type: ClusterIP
 ports:
 - port: 9876
   targetPort: 9876

---
apiVersion: v1
kind: Endpoints
metadata:
  namespace: ex
  name: ex-rocketmq
subsets:
 - addresses:
     - ip: 10.146.0.7        #rocketmq addresses
   ports:
     - port: 9876
```



