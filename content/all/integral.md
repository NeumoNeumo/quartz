---
tags:
  - math
  - algebra
  - integral
aliases: []
id: integral
---

## Methods

- [[algebraic_manipulation]] e.g. King's [here](https://math.stackexchange.com/a/5097031/1131110)
    - symmetry e.g. 组合积分法
- Variable Substitution Like $f(X)=G(U)$
    - Rationalizing substitutions
        - Universal trigonometric substitution
        - Chebyshev's theorem on binomial integration
        - [Euler_substitution](https://en.wikipedia.org/wiki/Euler_substitution)
        - $\frac{1-x}{1+x}=t$ Note that $\arctan x + \arctan t = \pi/4$. So $\frac {dx}{1+x^2} = -\frac {dt}{1+t^2}$
    - $\sqrt{\sin x} = \sin u$. See [[integral#^152420|this]].
- Modify the expression to make it integrable like [$\int_{0}^{\pi/4}\tan(x)\ln(x(\frac{\pi}{2}-x))\mathrm dx=-\frac{\ln(2)^2}{2}$](https://math.stackexchange.com/a/5071995/1131110) and [[integral#^152420|this]].
- Integration by parts(反对幂指三). You can do this as long as the integrand is a product.
  - Even if it is not a product, you can make it. e.g. Van der Corput's Lemma
- Expansion like Taylor, Fourier.
- [双元法](https://zhuanlan.zhihu.com/p/443599480)
- [Feynman's trick](https://zackyzz.github.io/feynman.html)


## Problems

$\int_0^{\pi / 2} \ln \left( 1 + \sqrt{\sin x} \right) d x$
^152420

[Solution](https://www.bilibili.com/video/BV1BvxXz8EPx)

我之前比较犹豫的一点是疑惑在变换后作者是怎么想到作代换 d(arcsin(sin^2 x)) = -2d(arcsin(cos(x)/sqrt 2)) 的，但现在看来，其实还算可以理解，因为如果直接用前者其实分部积分后会得到两个不收敛的项，所以要提前就给 (arcsin(sin^2 x)) 减去一个常数 C，让  (arcsin(sin^2 x) - C)(log(1+sinx)-log(1-sinx))在x=pi/2处收敛，也同时让 (arcsin(sin^2 x) - C) /cos(x)在pi/2处可积。事实上我们也可以用MeijerG函数表示，直接泰勒展开$ln(1+x)$即可，一般地，有

$$
\int_0^{\pi/2} [\log(1+\sin^{1/n} x)] dx = 
\frac{1}{\,2^{2n}\, \pi^{2n+1/2}}\,
\mathrm{MeijerG}\!\left[
\Big\{\{0,\tfrac{1}{2n},\tfrac{2}{2n},\dots,\tfrac{2n-1}{2n}\},\{1,1\}\Big\},
\Big\{\{0,0,\tfrac{1}{2n},\tfrac{2}{2n},\dots,\tfrac {n}{2n},\tfrac {n}{2n},\dots,\tfrac{2n-1}{2n}\},\{\}\Big\},1
\right].
$$

