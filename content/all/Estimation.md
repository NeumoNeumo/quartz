---
id: Estimation
aliases: []
tags:
  - math
  - analysis
---

# Methods

- [[algebraic_manipulation]]
- [[DCT]] (Dominated Convergence Theorem)

# Examples

## Probability method

[[randomness]]

Is $\sum_{k=1}^n \sin (k^2)$ bounded when $n \rightarrow \infty$?

No. The randomness in the series suggests the application of probablity theory. Consider a partial sum of random succinct $h$ terms. If this series is bounded, the partial sum is bounded, implying the variance of the partial sum is limited. But we will show that the variance is $\Omega(h)$. Actually, using $\text{Var}\left( \sum_{i=1}^h X_i \right) = \sum_{i=1}^h \text{Var}(X_i) + 2 \sum_{1 \leq i < j \leq h} \text{Cov}(X_i, X_j)$, the variance terms contribute $h/2$ and the covariance terms are $0$ by easy calculations. Furthermore, we can deduce $\limsup_{n\rightarrow \infty} \frac {|\sum_{k=1}^n \sin (k^2)|}{\sqrt n} \geq c > 0$.

The complete proof in [this video](https://www.bilibili.com/video/BV1KCetz4Exr) and [this post](https://mathoverflow.net/questions/201250/is-sum-k-1n-sink2-bounded-by-a-constant-m).

Remark: It defines a random process and analyzes its Wide-sense stationary (WSS) property.

---
$$
\sum_{n\ge 1} \frac {|\sin (n)|^n} n
$$

^64287d

Converge.

> [!Important]
> Def: We call a series $x_n\in [0,1)$ **poly-regular near 0** if for any interval $I$ of length $L$, $\#\{n\in I: x_n \le \rho \} \lesssim L\rho^\alpha$ where $\alpha > 0$.  
> Prop: For any poly-regular sequence, we have $\sum_{n\geq 1} \frac {\exp(-nx_n)}n$ converges.  
> Prop: $a$ is a number with a finite irrationality measure. Then $\{f(n)a\}$ is poly-regular where $f(x)\in \mathbb Z[x]$ and $f \neq 0$.  
> Note: Uniformly distributed sequence does not necessarily imply poly-regularity.

#todo
- [ ] Does this have anything to do with [low-discrepancy sequences](https://en.wikipedia.org/wiki/Low-discrepancy_sequence) and [Denjoy-Koksma inequality](https://en.wikipedia.org/wiki/Denjoy–Koksma_inequality)?
- [ ] Does poly-regular near every possible number imply finite irragularity? check [this](https://poe.com/s/ZbHmGQnKiNHMNGUcEoLr)
- [ ] irrationality of a sequence.

Remark: The proof involves [[dyadic_decomposition]] which is a kind of piecewise estimation. FYI, [this video](https://www.bilibili.com/video/BV1gnpLzeETg). Cauchy Condensation test is a form of [dyadic decomposition](https://www.tricki.org/article/Dyadic_decomposition).  
Remark: Aside from dyadic decomposition, you might also need equal-spacing partition. Dyadic decomposition has a finer granularity in a small scale and coarser granularity in a larger scale compared to the equal-spacing partition. It is suitable for $\sum_{i=1}^\infty i^t f(i)$ because it relates with $\sum f(i)$. On the other hand, equal-spacing partition is useful for $\sum_{i=1}^\infty \exp(-i) f(i)$. In the example above, you need to use equal-spacing partition for values of $\exp(-nx_n)$. In this problem, both equal-spacing and dyadic work.

## Piecewise Estimation

Useful especially when the sum has different contributions on different pieces, e.g. [U-shaped curve](https://www.bilibili.com/video/BV18snqzWEEV).

$$
\lim_{n \to \infty} \frac{\log^2(n)}{n} \sum_{k=2}^{n-2} \frac{1}{\log(k)\log(n - k)}
$$

It is 1 actually. [Complete proof](https://www.bilibili.com/video/BV18snqzWEEV)

