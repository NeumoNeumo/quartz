---
tags:
  - math
  - analysis
  - complex-analysis
---

# Classification
- Isolated Singularity
    - Removable Singularity
    - Pole
        - Simple Pole
        - Double Pole
    - Essential Singularity
- Non-isolated Singularities
    - Branch Point
    - Cluster Point
    - Natural Boundary

Equivalent Conditions for an Essential Singularity
- **Definition**  
  A point $z_0$ is called an *essential singularity* of a complex function $f(z)$ if $z_0$ is an isolated singularity that is neither a pole nor a removable singularity.  
- **Laurent Series Characterization**  
  In the Laurent series expansion of $f(z)$ about $z_0$,
  $$
  f(z) = \sum_{n=-\infty}^{\infty} a_n (z - z_0)^n,
  $$
  the essential singularity corresponds to the case where there exist infinitely many nonzero coefficients $a_n$ for negative powers, i.e., there are infinitely many terms with $n < 0$.  
- **Limit Behavior along Different Paths**  
  If $z_0$ is an essential singularity, then there exist at least two different paths approaching $z_0$ along which the limits of $f(z)$ are distinct (or fail to exist).  
- **Casorati–Weierstrass Theorem**  
  If $z_0$ is an essential singularity of $f(z)$, then in every neighborhood of $z_0$, the image of $f(z)$ is dense in the complex plane $\mathbb{C}$.  
- **Picard’s Great Theorem**  
  In every neighborhood of an essential singularity $z_0$, the function $f(z)$ attains every complex value infinitely often, with possibly one exceptional value in $\mathbb{C}$.
