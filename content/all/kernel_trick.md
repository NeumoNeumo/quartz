---
tags:
  - math
  - inequality
  - kernel
  - psd
aliases: []
id: kernel_trick
---

## Common kernels

- Linear kernel: $\langle\mathbf x, \mathbf y\rangle + c$ where $c\geq 0$.
- Polynomial Kernel: $\text{poly}(xy)$
- RBF kernel/Gaussian Kernel: $\exp (-\gamma ||x-y||^2)$
- Chi-square kernel: $\frac{xy}{x+y}$, for $x,y\geq 0$
- $\frac 1 {(x+y)^t}$ for $t>0$
- $\min(x,y)$ and $1/\max(x,y)$ for $x,y\geq0$
- $\cos(x-y)$
- Kac-Murdock-Szego kernel (KMS kernel) $\rho^{|x-y|}$ where $|\rho| < 1$
## Properties
0. Moore-Aronszajn: If $f$ is a kernel, there must be a feature map s.t. $f(x,y) = \langle\phi(x), \phi(y)\rangle_H$
1. if $f,g$ are Mercer kernels, then $f+g$, $fg$(Schur-Hadamard product theorem), $c\cdot f$, $c$ ($c\geq 0$), $f^n$ ($n\in\mathbb N^+$) are kernels.
2. If $f(xy)$ and $g(x,y)$ are kernels, then $f(g(x,y))$ is a kernel.
3. [Bochner's theorem](https://en.wikipedia.org/wiki/Bochner's_theorem): $h(x-y)$ is a kernel iif the fourier transform of $h(x)$ is a non-negative measure.
4. [Mercer's theorem](https://en.wikipedia.org/wiki/Mercer's_theorem)
6. If $k(x-y)$ is a kernel, then $K(x,y)=k(x-y)-k(x+y)$ is a kernal. The inverse is not true.
7. If $f$ is a Mercer kernel and $g$ has non-negative Taylor expansion coefs, then $g\circ f$ is also a Mercer kernel.
8. If $f$ is a Mercer kernel whose range is $(-1,1)$, then $g\circ f$ is a Mercer kernel iff $f$ is analytic and has non-negative Taylor expansion coefs. (Schoenberg, 1942) 

Note:
- RBF can be viewed as [a integral of two wavelets](https://zhuanlan.zhihu.com/p/135898326). Actually, this is the visualization of $\langle k(x,\cdot),k(\cdots, y)\rangle = k(x,y)$, which is a necessary and sufficient condition for a kernel funciton.

## Applications
### Cauchy–Schwarz inequality in RKHS

The kernel function appears in the form

$$\left(\sum_{i, j} \alpha_{i} \alpha_{j} k\left(x_{i}, x_{j}\right)\right) \left(\sum_{i, j} \beta_{i} \beta_{j} k\left(y_{i}, y_{j}\right)\right) \ge \left(\sum_{i, j} \alpha_{i} \beta_{j} k\left(x_{i}, y_{j}\right)\right)^{2} $$
Reproducing Kernel Hilbert Space(RKHS)

---
**Example**:

$$
\left(\sum_{1\leq i,j\leq n}\frac1{\left(a_i+a_j\right)^s}\right)\left(\sum_{1\leq i,j\leq n}\frac1{\left(b_i+b_j\right)^s}\right)\geq\left(\sum_{1\leq i,j\leq n}\frac1{\left(a_i+b_j\right)^s}\right)^2
$$
for positive $a,b$ and $s>0$.

**Remark**: [[algebraic_manipulation|Parameterization]] is very important in creating kernels.

---

Another form of Schwinger parameterization:

Given $0 < \alpha < 2$, for any real numbers $x_{1}, x_{2}, \cdots, x_{n}$, the following inequality holds:

$$ \sum_{i,j=1}^{n}\left|x_{i} - x_{j}\right|^{\alpha} \leqslant \sum_{i,j=1}^{n}\left|x_{i} + x_{j}\right|^{\alpha}. $$

Proof: Consider $\int_0^\infty \frac 1 {t^{1+\alpha}}(\sum\sin(x_it))^2dt$.

Note: $x_i$ can actually be vectors. We can use the same Mellin transformation to prove this. Or we can consider a random projection as shown in [this video](https://www.bilibili.com/video/BV15Qb3zEE6X/).

---

Given complex numbers $z_i \neq 0$, prove that $\sum_{1\le i,j\le n} \frac{z_i+z_j}{\max(|z_i|, |z_j|)}\ge n^2$

There are two proofs. The first is in [this video](https://www.bilibili.com/video/BV15Qb3zEE6X) and another is in [the comment](https://i0.hdslb.com/bfs/new_dyn/56cbe751715655ee3e88c1d5b36759c712724545.png) of the video. Both of them first use a trivial inequality to get rid of the constant term and then prove kernels. Finally, use the property of $\sum k(x_i, x_j) \ge 0$ (Lemma 2 of the video)

---

Source: 数学新星
$||x||=\min_{n\in \mathbb Z} | x-n|$. Prove that
$$
\sum_{1\le i,j\le n}2^{||x_i-x_j||}\le \sum_{1\le i,j\le n}2^{||x_i-x_j + \frac 12||}
$$

Proof: Bochner's theorem.

---

Positive definiteness of Hilbert matrix. Actually we used a Feynman's trick here. whenever you see something in the denominator, you can always consider using Feynman's integration technique. (But the magic of Feynman's trick is not limited to canceling the denominator, see [[integral|Feynman's trick]].

---

$$\sum_{i,j=1}^{n} \frac{1}{1 + (x_i - x_j)^2} \geq \sum_{i,j=1}^{n} \frac{1}{1 + (x_i + x_j)^2}$$

$$\frac{1}{1+u^2} = \frac{1}{2} \int_{-\infty}^{\infty} e^{-|t|} e^{itu} \, dt$$

---

$a_i\in (-1,1)$ prove that $\prod_{1\le i,j, \le n} \frac {1+a_ia_j}{1-a_ia_j}$

## When the Kernel Trick fails

#^104810
*A similar problem*: Let $f$ be a monotonically non-decreasing and convex function defined on $[0, +\infty)$ with $f(0) = 0$. Then for any real numbers $x_1, x_2, \cdots, x_n$, we have 

$$ \sum_{i,j=1}^{n} f(|x_i - x_j|) \leqslant \sum_{i,j=1}^{n} f(|x_i + x_j|). $$

Proof: 2021 IMO P2. Adjugement method and induction.

---

#^222539
Expanding $\int_0^\infty x^{-t-1} (\sum \sin a_i x)^4 dx\geq 0$ gives
$$
\sum_{1\leq i\leq n}(
|a_i + a_j - a_k - a_t|^{t} + |a_i - a_j + a_k - a_t|^{t} - |a_i + a_j + a_k - a_t|^{t} + |a_i - a_j - a_k + a_t|^{t} \\ - |a_i + a_j - a_k + a_t|^{t} - |a_i - a_j + a_k + a_t|^{t} - |-a_i + a_j + a_k + a_t|^{t} + |a_i + a_j + a_k + a_t|^{t}
) \geq 0
$$
when $t\in [2,4)$

---

$|x|^H+|y|^H-|x-y|^H$ is the kernel for fractal Brownian motion.

---

试证明，存在仅依赖于 $n$ 的常数 $c_n$，使得对于任意 $n$ 个互不相同且实部大于0的常数 $z_1, z_2, \cdots, z_n$ 以及正数 $\gamma$，由这些数定义的 $n \times n$ 矩阵
$$\mathrm{P}(\gamma) = \left[ \frac{1}{\gamma + \bar{z}_i + z_j} \right]_{n \times n} ,$$
有
$$c_n \mathrm{P}(\gamma) \ge -\gamma \frac{\partial \mathrm{P}(\gamma)}{\partial \gamma} .$$

$$c_n \mathrm{P} \ge \gamma \mathrm{Q} \Leftrightarrow c_n \mathrm{I}_n \ge \gamma \mathrm{P}^{-1/2} \mathrm{Q} \mathrm{P}^{-1/2} \Leftrightarrow c_n \ge \lambda_{\max} \left(\mathrm{P}^{-1/2} \mathrm{Q} \mathrm{P}^{-1/2}\right) .$$
又有
$$\begin{aligned}
\lambda_{\max} \left(\mathrm{P}^{-1/2} \mathrm{Q} \mathrm{P}^{-1/2}\right) &\le \operatorname{tr} \left(\mathrm{P}^{-1/2} \mathrm{Q} \mathrm{P}^{-1/2}\right) \\
&= -\frac{\mathrm{d} \ln \det \mathrm{P}(\gamma)}{\mathrm{d} \gamma} \\
&= \sum_{1 \le i, j \le n} \frac{1}{\gamma + \bar{z}_i + z_j} \le \frac{n^2}{\gamma}
\end{aligned}$$
因而取 $c_n = n^2$ 即可。

## Reference

- [Reproducing Kernel Hilbert Space, Mercer’s Theorem, Eigenfunctions, Nystrom Method, and Use of Kernels in Machine Learning: Tutorial and Survey](https://arxiv.org/pdf/2106.08443)
- https://www.bilibili.com/video/BV1RkZRBsEKu

