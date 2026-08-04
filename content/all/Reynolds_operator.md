---
id: Reynolds_operator
title: Reynolds_operator
aliases: []
tags: []
---

只要一个群 $G$ 作用在某个对象 $X$ 或向量空间 $V$ 上，就可以把任意对象通过“沿群轨道取平均”投影到 $G$-不变部分。
$$
R(v)=\frac{1}{|G|}\sum_{g\in G} g\cdot v.
$$
这个$R$就是Reynolds operator，“$R$是个投影算符”这个性质叫Maschke's theorem。

既然$R$是一个投影算符，那么根据“投影的迹为像空间维数”，可知G-不变子空间维数为$\dim V^G = \frac{1}{|G|}\sum_{g\in G}\chi(g)$.

## 应用

实际上就是群在不同空间上的作用。

在有限集合$X$上，考虑$E=\mathbb C^X$，即$X$上的复函数空间。定义$(g\cdot f)(x)=f(g^{-1}x)$，那么$\#(X/G) = \dim (\mathbb C^X)^G = \frac 1 {|G|} \sum_{g\in G} \chi(g) = \frac 1 {|G|} \sum_{g\in G} |X^g|$就得到了Burndisde引理。

在群函数空间$\text{Fun}(G)$中，定义$(g\cdot \phi)(g')=\phi(gg'g^{-1})$，那么$\phi^{\mathrm{Ad}}(g) \equiv \frac{1}{|G|}\sum_{g_\alpha}\phi\!\left(g_\alpha\, g\, g_\alpha^{-1}\right)$ 可以从任何一个有限群函数$\phi$生成一个Ad不变群函数。我们可以得到共轭类数$\dim \operatorname{Class}(G) = \frac1{|G|}\sum_{a\in G}|C_G(a)|$，其中$C_G(a)=\{x\in G:xa=ax\}$。

> [!note] 另一条路径
> 关于$\dim \operatorname{Class}(G) = \frac1{|G|}\sum_{a\in G}|C_G(a)|$还可以这样推：对于单个元素$a$的共轭类$\mathcal C$有$|\mathcal C|=\frac{|G|}{|C_G(a)|}$，于是$\sum_{a\in \mathcal C}|C_G(a)|=|G|$，每个共轭类贡献一次 $|G|$，除以 $|G|$ 后得到共轭类数。

类似的可以用于证明有限群的复表示可以酉化：$\langle v,w\rangle_G = \frac{1}{|G|}\sum_{g\in G} \langle g\cdot v, g\cdot w\rangle.$ 这是在Hermitian form空间$\text{Herm}(V)$(一个实向量空间)中做的投影。我们可以得到$\dim_{\mathbb R}\operatorname{Herm}(V)^G = \frac1{|G|}\sum_{g\in G} \chi(g^{-1})\chi(g)$。

另一个更高级的应用是对线性映射投影到intertwiner空间，$R(A)=\frac{1}{|G|}\sum_{g\in G}\sigma(g)A\rho(g)^{-1}$满足$R(A)\rho(g)=\sigma(g)R(A), \forall g\in G$，这是Schur orthogonality relations的关键。这是在$\text{Hom}(V,W)$中做的投影。你可以从中得到$\dim_{\mathbb C}\operatorname{Hom}_G(V,W) = \langle \chi_W,\chi_V\rangle_G$。其实这和上面的Hermitian form空间的投影几乎一模一样，interwiner就是跨空间的酉变换。

> [!info] Trick
> 如果你希望你的目标满足某个式子，那就把那个式子写成一个self-consistency equation，然后求和。例如你希望$R(A)\rho(g)=\sigma(g)R(A)$，那么就可以写成$R(A)=\sigma(g)R(A)\rho(g)^{-1}$，然后对右边求和。
