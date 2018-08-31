## State
* shape: (window_size, 1, feature_number)
* feature
    * 不同于v0.1, 只有序列数据，无静态数据
    * "cash"和"value"
        * v0.1版本：序列数据经过LSTM或者CNN, 然后拼接上(cash, value)，输入到dense层
        * v0.2版本：序列数据包含cash和value特征，每个window的开始，cash和value值为真实值，
          其他时刻为0
    * 增加"month", "day", "hour"特征
    * 同v0.1, 每个timestep的feature，使用dataframe.pct_change(), 即前后两个timestep差值的百分比；
      收盘价采用标准化后的绝对值
    
## Reward
* 回合结束的条件
    * acc.step.i + 1 >= self.EPISODE_LEN
    * acc.step.value < 0 or acc.step.cash < 0
* reward
    * 同v0.1, episode结束才有奖励, 回合内的每个timestep奖励值为0
