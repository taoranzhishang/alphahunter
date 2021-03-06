# 数据类型

1. 盘口数据(ORDER_BOOK)
   1. 该交易所所有交易品种的盘口数据。该数据每隔1秒左右记录一个交易品种的买卖20档盘口数据
   2. tips
      1. 下载数据并且解压缩后，会得到若干文件，每个文件夹中都存放一个交易品种的盘口数据。
      2. 例如“BINANCE_LTCBTC_20180204_ORDERBOOK.csv”代表币安交易所中LTCBTC这个品种在20180204的盘口数据。
      3. 数据中的时间都是格林威治时间(UTC)，比北京时间慢8个小时。
      4. [自动下载](http://yucezhe.com/product/data#!?series=developer)
   3. 字段说明
   
        | 字段名                         |          描述          |
        | ------------------------------ | :--------------------: |
        | lastUpdateId                   |     交易所提供的id     |
        | server_time                    | 服务器接收到数据的时间 |
        | buy_1_pric...buy_20_price      |     买1价...买20价     |
        | sell_1_price...sell_20_price   |     卖1价...卖20价     |
        | buy_1_amount...buy_20_amount   |     买1量...卖20量     |
        | sell_1_amount...sell_20_amount |     卖1量...卖20量     |
2. 逐笔数据(tick)
   1. 该交易所所有交易品种的逐笔数据。该数据并不是记录每一笔成交。若两笔成交相邻，并且他们的价格、买卖方向相同，会将这两笔成交合并显示
   2. tips
      1. 下载数据并且解压缩后，会得到若干文件，每个文件夹中都存放一个交易品种的逐笔数据
      2. 例如“BINANCE_LTCBTC_20180204_TICK.csv”代表币安交易所中LTCBTC这个品种在20180204的逐笔数据
      3. 若某品种在当天没有发生任一笔交易，则在当天没有数据。
      4. 数据中的时间都是格林威治时间，比北京时间慢8个小时。
   3. 字段说明
       | 字段名         |                             描述                             |
       | -------------- | :----------------------------------------------------------: |
       | aggregate_ID   |                 该笔交易在该交易所的ID，唯一                 |
       | time           |               该笔交易发生的时间(格林威治时间)               |
       | price          |                        该笔交易的价格                        |
       | amount         |                        该笔交易的数量                        |
       | buy_or_sell    |           该笔交易的方向，'s'代表卖出，'b'代表买入           |
       | first_trade_ID |  每笔交易都有trade_ID，本字段记录本行数据中的第一笔交易的ID  |
       | last_trade_ID  | 每笔交易都有trade_ID，本字段记录本行数据中的最后一笔交易的ID |

3. 对的，咱们自己规定最大的 Universe(考察的币种的范围), 以及每个表最多的字段，
   一旦数据币种不存在，我们就跳过，一旦某种数据没法计算我们某个字段，我们就留空值
   我们最大程度上保证自己的数据库统一规则
   time向上取整到毫秒