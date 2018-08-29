* 数据
    * 使用1分钟数据
* 状态:
    * 有两部分组成: {"series": [ohlcv(7维)], "stationary": [cash, value]}
        * CNN/LSTM用于处理series类型的状态
        * 在CNN/LSTM网络之后输入stationary类型的状态
        * Tensorforce中没有这种类型的网络结构，故自定义了网络结构来处理(custom_net() in hypersearch.py)
        * 可以先尝试利用Tensorforce处理series状态，保证简单性，看效果如何
    * close price: 相邻timestep收盘价差价的百分比
    * 其它价格：用当前timestep的收盘价做归一
    * 其它非价格特征：保持不变
    * 规范化
    * window_size?
        * 如果使用CNN, 则使用window_size的数据表示状态
        * 如果是LSTM, 则使用当前timestep的数据表示状态
* 动作
    * 取值
        * 0: buy, 每次使用固定比例的剩余现金来买入商品
        * 1: hold
        * 2: sell, 每次卖出固定比例的剩余商品，换成现金
    * 可能的问题：每次只能交易固定比例，行情不好时不能全部卖出，行情好时也不能全部买入
    * 当现金或者持有的商品不足以交易时，执行的动作貌似有问题？
* 奖励
    * 如果回合没有结束，每个timestep获得的奖励为0,
    * 如果回合结束，奖励值为: 当前的现金值+货品值，减去回合开始时现金值+货品值
