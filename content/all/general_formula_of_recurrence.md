---
id: general_formula_of_recurrence
aliases: []
tags:
  - math
  - algebra
---

> Problem 1: $a_{n+1} + 2a_n + 4 = a_{n-1}^2$

Note that: 

If $p = k = 2/q$, then
$$
((pa^2-q) + (pb^2-q)) + 2p/k (kab) + 2q = p(a+b)^2 \\
k(pa^2-q)(pb^2-q) + kq((pa^2-q) + (pb^2-q)) + kq^2 = p^2(kab)^2
$$

Therefore, the sequence is like $a+b, kab, m(a)+m(b), km(a)m(b), m(m(a))+m(m(b)), \cdots$, where $m(x) = px^2-q$. Moreover, the composition of $m$ can also be expressed using trigonometric function in the form $m^{(n)} = c^{2^n}+c^{2^{-n}}$.

> Problem 2: $a_n = a_{n-1}^2 - 2b_{n-1}$ and $b_n = b_{n-1}^2 - 2a_{n-1}$

Note that if $abc=1$, then
$$
a^2+b^2+c^2 = (a + b + c)^2 - 2(ab+bc+ca)\\
(ab)^2 + (bc)^2 + (ca)^2 = (ab+bc+ca)^2 - 2(a+b+c)
$$

Background: 这题的本质可能是Graeffe's Root-Squaring Method. 具体地，我们希望求3次多项式f(x)的根x_1, x_2, x_3，不妨设f(x) = x^3 - bx^2 + cx -1，否则令x <- ax 其中a为适当的常数。利用此题的结论我们可方便地求出 a_n = x_1^2^n + x_2^2^n + x_3^2^n，这是最大模主导的，于是 a_n^{1/2^n} 可快速求出一个根。

> Problem 3: $a_{n+1} = \frac{a_n}{4} + \frac{3a_n + 12}{4b_n^2}$ and $b_{n+1} = \frac{b_n^2 + a_n + 7}{4b_n}$.

Let
$$a_n = 3(c_n^2 + d_n^2) - 4\\b_n = \sqrt{3} c_n d_n$$
and 
$$c_{n+1} = \frac{c_n^2 + 1}{2c_n}\\d_{n+1} = \frac{d_n^2 + 1}{2d_n}$$

Note: 一般地，对于P1,2,3，都可以这样出题：令$c_{n+1}=f(c_n)$以及$d_{n+1}=f(d_n)$，其中$f$为有理式。再令$a_n$与$b_n$为关于$c,d$的对称有理式，最后写出$a$与$b$的递推关系。一般这种式子长得并不好看，例如P3；但有时候可以用特殊值化简一下，例如P2；极少数时候可以得到非常精妙的结果，例如P1。

Ni与Ne也可以感知抽象性的东西，例如理论

> Problem 4: $(a_(n+1)-a_n)^2=a_n^2+a_n+1$

Consider a triangle with side lengths of 1, $a_n$, and $a_{n+1} - a_n$, where one of the angles is 120 degrees.

## Reference
- [通项杯1](https://zhuanlan.zhihu.com/p/407534999)
- [通项杯2](https://tieba.baidu.com/p/7559954240)
