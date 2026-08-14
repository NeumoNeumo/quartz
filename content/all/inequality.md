---
id: inequality
aliases: []
tags:
  - inequality
  - math
---

- [[algebraic_manipulation]]
- Derivative (concavity/convexity/subharmonic): [[kernel_trick#^104810]], e.g. $\max_{|z+1|\leq 1} \sqrt {|z^2+z+1|} + \log|z|$ [^1]
- Trivial inequalities:
    - $|x|+|y| \ge |x+y| \ge |\,|x|-|y|\,|$
    - $|x + y| + |x - y| \ge 2\max\{|x|, |y|\}$
    - $a^2\geq a$ where $a\in \mathbb Z$. [[inequality#^272055]]
    - Existence means $\geq 1$. [[inequality#^272055]]
- Famous inequalities:
    - Holder: [[π_is_the_min_for_pi#^holder]]
    - Wolstenholme's Inequality: [[inequality_with_sqrt]]
    - Minkowski inequality: [[inequality_with_sqrt]]
- Probability
- Piecewise decomposition
    - [[Estimation#^64287d|dyadic decomposition]]
- Construct local inequalities. e.g. https://www.bilibili.com/video/BV127iuBbE21, [[inequality_with_sqrt]]

## Problems

$a_i \in \mathbb N_+$ prove that $\int_0^{2\pi} \prod_{i=1}^n (1-\cos a_i t) dt \ge \frac {n\pi} {2^{n-2}}$

^272055

Proof: Let $P(x)=\prod_{j=1}^n(1-x^{a_j}) =\sum_{j=0}^s b_jx^j$ then
$\text{LHS}=\frac1{2^n}\int_0^{2\pi}|P(e^{it})|^2\,dt =\frac{\pi}{2^{n-1}}\sum_{j=0}^s b_j^2$. We are going to prove that $\sum_{j=0}^s|b_j|\geq 2n$. Note that $P(1)$ has multiple zeros at 1. Apparently, $\sum_{j=0}^s b_j j^t=0$ where $t=0,1,\cdots,n-1$. Consider a multiset $A$ consisting $b_j$ $j$'s where $b_j>0$ and a multiset of $B$ consisting $-b_j$ j's where $b_j<0$. Then $\sum_{j\in A}j^t=\sum_{j\in B}j^t$. By Newton's identity, $|A|=|B|\geq n$.

Equality condition is related to [Prouhet-Tarry-Escott problem](https://en.wikipedia.org/wiki/Prouhet–Tarry–Escott_problem)

---

[^1]: A general theorem is: Let $f$ be a holomorphic function on a domain $D$, $f \not\equiv 0$. Then $\log|f|$ and $|f|^p$ ($0 < p < \infty$) are both subharmonic functions on $D$.
