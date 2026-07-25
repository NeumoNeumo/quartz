---
id: classical_mech
aliases: []
tags:
  - physics
---

## Lagrangian Mechanics

- 用广义坐标改写D'Alembert's principle即可得到。
- 也可以看作欧拉拉格朗日方程凑出Newton第二定律

经典力学中 $L = T - V$，狭义相对论下更一般的表示是$S = -\int P_\mu dx^\mu$.

## Hamiltonian Mechanics

- 作为欧拉-拉格朗日方程的降次改写。
- 可以看作凯勒流形上的哈密顿场下沿着能量等值面的运动
- $H$可以看作时间演化的生成元：$\frac{df}{dt} = \{f, H\}$，如果$\frac {\partial f}{\partial t} = 0$

## Hamilton-Jacobi Theory

作用量$S$不再是路径积分的结果，而是Hamilton's principal function，一个标量函数$S(x,t)$。

- $S$可以看作固定起始点，到$(x,t)$终点的驻作用量 相关推导见[这里](https://gemini.google.com/app/e9f53061d571e7ee)
- 也可以看作从第一类母函数$F_1(q,Q,t)$通过Legendre变换推出来的

### HJE

利用$dS = p \cdot dx - H \cdot dt$这个微分关系，可以得到HJE：$$H\left(x, \frac{\partial S}{\partial x}, t\right) + \frac{\partial S}{\partial t} = 0$$，这可以帮助我们求出$S$，而一旦知道$S$获得整个力学系统的信息了。

另一条路径是去寻找使新哈密顿量为0的正则变换，其第二类生成函数为$S$。这个式子和波动光学的演化形式类似。假设波函数 $\psi(q, t) = A e^{i S(q, t) / \hbar}$，
就可以推导出薛定谔方程。见[这里](https://gemini.google.com/app/0005902074161f64)

## Noether's theorem

拉格朗日力学中的表述是 $p\delta q-H\delta t$ is constant.
在哈密顿力学中可以用泊松括号表述.

- 可以用变分符号直接推导。
- 可以将变分当作单参数连续变换在数学上更严谨地推导。
- 可以在微分几何的框架下进行推导。
- 可以类比折射定律进行推导，具体来说考虑横向均匀的介质$\frac{\partial L_{\text{opt}}}{\partial x} = 0$中的光线，光程积分为$S_{\text{opt}} = \int L_{\text{opt}} dy$，则有光学守恒量$n \sin\theta$

## 凯勒流形：一个统一耗散系统与保守系统的框架

$$\nabla H = (dH)^\sharp_g$$
$$X_H = (dH)^\sharp_\omega$$
$$X_H = J(\nabla H)$$

