---
tags:
  - math
  - inequality
  - integral
aliases: []
id: π_is_the_min_for_pi
---

Define

$$\pi_p = \frac 2 p \int_0^1 (u^{1-p} + (1-u)^{1-p})^{1/p} du$$

for $p \in [1,\infty)$. Especially, $\pi_2=\pi,\, \pi_1=\pi_\infty =4$. Prove that $\pi_p\geq \pi$.

[Complete proof](https://www.tandfonline.com/doi/abs/10.1080/07468342.2000.11974122).

$$
\begin{align*}
\pi_p &= \frac 2 p \int_0^1 \frac {(u^{p-1} + (1-u)^{p-1})^{1/p}}{u^\frac{p-1}p (1-u)^\frac{p-1}p} du &(1) \\
&\overset{(2)}\geq \frac 2 p \int_0^1 \frac {u^\frac{2(p-1)}p + (1-u)^\frac{2(p-1)}p}{u^\frac{p-1}p (1-u)^\frac{p-1}p} du \\
&= \frac 4p \int_0^1 {u^\frac{p-1}p (1-u)^{-\frac{p-1}p}} du \\
&= \frac 4p Beta(2-1/p, 1/p) \\
&= \frac 4p \Gamma(2-1/p) \Gamma(1/p) \\
&= \frac {4\pi}p (1-1/p) \frac 1 {\sin \frac \pi p}
\geq \pi
\end{align*}
$$

$(2)$ is the most important step. This is an inverse use of [[algebraic_manipulation|King property]] which successfully turns a sum of two terms into a single term. It turns the problem into an easy Beta funciton. If you don't do arithmetic transform to get (1), you will not have the opportunity to use (2), which shows the importance of arithmetic transform in inequalities.

It also remind us that when all attempts appear to fail, a basic yet non-trivial intermediate step may be required. I would call it a "bridge". Identifying such a bridge demands a systematic and profound understanding of the available techniques, enabling one to anticipate both the preconditions and consequences of the bridge.

Proof of $(2)$: Using Holder's inequality, you can always have something like $(u^a + (1-u)^a)^b \geq (u^b + (1-u)^b)^a$ as long as $a > b > 1$ or $0<a<b<1$. Here $a=p-1$ and $b=2-2/p$ #^holder

Another definition[^1] of $\pi_p$ is 
$$
\frac{\pi_{p}}{2} = \sin_{p}^{-1}(1) = \int_{0}^{1} \frac{1}{\left(1 - t^{p}\right)^{1/p}} \, dt
$$
where $p>1$ and $\sin_p$ is defined by $\cos_p(x)^p + \sin_p(x)^p = 1$ and $\frac {d \sin_p(x)} {dx} = \cos_p(x)$. In this definition, $\pi_p$ is monotonically decreasing wrt $p$.

[^1]: [Monotonicity properties and bounds for the complete p-elliptic integrals](https://pmc.ncbi.nlm.nih.gov/articles/PMC6154081/)
