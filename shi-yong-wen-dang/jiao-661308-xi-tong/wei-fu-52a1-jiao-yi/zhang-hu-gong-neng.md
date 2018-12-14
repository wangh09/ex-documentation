## 账户相关功能  /account

#### 1.获取账户信息

```
GET    http://47.92.88.235:8082/mapi/account/get
```

* 参数：
  * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "get mat-user info",
      "status": 200,
      "data": {
        "id": 100003,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1527044943863,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1527044943863
      },
      "timestamp": 1529587370679
    }
    ```

#### 2.创建账户信息

```
POST    http://47.92.88.235:8082/mapi/account/create
```

* 参数：

  ```
  {
    "canTrade": true,     //能否交易
    "canWithdraw": true    //能否提现
  }
  ```

* 返回结果：

  * ```
    {
      "title": "create mat-user info",
      "status": 200,
      "data": {
        "id": 100014,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1529587686246,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1529587686246
      },
      "timestamp": 1529587686261
    }
    ```

#### 3.更新账户信息

```
POST    http://47.92.88.235:8082/mapi/account/update
```

* 参数：获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

  ```
  {
    "canTrade": true,     //能否交易
    "canWithdraw": true    //能否提现
  }
  ```

* 返回结果：

  * ```
    {
      "title": "create mat-user info",
      "status": 200,
      "data": {
        "id": 100014,
        "canSignin": true,
        "canTrade": true,
        "canWithdraw": true,
        "createdAt": 1529587686246,
        "level": 0,
        "type": "TRADER",
        "updatedAt": 1529587686246
      },
      "timestamp": 1529587686261
    }
    ```

#### 4.获取账户对应的api\_key

```
GET    http://47.92.88.235:8082/mapi/account/apiKeys
```

* 参数：获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常

* 返回结果：

  * ```
    {
      "title": "get user apiKeys",
      "status": 200,
      "data": {
        "apiKeys": [
          {
            "id": 100009,
            "createdAt": 1528366740383,
            "userId": 100003,
            "apiKey": "AAAAAYajLSRwV1mfgFUzxg2tR5rKTV1J",
            "apiSecret": "******",
            "description": "test",
            "netAddress": -1062731519,
            "netmask": -1,
            "canTrade": true,
            "canWithdraw": true,
            "enabled": true,
            "ipRestriction": "192.168.1.1"
          },
          {
            "id": 100007,
            "createdAt": 1527757079965,
            "userId": 100003,
            "apiKey": "AAAAAYaj158ABB4rCnAjgJTP4JISTbXd",
            "apiSecret": "******",
            "description": "123112",
            "netAddress": -1062731775,
            "netmask": -1,
            "canTrade": true,
            "canWithdraw": true,
            "enabled": true,
            "ipRestriction": "192.168.0.1"
          },
          {
            "id": 100008,
            "createdAt": 1527757079965,
            "userId": 100003,
            "apiKey": "AAAAAYaje3-pbYPQZu2e9D6rCCOTLxHN",
            "apiSecret": "******",
            "description": "123112",
            "netAddress": -1062731775,
            "netmask": -1,
            "canTrade": true,
            "canWithdraw": true,
            "enabled": true,
            "ipRestriction": "192.168.0.1"
          },
          {
            "id": 100006,
            "createdAt": 1527757079961,
            "userId": 100003,
            "apiKey": "AAAAAYajkohEN605kb4mUmbYrqJLjLFz",
            "apiSecret": "******",
            "description": "123112",
            "netAddress": -1062731775,
            "netmask": -1,
            "canTrade": true,
            "canWithdraw": true,
            "enabled": true,
            "ipRestriction": "192.168.0.1"
          },
          {
            "id": 100004,
            "createdAt": 1527757079960,
            "userId": 100003,
            "apiKey": "AAAAAYajiQJRpplcqHIeaBsPbEhldc8i",
            "apiSecret": "******",
            "description": "123112",
            "netAddress": -1062731775,
            "netmask": -1,
            "canTrade": true,
            "canWithdraw": true,
            "enabled": true,
            "ipRestriction": "192.168.0.1"
          }
        ]
      },
      "timestamp": 1529587850184
    }
    ```

#### 5.创建账户对应的api\_key

```
POST    http://47.92.88.235:8082/mapi/account/apikeys
```

* 参数：

  ```
  {
    "authType": "GA",
    "canTrade": true,
    "canWithdraw": true,
    "code": "string",
    "description": "string",
    "ip": "string"
  }
  ```

* 返回结果：

  * ```

    ```

#### 6.删除账户对应的api\_key

```
DELETE    http://47.92.88.235:8082/mapi/account/apiKeys/{apiKey}
```

* 参数：apiKey对应的值

* 返回结果：

  * ```
    {
      "title": "delete apiKeys",
      "status": 200,
      "data": null,
      "timestamp": 1529588378757
    }
    ```

#### 7.失效账户对应的api\_key

```
POST    http://47.92.88.235:8082/mapi/accoun/account/apiKeys/{apiKey}/disable
```

* 参数：apiKey对应的值

* 返回结果：

  * ```
    {
      "title": "disable apiKey",
      "status": 200,
      "data": false,
      "timestamp": 1529588502050
    }
    ```

#### 8.生效账户对应的api\_key

```
POST    http://47.92.88.235:8082/mapi/accoun/account/apiKeys/{apiKey}/enable
```

* 参数：apiKey对应的值

* 返回结果：

  * ```
    {
      "title": "disable apiKeys",
      "status": 200,
      "data": true,
      "timestamp": 1529588678505
    }
    ```



