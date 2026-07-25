---
tags:
  - math
aliases: []
id: rational_points
---

**Genus**: $(d-1)(d-2)/2$ where $d$ is the degree of a polynomial

**Mordell-Weil Theorem**: Let $E$ be an elliptic curve defined over the rational numbers $Q$. Then the group $E(Q)$ of rational points on $E$ is a finitely generated abelian group.

By the structure theorem for finitely generated abelian groups, this means:  
$$
E(\mathbb{Q}) \cong \mathbb{Z}^r \oplus E(\mathbb{Q})_{\text{tors}},
$$ 
where:
- $r$ is the **rank** of $E$ (a non-negative integer measuring the "size" of the free part),
- $E(\mathbb{Q})_{\text{tors}}$ is the *torsion subgroup* (the finite subgroup of points of finite order).

**Mazur Theorem**:  $E(\mathbb{Q})_{\text{tors}}$  is limited to one of 15 possible finite groups (e.g., cyclic groups $C_n$ for $n = 1, \dots, 10, 12$ (no 11!) or products $C_2 \times C_{2m}$ for $m = 1, \dots, 4$).

**Mordell-Faltings Theorem**: Let $C$ be a smooth algebraic curve of genus $g≥2$ defined over a number field $K$. Then, the set of $K$-rational points $C(K)$ is finite.

**Siegel's Theorem**: Let $C$ be an irreducible algebraic curve defined over a number field $K$. If $C$ has genus $g≥1$ (i.e., it is not rational or elliptic with positive rank), then the set of $S$-integral points on $C$ is finite.

> [!info]
> **S-Integral Points:** Solutions where denominators are restricted to a finite set of primes S

