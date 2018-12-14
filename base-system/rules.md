# Rules
# 编码规范

### Enum
### 常量

Length of enum constants MUST NOT be more than 20 chars, otherwise database column VARCHAR(20) will overflow.
所有数据库存储的enum常量均为字符串，长度不超过20字符，否则数据库字段VARCHAR(20)将溢出。

### Database
### 数据库

The target database is MySQL >= 5.6 with master-slave. Queries, analysis is performed on slave db.
数据库支持主从复制的MySQL >= 5.6。查询和分析尽可能使用从数据库。

Exchange application is down if master db is crash. Queries are failed if slave db is crash.
如果主数据库宕机，交易所将停止。如果从数据库宕机，某些API查询将失败。

### Match Service
### 撮合服务

Match service is single-threaded for each symbol.
对每个交易对，撮合服务是单线程运行。

Match service is master-master mode for each symbol, but one master is primary, another is backup. The backup match service produces match results in 1 second delay.
两个撮合服务以master-master模式同时运行，其中一个是主撮合，一个是备份。备份撮合将延迟1秒发送撮合结果（注：延迟是减少清算的数据库锁冲突，尚未实现）

### API

All APIs accept JSON only. The content type MUST be set to `application/json`.
所有API仅接受JSON。请求类型必须为`application/json`。

A successful API response has a status of 200 with JSON body.
一个成功的API响应是200，及返回的JSON。

An error API response has a status of 400 with JSON body.
一个错误的API响应是400，及返回的JSON。

The body (if has) of the request MUST be less than **20kb**, otherwise will return error `REQUEST_BODY_TOO_LARGE`.
请求的body不得超过20kb，否则返回`REQUEST_BODY_TOO_LARGE`错误。

### Decimals
### 数值

All decimals are defined as SQL `DECIMAL(32, 16)` which means a decimal value holds 16 integer digits and 16 fractional digits.
所有无精度误差的数值在SQL中均被定义为`DECIMAL(32, 16)`，包含16位整数和16位小数。

Range: `+/- 9999999999999999.9999999999999999`
范围：`+/- 9999999999999999.9999999999999999`

Currency scale MUST be 0 to 10.
币种的精度（scale）必须为0~10。

The total scale of the two currencies in a symbol MUST be 0~12.
交易对的两个币种精度不超过12。

Fee scale MUST be 0~4 (the minimum fee is 0.0001).
手续费精度不超过4（即最小手续费为0.0001）。

### Rules
### 编码规则

MUST-rules:


ONLY-rules:

* @RoutingWith is ONLY allowed in controller's methods.
* @RoutingWith只能用于Controller级别的方法。

NOT-rules:

* @Transactional is NOT allowed in controller-level.
* @Transactional不允许在Controller级别使用（事务范围过大）

* Nested @RoutingWith is NOT allowed.
* @RoutingWith不能嵌套。
