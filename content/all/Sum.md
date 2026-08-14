---
tags:
  - math
aliases: []
id: Sum
---

- Algebraic transformation
    - Telescoping/Gosper: A general method for many Hypergeometric identities like $\sum_{m=0} \frac{2(k-1)!^2 (4m+3)}{(k-2m-2)!(k+2m+1)!} = 1$.
    - King property/substitution, symmetric completion, [[Reynolds_operator]], e.g. $\sum_{k=1}^n \frac{\sin \pi k^2/(2n)}{\sin \pi k/(2n)}$ ([proof](https://zhuanlan.zhihu.com/p/714024274))
    - Schwinger parameterization $\frac 1 {A^n}=\frac 1{(n-1)!}\int_0^\infty x^{n-1}e^{-xA}\text dx$. e.g. $\sum_{m,n=1}^\infty(m^2+n^2)^{-s}=\zeta(s)\beta(s)-\zeta(2s)$ ([proof](https://www.bilibili.com/video/BV1rZV1z7Eqa))
    - Power parameterization $|t|^{a} = \frac{\Gamma(a+1)\sin(a\pi/2)}{\pi}\int_{-\infty}^{\infty}\frac{1-\cos(wt)}{|w|^{1+a}}dw$ for $a\in(0,2)$. e.g. $\sum_{1\leq i,j \leq n} (|x_i+x_j|^a - |x_i-x_j|^a)\geq 0$
- Generating function. e.g. $\sum_{n=2}^\infty \prod_{k=1}^n \frac {k}{n+k-1} = \sum_{n=2}^\infty \frac {2^n}{\binom {2n} n} =\pi/2$ ([proof](https://math.stackexchange.com/questions/420732/trying-to-prove-that-sum-j-2-infty-prod-k-1j-frac2-kjk-1-pi/420886#420886))
    - Other functions e.g. [[Basel_problem]](Eular's method)
- Discrete sum relates with integral by contour integral, e.g. [[Basel_problem]] and [this problem](https://math.stackexchange.com/questions/3139642/all-positive-solutions-of-tan-x-x) . And vice versa, the residue theorem transforms integrals into summations as well. Useful: $\cot \pi z$ is bounded on the square contour $N+1/2$ when $N\to \infty$. ^residue
- Special functions.
    - Weierstrass factorization theorem. e.g. 
    $$
    \prod_{n=1}^{\infty} \frac{(n+a_1)(n+a_2)\dots(n+a_k)}{(n+b_1)(n+b_2)\dots(n+b_k)} = \frac{\Gamma(1+b_1)\Gamma(1+b_2)\dots\Gamma(1+b_k)}{\Gamma(1+a_1)\Gamma(1+a_2)\dots\Gamma(1+a_k)}
    $$
    when $a_1 + a_2 + \dots + a_k = b_1 + b_2 + \dots + b_k$. (often used together with *Euler's Reflection Formula* $\Gamma(z)\Gamma(1-z)=\pi/\sin(\pi z)$. [examples](https://zhuanlan.zhihu.com/p/124237201?utm_source=pocket_saves) Since the sum of inverse trigonometric functions can be expressed as sum of log, this formula can also be applies like [this](https://zhuanlan.zhihu.com/p/28671855851).
    - $\pi \cot \pi x = \sum_{-\infty}^\infty \frac 1 {x-n}$. (a special case of [[#^residue]] )[examples](https://zhuanlan.zhihu.com/p/698027036)
    - Eisenstein series and modular form. [examples](https://math.stackexchange.com/q/1943244/1131110)
- Fourier Transformation(Parseval's Identity), e.g. [[Basel_problem]], $\sum\frac 1 {1+n^2}$. Poisson summation formula. e.g. $\theta(x)=\frac 1 {\sqrt{x}} \theta (\frac 1 x)$
- Approximation. e.g. Weyl's sum

ref: https://zhuanlan.zhihu.com/p/663917766

#todo
https://web.evanchen.cc/handouts/Summation/Summation.pdf
