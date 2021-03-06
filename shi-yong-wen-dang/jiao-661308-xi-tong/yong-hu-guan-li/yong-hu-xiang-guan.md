#### 1.分页查询用户登录日志

```
GET    http://localhost:8080/user/logs/list/20?page={page}&size={size}&sort=[sort]
```

* **参数说明：**
  * Long **userID **
  * 分页参数参考其他接口
* **返回结果：**

```
{
  "content": [
    {
      "id": 481,
      "userId": 20,
      "ipAddress": "61.50.105.122",
      "countryName": "China",
      "cityName": "Beijing",
      "status": "success",
      "device": "PC",
      "createdBy": "inkId_7f00644b3d91400e9d5d3a3fcf4be8ec",
      "createdDate": "2018-10-24T02:41:59Z",
      "lastModifiedBy": "inkId_7f00644b3d91400e9d5d3a3fcf4be8ec",
      "lastModifiedDate": "2018-10-24T02:41:59Z"
    },
    ......[other data]
  ],
  "size": 5,
  "totalElements": 29,
  "pageable": {
    "sort": {
      "sorted": false,
      "unsorted": true
    },
    "pageSize": 5,
    "pageNumber": 0,
    "offset": 0,
    "paged": true,
    "unpaged": false
  },
  "last": false,
  "totalPages": 6,
  "sort": {
    "sorted": false,
    "unsorted": true
  },
  "first": true,
  "numberOfElements": 5,
  "number": 0
}
```

* **异常情况：无**

#### 2.根据用户ID数组查询

```
GET    http://localhost:8080/user/ids/[ids]
```

* **参数说明：**
  * **Long \[ \] ids **
* **返回结果：**

```
[
  {
    "id": 1,
    "email": "system@localhost.com",
    "mobile": "+86-10000",
    "inkId": "1000",
    "areaCode": "+86",
    "firstName": "System",
    "lastName": "System",
    "imageUrl": "",
    "activated": true,
    "langKey": "en",
    "createdBy": "system",
    "createdDate": "2018-09-08T15:49:48Z",
    "lastModifiedBy": "anonymousUser",
    "lastModifiedDate": "2018-10-19T07:40:57Z",
    "authorities": [
      "ROLE_USER"
    ]
  },
  ......[other data]
]
```

* **异常情况：无**

#### 3.获取前台用户权限列表

```
GET    http://localhost:8080/user/authority/list
```

* **返回结果：**

```
[
  {
    "name": "ROLE_ADMIN"
  },
  {
    "name": "ROLE_FREEZE"
  },
  {
    "name": "ROLE_USER"
  }
]
```

* **异常情况：无**

#### 4.修改用户权限

```
POST    http://localhost:8080/user/authority/set/{userId}
```

* **接口说明：**用户缓存会清空
* **参数说明：**
  * **Long userId**
  * **Set&lt;Authority&gt; （具体权限参考上个接口）**

```
[
  {
    "name": "ROLE_FREEZE"
  }
]
```

* **返回结果：**

```
{
  "id": 5,
  "email": "32694110@qq.com",
  "mobile": "+86-17610016050",
  "inkId": "10089",
  "areaCode": null,
  "firstName": null,
  "lastName": null,
  "imageUrl": null,
  "activated": true,
  "langKey": null,
  "createdBy": "",
  "createdDate": "2018-09-08T15:53:01Z",
  "lastModifiedBy": "10089",
  "lastModifiedDate": "2018-10-18T15:03:24Z",
  "authorities": [
    "ROLE_FREEZE"
  ]
}
```

* **异常情况：500 用户不存在**

#### 5.更新用户信息

```
PUT    http://localhost:8080/user/info
```

* **接口说明：**
  * 支持修改注册邮箱
  * 支持多账户绑定同一手机
  * 更新用户信息后，删除用户所有缓存
* **参数说明：**

```
{
  "email": "string",
  "langKey": "string",
  "areaCode" : "string",
  "imgUrl" : "string",
  "mobile": "string"
}
```

* **返回结果：**

```
{
  "id": 3,
  "email": "admin@localhost.com",
  "mobile": "+86-13888888888",
  "inkId": "1010",
  "areaCode": "+86",
  "firstName": "Administrator",
  "lastName": "Administrator",
  "imageUrl": "",
  "activated": true,
  "langKey": "en",
  "createdBy": "system",
  "createdDate": "2018-06-20T02:38:19Z",
  "lastModifiedBy": "system",
  "lastModifiedDate": null,
  "authorities": [
    "ROLE_USER",
    "ROLE_ADMIN"
  ]
}
```

#### 6.重置用户安全相关

```
PUT    http://localhost:8080/user/security/reset
```

* **接口说明：**
  * 修改用户GA秘钥、资金安全密码（用户缓存会清空）。
* **参数说明：**
  * String **userId : **必传。（如果 userId 不存在，无返回结果）
  * String **googleSecret : **如果重置，直接传 null
  * String **currencyPassword ：**如果传值，则修改密码，不传默认使用原密码
  * String **lastModifiedBy ：**当前操作的账号（如果不传，默认写入 system 作为操作人）
* **参数：**

```
{
  "userId": 11119
  "googleSecret": null,
  "currencyPassword": "123456",
  "lastModifiedBy": "m-admin"
}
```

* **返回参数：**

```
{
  "id": 1,
  "userId": 11119,
  "googleSecret": null,
  "currencyPassword": "$2a$10$3DeeM0njICVMo9wemF746O4307MZcdEwyiszqlssrJM9ZmudgWlaO",
  "createdBy": "coreId_b5de420f3c8542b78c4a822270d7746b",
  "createdDate": "2019-03-20T09:34:13Z",
  "lastModifiedBy": "m-admin",
  "lastModifiedDate": "2019-03-20T10:55:44Z"
}
```

* **异常情况：无**

#### 7.获取用户缓存的数据

```
GET    http://localhost:8080/user/redis/{email}
```

* **接口说明：**
  * 主要获取用户的短信验证码、邮件验证码、注册激活码（当邮件、短信可达率低时使用）
* **参数：**
  * **String email : 用户邮箱**
* **返回结果：**
* **返回结果说明：**
  * **短信、邮件后边的值是根据发送的类型变化的。**

```
{
  "AUTH_SMS_CODE_+8617610016050changePass": "791732",
  "AUTH_EMAIL_CODE_bonismo@hotmail.comchangePass": "72261890",
  "ACTIVATION_KEY": "123456789"
}
```

#### 8.删除用户缓存

```
DEL    http://localhost:8080/user/redis/{userId}
```

* **接口说明：**
  * 主要删除用户登录、发送邮件、短信、修改手机号后无法操作某些功能等限制
* **返回结果：无**



