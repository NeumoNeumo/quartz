---
id: optimizer
aliases: []
tags:
  - AI
---

## Facts

#todo
- 模型训练后期，分类loss把类别向量往离其它类别更远的地方推，SGD中的WD把它们往回拉，两者平衡的结果就是NC中的ETF。但如果是AdamW，外推力就会因为历史梯度而产生各向异性扭曲，从而更难NC。 [^1]

- Muon可以对抗谱塌陷 (Spectral Collapse) 和主导特征的“虹吸效应”，而这两种效应会导致权重矩阵 $W$ 迅速倾向于低秩空间，丧失了表达更丰富细节特征的能力，[^2]。这一现象在[[LLM#^022856|这里]]也有描述。

- Init $x=u=0$. Optimizing $||Ax-b||_2^2$ using GD on $x$ gives an implicit regularization of $||x||_2^2$ and optimizing$||Ax-b||_2^2$ where $x=u\odot u$  using GD on $u$ gives an implicit regularization of $||x||_1$. [^4]

## Tricks

**Unconstrained Features Model**将损失函数看作分类头前的feature与分类头矩阵的一个二元函数

$$\mathcal{L}(\mathbf{W}, \mathbf{H}) = \mathcal{L}_{CE}(\mathbf{W}\mathbf{H}) + \frac{\lambda}{2} \|\mathbf{W}\|_F^2 + \frac{\lambda}{2} \|\mathbf{H}\|_F^2$$

$\mathbf{H}$ 是输入数据 $X$ 经过前面几十层非线性变换得到的，如果直接对 $\theta$ 求导，数学上难以处理。因此UFM假设网络前面的层表达能力足够强，以至于我们可以把最后一层的输入特征 $\mathbf{H}$ 当作自由变量（Free Variables），直接对其进行优化。但UFM显然抹杀了Jacobi矩阵带来的bias。

#todo
但我们显然可以结合UFM与NTK，参见 https://gemini.google.com/share/7600e5ee08e7

如果你想考虑二阶项，直接算Hessian有点贵，可以利用加噪/随机mask，例如dropout与magma，详细推导可见[这则评论](https://kexue.fm/archives/11654/comment-page-1#comment-29312)。或者也可以像SAM(Sharpness-Aware Minimization)[^3]，先沿着梯度方向走一步，然后用终点处的梯度更新矩阵，这样也包含了Hessian的信息。不要相信这两篇文章所声称的直觉和推导，他们说得都有问题。

如果你想证明某个优化器得到的结果是最优的，可以考虑使用一个certificate。这个certificate可以来自KKT条件、Max–min inequality、次梯度条件、法锥条件等。一个有用的intuition：约束优化中，对偶变量/Lagrange乘子通常用于累积约束违反所产生的压力 [^5]

## Ref

[^1]: [Optimizer choice matters for the emergence of Neural Collapse](https://arxiv.org/abs/2602.16642)
[^2]: [What Happens During the Loss Plateau? Understanding Abrupt Learning in Transformers](https://arxiv.org/abs/2506.13688)
[^3]: [Sharpness-Aware Minimization for Efficiently Improving Generalization](https://arxiv.org/abs/2010.01412)
[^4]: [Implicit Regularization in Matrix Factorization](https://arxiv.org/abs/1705.09280)
[^5]: [Implicit Regularization in Matrix Factorization](https://arxiv.org/abs/1705.09280)
