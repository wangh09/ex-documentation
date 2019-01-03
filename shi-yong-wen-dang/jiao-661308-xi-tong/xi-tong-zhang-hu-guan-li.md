#### 1.获取系统用户

```
GET    http://localhost:8080/asset/system/users
```

* **接口说明：根据用户类型（可选）获取获取系统用户**
* **参数说明：**

  * String type : 用户类型（默认查询全部系统用户）
  * Integer page : 1
  * Integer size : 10 

* **返回结果：**

```
{
  "pageNum": 1,
  "pageSize": 10,
  "size": 10,
  "orderBy": null,
  "startRow": 1,
  "endRow": 10,
  "total": 1005,
  "pages": 101,
  "list": [
    {
      "id": 103,
      "createdAt": 1543991766276,
      "updatedAt": 1543991766276,
      "version": 0,
      "referrerId": 0,
      "organizationId": 0,
      "type": "ASSET",
      "level": 0,
      "internal": true,
      "canSignin": false,
      "canTrade": false,
      "canWithdraw": false
    }
  ],
  "firstPage": 1,
  "prePage": 0,
  "nextPage": 2,
  "lastPage": 8,
  "isFirstPage": true,
  "isLastPage": false,
  "hasPreviousPage": false,
  "hasNextPage": true,
}
```

* **异常情况：无**

#### 2.获取系统用户账户余额

```
POST    http://localhost:8080/asset/system/account/balance
```

* **接口说明：获取系统用户账户余额**
* **参数说明：**

  * **Long \[ \] ids**

* **返回结果：**

```
{
  "103": {
    "id": 103,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": false,
    "createdAt": 1543991766276,
    "level": 0,
    "type": "ASSET",
    "updatedAt": 1543991766276,
    "balance": "-10113796.2893611451682473418213321600"
  },
  "104": {
    "id": 104,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": false,
    "createdAt": 1543991766276,
    "level": 0,
    "type": "DEBT",
    "updatedAt": 1543991766276,
    "balance": "-2.69476867193199266369520000"
  }
}
```

* **异常情况：无**



#### 3.获取系统账户详情

```
POST    http://localhost:8080/asset/account/spot
```

* **接口说明：获取系统账户详情**
* **参数说明：**

  * **Long \[ \] ids**

* **返回结果：**

```
{
  "103": {
    "id": 103,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": false,
    "createdAt": 1543991766276,
    "level": 0,
    "type": "ASSET",
    "updatedAt": 1543991766276,
    "balance": "-10113796.2893611451682473418213321600"
  },
  "104": {
    "id": 104,
    "canSignin": false,
    "canTrade": false,
    "canWithdraw": false,
    "createdAt": 1543991766276,
    "level": 0,
    "type": "DEBT",
    "updatedAt": 1543991766276,
    "balance": "-2.69476867193199266369520000"
  }
}
```

* **异常情况：无**



