---
tags:
  - math
  - algebra
  - trick
aliases: []
id: algebraic_manipulation
---

我经常带有一种本质论的观点，认为绝大多数变形没有给问题的解决带来本质上的改善，问题的难点的解决所需要的复杂度没有发生改变。事实上，在群论中我们经常可以看到这一点，例如Abel-Ruffini定理的证明总是绕不过“5阶及以上的交错群不具有非平凡正规子群”这个要道——不论是采用Abel原始证明的根式扩张的观点还是用更直截了当的Galois理论的可解群的观点亦或采用Galois拓扑的视角。可能正是这种观念让我代数变形水平一般。但只要去观察一下Erdos的文章，就会发现哪怕最简单的代数变形，也可能有化腐朽为神奇的力量（当然，Erdos是一个极端的例子，这种只用普通魔法就成为一级魔法师的神仙在历史上也是不多见的）。在物理中也一样，那些乍一眼看上去没有改变问题本质的重写，例如将牛顿第二定律写为达朗贝尔原理、拉格朗日方程、哈密顿正则方程（还有经典的麦克斯韦方程组不同写法的阵营九宫格），或许在解决一些问题时有自己特殊的作用。例如拉格朗日方程的空间坐标协变性使得它处理低自由度的复杂系统时非常高效，又例如哈密顿正则方程可能直接启发了将量子系统的演化用一个线性演化算子表示。

- King property/substitution, symmetric/form completion
    - symmetric examples: 
        - $\ln(1-\sqrt{\sin(x)})$ and $\ln(1+\sqrt{\sin(x)})$ [[integral#^152420|details]]
        - $\sum_{m=1}^N \sum_{n=1}^m \exp( m(2n-1-m) \pi i / (2N))$ to $\sum_{\substack{|m|,|n|\le N \\ 2 \nmid m+n}}\exp( mn \pi i / (2N))$
    - telescoping
- Parameterization
    - Schwinger parameterization $\frac 1 {A^t}=\frac 1{(t-1)!}\int_0^\infty x^{t-1}e^{-Ax}\text dx$ for $t>0$. Another form for $t\in(0,2)$, $|A|^{t} = \frac{\Gamma(t+1)\sin(t\pi/2)}{\pi}\int_{-\infty}^{\infty}\frac{1-\cos(Ax)}{|x|^{1+t}}dx$.
    - [Feynman parameterization](https://en.wikipedia.org/wiki/Feynman_parametrization)
    - $\frac{1}{1+x^4}=\int_0^\infty e^{-tx^2}\sin t\, dt$
    - $\frac{1}{1+u^2} = \frac{1}{2} \int_{-\infty}^{\infty} e^{-|t|} e^{itu} \, dt = \int_{0}^{\infty} e^{-t} \cos(ut) \, dt$
    - Burnstein theorem
- [[Feynman_trick]]
- equivalence between trigonometric function and exponential function
- Expansion
    - Taylor series
    - Fourier series
    - Weierstrass factorization (for holomorphic functions)
    - Mittag-Leffler's theorem (for meromorphic functions)
- Other identities. See Anki

In fact, Schwinger parameterization and Power parameterization can be generalized as $A^t = C\int_0^\infty \frac {f(Ax)} {x^{t+1}} dx$. The parameterization is valid as long as the integral converges. It requires $f(x) = o(x^t)$ when $x \rightarrow 0$ and $\infty$. Schwinger parameterization uses $f(x)=\exp(-x)$ and Power parameterization uses $f(x) = 1-\cos(x)$. If we put other things into $f(x)$, we will get something like $|A|^t = C_t\int_0^\infty \frac {\sin(Ax)^4} {x^{t+1}} dx$ for $t\in(0,4)$. (A direct application can be found in [[kernel_trick|#^222539]]

#todo
- [ ] [other parameterizations](https://poe.com/chat/3iznfk1pbcctcnsz06)
