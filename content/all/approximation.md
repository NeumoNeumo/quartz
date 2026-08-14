---
id: approximation
aliases: []
tags:
  - math
  - analysis
---

What if the function has a poor property? Let's approximate it using a better function!
1. The fourier transform of a function in $L^1$ might not be integrable. But we can approximate it by a series of functions in $L^1 \cap L^2$. And finally, we get a fourier operator on $L^2$.
2. When trying to prove $\hat{\hat{f}} = f$  almost everywhere for a function $f\in L^1$, we would encounter the obstacle $\int_{\mathbb R}\int_{\mathbb R} f(x)\exp(-wix)\exp(wix')dxdw$, which is not integrable in elementary calculus. But we can approximating it with $\int_{\mathbb R}\int_{\mathbb R} f(x)\exp(-wix)\exp(wix') \exp(-ux^2)dxdw$ where $u\rightarrow 0$. This is equivalent to convolute $f$ with a Gaussian kernel.
    1. More normalization in this [post](https://zhuanlan.zhihu.com/p/605817862)
    2. [An application in AI](https://zhuanlan.zhihu.com/p/12592746504). tldr: the gradient landscape of a diffusion model is smoothed by its internal Gaussian convolution, leading to a more robust model. (The title is a bit like a click gait though.)
3. Use Fourier series to approximate the target function when proving Weyl criterion.
4. Use smoothed sums when calculate divergent sums like [this post](https://terrytao.wordpress.com/2010/04/10/the-euler-maclaurin-formula-bernoulli-numbers-the-zeta-function-and-real-variable-analytic-continuation/).

