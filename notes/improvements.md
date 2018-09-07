# 需要改进的地方
## data
* episode start: 随机产生

## State
* 只使用OCHL，不使用cash/value
* 用收盘价归一化
* 标准化
    * 如果标准化，则reward如何定义？
* time period可配置：分钟、半小时、１小时、４小时、天

## Reward
* agent的每一步行动都会有reward，而不是0
* 引入做空机制
* 当前timestep的总价值(cash+value)减去前一个timestep的总价值作为reward

## action
* 不能做空
    * 建仓
    * 空仓
* 可以做空
    * 多头
    * 空仓
    * 空头

## Environment
＊ 根据现金和货品持有量，对agent的动作做反应:
    * 是否允许买、卖取决于是否允许补仓、减仓，资金或者货品是否足够
    * 回合结束条件
        * 超过回合最大长度
        * 总价值低于止损线
* self.start_cash = 1, self.start_value = 0

## Network
* 对比portfolio中的网络结构和本项目网络结构的差别, 用最好的结构
