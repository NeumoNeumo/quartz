---
tags:
  - math
  - inequality
aliases: []
id: prove_a_function_is_zero
---

$f\in D^2 [0, +\infty)$ satisfying $f(0) = f'(0) = 0$ and
$$
|f''(x)|^2 \leq |f(x)f'(x)|
$$

for every $x\ge 0$.

Proof 1: Consider the function $g(x) = f^2(x) + f'^2(x)$ and show that $g'(x) \le 100g(x)$, thus $\frac d {dx}(exp(-100x) (f^2(x) + f'^2(x))) \le 0$.

Remark 1: We can write proof 1 in a more concealed way: let $g(x) = exp(-2.5x) (f^2(x) + f'^2(x))$ then $g^2(x) \le 0$. This will surprise your reader.

Proof 2: Use Gronwall's inequality to connect the magnitude of derivatives and antiderivatives. Assume $f''(x)\le M$ for $x\in [0, t]$ and $f''(t) = M$. Additionally, wlog $t<1$. Then $f'(t) \le Mt$ and $f(t) \le \frac 12 Mt^2$. Therefore $t \ge \sqrt[3]2$.

Remark 2: Whenever a function want to increase, its derivative changes one step ahead. If we constrain this, it cannot move.

Remark 3: The condition $|f''(x)|^2 \leq |f(x)f'(x)|$ can be generalized to
$$
|f^{(m)}(x)|^{\sum_{i=0}^{m-1}t_i} \le C \prod_{i=0}^{m-1} |f^{(i)}(x)|^{t_i}
$$
where $t_i \ge 0$.
