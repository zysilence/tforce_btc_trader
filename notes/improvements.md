# 需要改进的地方
## State
* 只使用OCHL，不使用cash/value
* 先用收盘价归一化，再标准化
* time period可配置：分钟、半小时、１小时、４小时、天

## Reward
* agent的每一步行动都会有reward，而不是0
* 引入做空机制
* 当前timestep的总价值(cash+value)减去前一个timestep的总价值作为reward

## action
* long, hold, short

## Environment
＊ 根据现金和货品持有量，对agent的动作做反应:
    * 是否允许买、卖取决于是否允许补仓、减仓，资金或者货品是否足够
    * 回合结束条件
        * 超过回合最大长度
        * 总价值低于止损线

## Network
* 对比portfolio中的网络结构和本项目网络结构的差别, 用最好的结构
