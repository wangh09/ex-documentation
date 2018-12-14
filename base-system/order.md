# 订单

订单类型包括：

- 限价单
- 市价单

## 通用设置

创建订单时，必填的设置包括：

- 交易对：symbol，例如：BTC_USD

## 限价单

限价买单必须设置：

- 订单类型：orderType = "BUY_LIMIT"
- 买入价格：price，例如：1992.12
- 买入数量：amount，例如：2.15

限价卖单必须设置：

- 订单类型：orderType = "SELL_LIMIT"
- 买入价格：price，例如：1992.12
- 买入数量：amount，例如：2.15

## 市价单

市价买单必须设置：

- 订单类型：orderType = "BUY_MARKET"
- 买入总价：price，例如：12000.00

市价卖单必须设置：

- 订单类型：orderType = "SELL_MARKET"
- 卖出数量：amount，例如：2.15

## 冰山类型

针对限价买单和限价卖单，可以设置冰山委托：

- hidden = true

当设置hidden为true时，该订单在买卖盘不显示，但价格和时间优先级和其他限价单完全一样。

默认`hidden`为`false`。

使用冰山委托可以防止暴露大买单／大卖单意图。

## Fill Or Kill类型

针对限价买单和限价卖单，可以设置fillOrKill：

- 全部成交或全部取消：fillOrKill = true

设置fillOrKill后，可以确保限价买单和限价卖单以指定的价格买入／卖出全部数量。如果买卖盘没有足够的对手盘，则限价买单和限价卖单不会成交，直接全部取消。

此设置用于确保以某个价位买入足够的数量，或者卖出足够的数量，否则，将不会有任何成交。

## Post Only类型

针对限价买单和限价卖单，可以设置postOnly：

- 仅作为Maker：postOnly = true

设置postOnly后，限价单会直接进入买卖盘并以Maker出现。如果不符合条件，该订单会被直接全部取消。
