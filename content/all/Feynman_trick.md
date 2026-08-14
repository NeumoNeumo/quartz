---
tags:
  - math
  - algebra
aliases: []
id: Feynman_trick
---

## Integration

**Note**: It helps us get rid of the denominator.

**Example**: $\int_0^1 \frac{x-1}{\ln x}dx$

> [!hint]- hint
> $I(t)=\int_0^1 \frac{x^t-1}{\ln x}dx$

**Note**: Sometimes, it does not cancel the denominator but also simplifies the formula.

**Example**: $\int_0^1 \frac{\ln(1+x)}{1+x^2}dx$

> [!hint]- hint
> Consider $\int_0^1 \frac{\ln(1+ax)}{1+x^2}dx$  
> Or, a tricky usage: consider $\frac 12 \int_0^1 \frac{\ln(2x+a(1+x^2))}{1+x^2}dx$, which is a combination of [[algebraic_manipulation|algebraic manipulation]] and Feynman's trick. This trick of $log$ is also used [here](https://math.stackexchange.com/questions/5071974/prove-the-integral-int-0-pi-4-tanx-lnx-frac-pi2-x-mathrm-dx-f/5097031#5097031). Multiplying by something in logarithms is as natural as adding something in linear algebra.

**Example**: $\int_0^1 x^3 \ln^2 x \, dx$

> [!hint]- hint
> Take the derivative of $\int_0^1 x^a dx  = \frac{1}{a+1}$ w.r.t $a$.

**Example**: [Ramanujan's master theorem](https://www.bilibili.com/video/BV1xEtRe4EhQ) also uses parameterization to provides the approximation to any function.

**Note**: Feyman's trick is equivalent to parameterization. 

**example**: $\int_0^\infty \frac{\sin x}{x}dx = \int_0^\infty \int_0^\infty \sin x e^{-xt}dtdx = \int_0^\infty \int_0^\infty \sin x e^{-xt}dxdt=\int_0^\infty \frac{1}{1+t^2}dt =\frac{\pi}{2}$

## Reference
https://zackyzz.github.io/feynman.html
