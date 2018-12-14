## 压测方法

以2000个线程模拟2000个独立用户，同时进行BTC\_USDT交易对的买卖操作。其中奇数编号的线程挂买单（数量0.1，价格1usdt）；偶数编号的线程挂卖单（数量价格与买单相同）。当订单响应稳定时，系统的TPS计算方法约等于：单笔订单撮合的事务数\*每秒订单数。其中单笔订单的事务数为：1挂单+1定序+0.5撮合+1撮合记录+0.5清算+2清算记录\(A, fee\)+4转账（A-&gt;frozenA, frozenA-&gt;frozenB, frozenB-&gt;B, A-&gt;fee\)，+0.5市价+0.5tick+0.5bar=11.5。

## 压测配置

* 数据库
  * PolarDB 4c32G，读写分离
* 撮合配置（以下均为阿里云计算优化型实例）
  * 撮合引擎：4c16GB（实际使用8GB）
  * Api：4c16GB
  * RocketMQ：4c16GB
  * 其他服务：一台4c16GB

## 压测结果

每秒订单数的压测结果如下图所示：![](/assets/import_1000.png)之后，使用nginx对API进行横向扩展，压测结果如下：

![](/assets/import_2000.png)TPS虽然有一定的提升，但是压测的最后失败数高很多，查看数据库的TPS，结果如下：

![](/assets/import_3000.png)

可见，系统的每秒订单数被数据库的TPS限制住了。故在此配置下，整个撮合系统的每秒订单数约1000单/s，整体TPS在15000/s。

其他系统均未达到资源限制，监控结果如下：

api:

![](/assets/import22.png)

mq:

![](/assets/importmq.png)

match:

![](/assets/impor332t.png)

其他：

![](/assets/importqq.png)

