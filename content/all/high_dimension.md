---
id: high_dimension
aliases: []
tags:
  - theory
---

## Counterintuitive

A random matrix is "almost" an orthogonal matrix. However, its spectrum follows the circular Law.

Lévy's Lemma: 如果你在 $n$ 维球面上任选一个函数 $f(x)$，只要这个函数变化得不是太快（即它是 Lipschitz 连续的），那么这个函数在球面上几乎处处都等于它的中位数（或平均值）。对于 $n$ 维单位球面上的 $L$-Lipschitz 函数 $f$，有：$$P(|f(x) - E[f]| > \epsilon) \le 2 \exp\left( - \frac{(n-1) \epsilon^2}{2L^2} \right)$$

Johnson-Lindenstrauss Lemma：假设你有 $N$ 个点存储在 $d$ 维空间中（$d$ 可能非常大，比如 100 万维）。对于任何给定的误差容忍度 $0 < \epsilon < 1$，存在一个映射 $f: \mathbb{R}^d \to \mathbb{R}^k$，使得对于所有的点对 $u, v$，都有：$$(1-\epsilon) \|u-v\|^2 \le \|f(u)-f(v)\|^2 \le (1+\epsilon) \|u-v\|^2$$最神奇的地方在于所需的维度 $k$：$$k \approx \frac{8 \ln N}{\epsilon^2}$$

