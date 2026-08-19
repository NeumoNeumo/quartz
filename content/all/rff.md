---
id: rff
title: Random Fourier Features
aliases:
  - Random Fourier Features
tags:
  - ai
---

Bochner's theorem writes a normalized positive definite function into the Fourier transform of a probability measure, $f(g)=\int_{\widehat{G}} \xi(g)\,d\mu(\xi)=\mathbb{E}_{\xi\sim\mu}[\xi(g)]$. So we can sample from a distribution to construct random features.

For example, for the Gaussian RBF kernel,
$k(\boldsymbol{x},\boldsymbol{y})=\exp\left(-\frac{\lVert\boldsymbol{x}-\boldsymbol{y}\rVert^2}{2\sigma^2}\right)=\int e^{i\boldsymbol{\omega}^\top(\boldsymbol{x}-\boldsymbol{y})}p(\boldsymbol{\omega})\,d\boldsymbol{\omega}=\mathbb{E}_{\boldsymbol{\omega}\sim\mathcal{N}(\boldsymbol{0},\sigma^{-2}I_d)}\left[e^{i\boldsymbol{\omega}^\top\boldsymbol{x}}e^{-i\boldsymbol{\omega}^\top\boldsymbol{y}}\right]$.


Performer/FAVOR+[^1] uses the following random feature to remove the softmax in linear transformer

$$
\begin{aligned} 
e^{\boldsymbol{q}^\top\boldsymbol{k}}&=\mathbb{E}_{\boldsymbol{\omega}\sim\mathcal{N}(\boldsymbol{0},I_d)}\left[e^{\boldsymbol{\omega}^\top\boldsymbol{q}-\lVert\boldsymbol{q}\rVert^2/2} \times e^{\boldsymbol{\omega}^\top\boldsymbol{k}-\lVert\boldsymbol{k}\rVert^2/2}\right]\\[6pt]
&\approx\frac{1}{\sqrt{m}}\begin{pmatrix}e^{\boldsymbol{\omega}_1^\top\boldsymbol{q}-\lVert\boldsymbol{q}\rVert^2/2} \\
e^{\boldsymbol{\omega}_2^\top\boldsymbol{q}-\lVert\boldsymbol{q}\rVert^2/2}\\
\vdots\\ 
e^{\boldsymbol{\omega}_m^\top\boldsymbol{q}-\lVert\boldsymbol{q}\rVert^2/2} \end{pmatrix}
\cdot\frac{1}{\sqrt{m}}\begin{pmatrix}e^{\boldsymbol{\omega}_1^\top\boldsymbol{k}-\lVert\boldsymbol{k}\rVert^2/2} \\
e^{\boldsymbol{\omega}_2^\top\boldsymbol{k}-\lVert\boldsymbol{k}\rVert^2/2}\\
\vdots\\ 
e^{\boldsymbol{\omega}_m^\top\boldsymbol{k}-\lVert\boldsymbol{k}\rVert^2/2} \end{pmatrix}
\end{aligned}
$$

This is actually similar to RFF: $\exp\left(\lVert\boldsymbol{q}-\boldsymbol{k}\rVert^2/2\right)=\int e^{-\boldsymbol{\omega}^\top(\boldsymbol{q}-\boldsymbol{k})}p(\boldsymbol{\omega})\,d\boldsymbol{\omega}=\mathbb{E}_{\boldsymbol{\omega}\sim\mathcal{N}(\boldsymbol{0},I_d)}\left[e^{-\boldsymbol{\omega}^\top\boldsymbol{q}}e^{\boldsymbol{\omega}^\top\boldsymbol{k}}\right]$. Then $\exp\left(\lVert\boldsymbol{q}+\boldsymbol{k}\rVert^2/2\right)=\mathbb{E}_{\boldsymbol{\omega}\sim\mathcal{N}(\boldsymbol{0},I_d)}\left[e^{\boldsymbol{\omega}^\top\boldsymbol{q}}e^{\boldsymbol{\omega}^\top\boldsymbol{k}}\right]$.

RFF uses the characteristic function $\mathbb{E}[e^{i\boldsymbol{\omega}^\top\boldsymbol{x}}]=e^{-\lVert\boldsymbol{x}\rVert^2/2}$, while Performer uses the moment-generating function $\mathbb{E}[e^{\boldsymbol{\omega}^\top\boldsymbol{x}}]=e^{\lVert\boldsymbol{x}\rVert^2/2}$.


[^1]: https://arxiv.org/abs/2009.14794
