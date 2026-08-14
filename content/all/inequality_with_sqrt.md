---
aliases: []
id: inequality_with_sqrt
tags:
  - inequality
  - math
---

## Examples

For $a\geq b\geq c\geq 0$, prove that $\sum \sqrt{a^2+bc}\leq \frac 32 {(a+b+c)}$

Note that the equality holds for $(1,1,0)$.

Proof 1 (local expansion): As long as we can remove one sqrt, the problem can be degenerated into a polynomial inequality. So let's do it.
$$\sqrt{a^2 + bc} \leq a\sqrt{1 + bc/a^2}\leq a(1 + .5 bc/a^2)$$
Actually, $a(1 + .5 bc/a^2)\leq a+.5c$ is enough and it's easier for calculation.

Proof 2 (local AM-GM): We can also use famous inequalities to remove the square root. For example, $\sqrt{b^2+ac} \leq \frac 12 (\frac {b^2+ac}{b+c} + b + c)$ and $\sqrt{c^2+ab} \leq \frac 12 (\frac {c^2+ab}{b+c} + b + c)$.

Proof 3 (local inequality): $\sqrt{k^2 a^2+bc} \leq k a + \frac{bc}2(\frac 1 {a+b} + \frac 1 {a+c})$

Proof 4 (special trick): Note that if $x,y,z\geq 0$ and $x^2+y^2+z^2+2xyz \leq 1$ then $\sum x \leq 3/2$. Then we let $x = \frac {\sqrt{a^2+bc}}{a+b+c}$. This lemma makes sqrt only appear in on place.

Generalization 1: https://artofproblemsolving.com/community/c6h1954963p13518356

Generalization 2: Using Wolstenholme's Inequality in Proof 4, we can prove that $(\sum a)(\sum x^2) \ge 2(\sum xy\sqrt{a^2+bc})$

Remark: Actually, if the variables are between $[-1,1]$, Wolstenholme's Inequality $\iff$ $(\cos A, \cos B, \cos C)$ $\iff$ $x^2+y^2+z^2+2xyz = 1$.

---

Minkowski inequality can also deal with sqrt. e.g. $\min_{\Pi x_i=1}\sum \sqrt{1+8x_i}$ for $x_i \ge 0$.
