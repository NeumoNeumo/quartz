---
id: generalization
aliases: []
tags: []
---

## Metrics

Metrics to predict generalization performance:
- Fisher information
- [SMAD](https://arxiv.org/pdf/2602.07135v3) (Saddle-Minimum Average Distance): 模型训练收敛到的那个局部极小值点为中心，提取出 Hessian 矩阵中特征值最大的前几个特征向量，构建网格表，算出格点loss，用0 维持续同调计算出计算各个盆地的“持续期”，persistence的均值即为SMAD，越小越好。相比fisher information的优点是更全局。


