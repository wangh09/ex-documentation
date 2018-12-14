## 币币交易功能  /trade

#### 1.获取个人订单

```
GET    http://47.92.88.235:8082/mapi/trade/orders
```

* 参数：symbol币对（BTC_USD、ETH_\_USD），startTime开始时间，endTime结束时间，pageSize几条数据，pageNum第几页，status订单状态，type订单类型，source来源（PC，WEB）
* * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "Get someone user orders",
      "status": 200,
      "data": [
        {
          "id": 2754602,
          "createdAt": 1529595196032,
          "updatedAt": 1529595196116,
          "seqId": 2654601,
          "refOrderId": 0,
          "refSeqId": 0,
          "userId": 100003,
          "symbol": "BTC_USD",
          "type": "SELL_LIMIT",
          "price": 2.17,
          "amount": 0.128,
          "filledAmount": 0.128,
          "fee": 0.00027776,
          "triggerOn": 0,
          "features": 0,
          "status": "FULLY_FILLED"
        },
        {
          "id": 2754600,
          "createdAt": 1529595195476,
          "updatedAt": 1529595195542,
          "seqId": 2654599,
          "refOrderId": 0,
          "refSeqId": 0,
          "userId": 100003,
          "symbol": "BTC_USD",
          "type": "SELL_LIMIT",
          "price": 1.63,
          "amount": 0.1634,
          "filledAmount": 0.1634,
          "fee": 0.000266342,
          "triggerOn": 0,
          "features": 0,
          "status": "FULLY_FILLED"
        },
        {
          "id": 2754598,
          "createdAt": 1529595195428,
          "updatedAt": 1529595195491,
          "seqId": 2654597,
          "refOrderId": 0,
          "refSeqId": 0,
          "userId": 100003,
          "symbol": "BTC_USD",
          "type": "SELL_LIMIT",
          "price": 1.96,
          "amount": 1.2705,
          "filledAmount": 1.2705,
          "fee": 0.00249018,
          "triggerOn": 0,
          "features": 0,
          "status": "FULLY_FILLED"
        },
        {
          "id": 2754596,
          "createdAt": 1529595194368,
          "updatedAt": 1529595194432,
          "seqId": 2654595,
          "refOrderId": 0,
          "refSeqId": 0,
          "userId": 100003,
          "symbol": "BTC_USD",
          "type": "SELL_LIMIT",
          "price": 2.3,
          "amount": 0.9615,
          "filledAmount": 0.9615,
          "fee": 0.00221145,
          "triggerOn": 0,
          "features": 0,
          "status": "FULLY_FILLED"
        },
        {
          "id": 2754594,
          "createdAt": 1529595193817,
          "updatedAt": 1529595193877,
          "seqId": 2654593,
          "refOrderId": 0,
          "refSeqId": 0,
          "userId": 100003,
          "symbol": "BTC_USD",
          "type": "SELL_LIMIT",
          "price": 1.15,
          "amount": 1.401,
          "filledAmount": 1.401,
          "fee": 0.00161115,
          "triggerOn": 0,
          "features": 0,
          "status": "FULLY_FILLED"
        }
      ],
      "timestamp": 1529595196288,
      "pageSize": 5,
      "pageNum": 1,
      "pageTotal": 20
    }
    ```

#### 

#### 2.获取指定订单撮合细节

```
GET    http://47.92.88.235:8082/mapi/trade/order/{orderId}/matches
```

* 参数：{orderId}订单id，source来源（PC，WEB）
* * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "match detial",
      "status": 200,
      "data": {
        "matches": [
          {
            "id": 2782615,
            "createdAt": 1529595193878,
            "type": "MAKER",
            "price": 1.15,
            "amount": 1.401,
            "fee": 0.00161115
          }
        ]
      },
      "timestamp": 1529595552158
    }
    ```

#### 3.获取指定订单

```
GET    http://47.92.88.235:8082/mapi/trade/order/{orderId}
```

* 参数：{orderId}订单id，source来源（PC，WEB）
* * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "Get the details of the order",
      "status": 200,
      "data": {
        "id": 2754594,
        "createdAt": 1529595193817,
        "updatedAt": 1529595193877,
        "seqId": 2654593,
        "refOrderId": 0,
        "refSeqId": 0,
        "userId": 100003,
        "symbol": "BTC_USD",
        "type": "SELL_LIMIT",
        "price": 1.15,
        "amount": 1.401,
        "filledAmount": 1.401,
        "fee": 0.00161115,
        "triggerOn": 0,
        "features": 0,
        "status": "FULLY_FILLED"
      },
      "timestamp": 1529595717158
    }
    ```

#### 4.获取个人所有账户

```
GET    http://47.92.88.235:8082/mapi/trade/user/accounts
```

* 参数：source来源（PC，WEB）
* * 获取当前请求的jwt中的userId属性，无userId抛出401Exception，若有，通过userId获取matId，如果没有userId对应的matId返回400BadRequestAlertException异常
* 返回结果：

  * ```
    {
      "title": "match detial",
      "status": 200,
      "data": [
        {
          "currency": "BTC",
          "type": "SPOT_AVAILABLE",
          "balance": 11109871669.78764,
          "id": 100002,
          "createdAt": 1527044984368,
          "updatedAt": 1529595757039,
          "version": 0,
          "userId": 100003,
          "withdrawflag": false,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "BTC",
          "type": "SPOT_FROZEN",
          "balance": 100124.7871,
          "id": 100007,
          "createdAt": 1527045391162,
          "updatedAt": 1529595757094,
          "version": 0,
          "userId": 100003,
          "withdrawflag": false,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "ETH",
          "type": "SPOT_AVAILABLE",
          "balance": 9.8996,
          "id": 100214,
          "createdAt": 1527818655871,
          "updatedAt": 1528440568262,
          "version": 0,
          "userId": 100003,
          "withdrawflag": true,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "ETH",
          "type": "SPOT_FROZEN",
          "balance": 0,
          "id": 100215,
          "createdAt": 1527818755087,
          "updatedAt": 1527821812323,
          "version": 0,
          "userId": 100003,
          "withdrawflag": true,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "INK",
          "type": "SPOT_AVAILABLE",
          "balance": 79.28,
          "id": 100322,
          "createdAt": 1528274599129,
          "updatedAt": 1528442533401,
          "version": 0,
          "userId": 100003,
          "withdrawflag": true,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "INK",
          "type": "SPOT_FROZEN",
          "balance": 0,
          "id": 100323,
          "createdAt": 1528426597673,
          "updatedAt": 1528442533401,
          "version": 0,
          "userId": 100003,
          "withdrawflag": true,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "USD",
          "type": "SPOT_AVAILABLE",
          "balance": 11113747193.898602,
          "id": 100005,
          "createdAt": 1527045008755,
          "updatedAt": 1529595757093,
          "version": 0,
          "userId": 100003,
          "withdrawflag": false,
          "depositflag": false,
          "tradeflag": false
        },
        {
          "currency": "USD",
          "type": "SPOT_FROZEN",
          "balance": 10,
          "id": 100006,
          "createdAt": 1527045387214,
          "updatedAt": 1527938581484,
          "version": 0,
          "userId": 100003,
          "withdrawflag": false,
          "depositflag": false,
          "tradeflag": false
        }
      ],
      "timestamp": 1529595757469
    }
    ```



