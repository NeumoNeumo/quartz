---
id: NTK
title: NTK
aliases: []
tags:
  - theory
  - ai
---

## Facts

- feature leaning regime的模型在白化数据下会先剧烈变动其NTK，得到一个数据依赖的低秩核，在此期间loss几乎保持不变，然后再进行NTK拟合。[^1]

#todo
- DNN as a kernel learner https://gemini.google.com/app/edb4a69f259ffd14

- [[rff|Random Fourier Features]](RFF)可以看作NNGP的activation为cos，变动w的distribution一个特例。

- 有限宽神经网络训练早期的 empirical NTK 会发生快速、任务相关的谱结构调整：标签/目标函数的能量更集中到 top eigenspaces 上[^4]；由于这些 eigenspaces 对应较大的特征值，训练会沿这些方向更快下降 [^6]。

- 无限宽单隐层神经网络的梯度更新相当于MF中的Wasserstein 梯度流，也就是能量泛函在Wasserstein距离W_2下的最速降线。

- 具有尺度不变性的activation的各向同性初始化的单隐层宽神经网络的loss如果关于输出是凸的，那么在GD下可以收敛到最优解。这个非线性系统可以用MF分析，主要思路是测度与输出是线性关系，因此关于测度也是凸的。如果现在不是最佳测度，则存在一个变分使得loss下降，而因为activation是尺度不变的，这个变分可以吸收进参数更新中。[^7]

## Tricks

A trick in [Exact learning dynamics of deep linear networks with prior knowledge](https://proceedings.neurips.cc/paper_files/paper/2022/hash/2b3bb2c95195130977a51b3bb251c40a-Abstract-Conference.html):

Equivalent way to find NTK of a complex network: if $\frac{d\text{vec}(\hat{Y})}{dt} = \Theta \cdot \text{vec}(Y - \hat{Y})$, then $\Theta$ is NTK, $\nabla_{\theta}\text{vec}(\hat{Y})\nabla_{\theta}\text{vec}(\hat{Y})$, where $\hat Y$ represents the prediction.

You can solve time-variant NTK using Peano-Baker series. Moreover, a symmetric matrix like NTK has a simpler transition matrix. $\phi_t = \exp (-\int_0^t K_s ds)$ [^1]

---

It is the spectral norm that determines the stability and effectiveness of training instead of the Frobenius norm[^3]. An analysis based solely on the norm leads to conclusions similar to muP.

This paper[^2] follows a similar approach on analyzing the norm during training. The unified form of NTK and muP is called abc-parametrization. Actually, there are only two gauge invariants in abc-parameterization, but abc is better for engineering since computer has a limited precision.

---

## Refs

[^1]: [Neural Networks as Kernel Learners: The Silent Alignment Effect](https://arxiv.org/abs/2111.00034)
[^2]: [The lazy (NTK) and rich (μP) regimes: A gentle tutorial](https://arxiv.org/abs/2404.19719)
[^3]: [A Spectral Condition for Feature Learning](https://arxiv.org/abs/2310.17813)
[^4]: [Neural Spectrum Alignment: Empirical Study](https://arxiv.org/abs/1910.08720)
[^5]: ???
[^6]: [A Theory of Neural Tangent Kernel Alignment and Its Influence on Training](https://arxiv.org/abs/2105.14301)
[^7]: [On the Global Convergence of Gradient Descent for Over-parameterized Models using Optimal Transport](https://arxiv.org/abs/1805.09545)
