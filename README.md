# index

## model free

1. model free：没有明确给出**状态转移和奖励函数**，只能观察到交互采样出的轨迹
2. model free直接从经验中学习**值和策略**，无需构建马尔可夫决策模型
3. 关键步骤：估计值函数；优化策略

### （1） 蒙特卡洛方法--依赖于重复随机采样来获得数值结果的计算算法

* 必须**等待片段结束**，直到累计奖励已知
* 只能够从完整的序列中学习
* 只能应用于片段化的（有限长度的）马尔可夫决策过程
* 高方差、无偏差
* 对初始值不敏感

### （2） 时序差分学习--直接从经验片段进行学习

* 能在**每一步之后进行在线**学习
* 能够从不完整的序列中学习
* 能在连续（**无终止**）环境下工作
* 低方差、有偏差

## 动作值函数Q

### \(1\)    SARSA算法--on-policy

对于当前策略执行的每个（状态-动作-奖励-状态-动作）元组

$$
Q(s,a)\leftarrow Q(s,a)+\alpha (r+\gamma Q(s',a')-Q(s,a))
$$

### （2） Q学习--off-policy

* 无需重要性采样\(why?\) 无偏
* 根据行为策略选择动作
* 根据目标策略选择后续动作$a'\_{t+1}$
* 更新$Q\(s\_t,a\_t\)$ 的值以逼近目标状态-动作值

$$
Q(s_t,a_t)\leftarrow Q(s_t,a_t)+\alpha (r_{t+1}+\gamma \textcolor{red}{Q(s_{t+1},a'_{t+1})}-Q(s_t,a_t))\\
       \leftarrow Q(s_t,a_t)+\alpha (r_{t+1}+\gamma \textcolor{red}{max_{a'_{t+1}}Q(s_{t+1},a'_{t+1})}-Q(s_t,a_t))
$$
