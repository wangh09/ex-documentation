# 项目介绍


# 后端应用开发说明

## 基本组建

本项目所搭建后端应用采用Jhipster开发，并基于 Spring Cloud 实现应用的微服务化。微服务环境包括以下四类组建：

* ink-registry: 基于jhipster-registry的服务发现与参数配置中心，并可完成部分服务监控功能。

* ink-uaa: 基于spring security 与 oauth2 实现的用户注册中心，集中式管理用户的注册登陆、鉴权等需求。

* ink-service-*: 底层微服务，单独模块实现单一功能。例如 ink-service-ex-api 将实现与底层撮合模块交互的功能。

* ink-gateway-*: 对外提供服务的服务网关，是各个应用访问环境的入口。

## 开发规范

项目使用参数配置中心，配置将从gitlab上进行拉取，具体的地址为： http://47.92.137.252/ink/inkapps-config.git.

项目目前阶段一共使用三个profile：test, dev, prod。

* 其中test profile是专门为微服务设计，用于本地测试发使用的，该profile将关掉服务注册模块，开发人员应当在相应的分支上关掉鉴权单元后，可以直接访问测试此服务。

* dev profile是开发环境(搭建于aliyun)的配置。

* prod是正式上线环境的配置，目前不使用。

# 底层介绍与开发说明

TBD

#充币与提币说明
==========================================

## 充币相关

* 交易所钱包的充币是指用户操作自己钱包将币从钱包转到交易所上，因此需要交易所提供每个用户的充币地址。
  用户的充币地址可以使用如下接口获取：

```
  GET /ui/users/{userId}/deposit/{currency}/address
```

* 交易所的充币策略可以进行配置，可以设置充币金额对应的所需的网络确认数，以如下接口：

```
 POST /manage/deposits/{currency}/rules
```

调用示例：

```
{
  "rules": [
    {
      "amount": 0,
      "confirms": 0
    }
  ]
}
```

如果如下配置充值策略，则 当充值金额 > 20 eth时，需要12个网络确认； > 10时需要6个网络确认， 其余情况需要3个即可。

```
amount  confirms
!---------------
 20      12
 10       6
  0       3
```

该设置是为了在大额充值时需要更多确认数来保证安全。一般的交易所仅设置一个即可，如:

```
amount  confirms
!--------------
  0       12
```

则任意充值需要12个确认后上账。

当用户操作钱包进行充值后，可以通过

```
GET /ui/users/{userId}/deposit/logs
```
查询充值进度(confirms/minimumConfirms)，其中minimumConfirms就是由如上的充值策略设定的。当confirms >= minimumConfirms时，将自动为用户上账，用户可调用

```
GET /ui/users/{userId}/accounts
```
查询到自己的余额。

在deposit/logs接口中存有 uniqueId, 可以用来获取区块链上的充值信息，一个典型的以太坊充值log的uniqueId为：

```
blockId#txId
```

示例：

```
0x1ddd88c4c881990721cf2427d3112b92235061d886bb8a4b0f1cfa1c27354a4d#0xdd3709a881ac55d9a2e0f26ea156a5b7104dfca6419c479ba291a623b97203d8
```


## 提币相关


* 提现策略的设定主要使用以下接口：

```
POST /manage/{currency}/withdraw/rules
```

主要包括以下参数：

feeRate: 费率， maximumFee: 最大手续费， minimumFee: 最小手续费，minimumAmount: 最小提现额度， withdrawDisabled: 是否关闭提现。

提现时，首先会判断最小提现额度，如果用户提现的额度太小，直接驳回。

然后会根据费率计算提现费率， 即 fee= feeRate * amount。 如果fee小于最小手续费，则fee=minimumFee; 如果fee大于最大手续费，则fee=maximumFee。

用户调用
```
POST /ui/users/{userId}/withdraw/requests
```

接口进行提现，如果没有问题，将会进入审批流程。审批流程如下：

首先提交成功后，业务系统可以根据提现信息进行检查，比如如果提现的数额大于一定数量的时候，需要人工审核，并调用如下接口：

```
POST /manage/withdraws/{withdrawRequestId}/check
{
  "errorCode": "string",
  "errorMessage": "string",
  "needReview": true,
  "success": true
}
```


其中success置成true 则表示检查通过，置成false则表示驳回（例如用户24小时内提现了10000个以太坊，直接success=false驳回，并设置相应的errorCode和Message作为提示）。

如果success置成true，则通过needReview来设置是否需要人工审查。比如amount < 100 个以太坊，则直接设置needReview=true，系统将直接为用户提现。

如果needReview设置为false，则表示需要人工审核，并进入人工审核流程。

人工审核成功后，需要手动调用

```
POST /manage/withdraws/{withdrawRequestId}/review
{
  "approved": true,
  "errorCode": "string",
  "errorMessage": "string"
}