---
id: Noether_thm
aliases: []
tags: []
---

# Noether's Theorem

## General Dynamics

$$\dot{z} = M \nabla_z H$$

where $M$ is a matrix ($M=J$ in Hamiltonian mechanics, $M=-I$ in gradient descent).

If $f$ is symmetric along a vector field $V$ (w.o. variation of time), $V^T \nabla_z H = 0$. If there is a quantity $Q$ such that $\nabla_z Q = M^{-T} V$, then it is a constant.

In Hamiltonian, such $Q$ must exist?

#todo
- [ ] 感觉诺特定理的不同形式也可以画一个九宫格，就像麦克斯韦方程组一样，拉格朗日力学、哈密顿力学、HJT，经典力学、相对论、广义相对论、量子力学、微分几何、梯度下降、是否考虑时间变分中的守恒量有形式不同、内涵类似的表述。参考https://math.uchicago.edu/~may/REU2017/REUPapers/Hudgins.pdf , https://hal.science/hal-04682603v3/file/Noether_v3.pdf , https://gemini.google.com/app/f9b793e699249712 , https://gemini.google.com/app/0fc1197a7370f5fa
