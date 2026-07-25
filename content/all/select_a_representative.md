---
id: select_a_representative
aliases:
  - select a representative
tags:
  - math
  - combinatorics
---

Let $a_1, a_2, \cdots$ be a sequence of nonnegative real numbers. Suppose that for every positive integer $n$, there exist indices $i,j$ such that $|a_{i} - a_{j}| = n^{-1/3}$. Prove that $\sum_{i=1}^\infty a_i$ diverges.

^260220

Solution 1: Define $I_i=\{m\in \mathbb N_+:\exists j\in \mathbb N_+, a_i-a_j=m^{-1/3}\}$. First prove that there exist $\lambda,N>0$ such that $|I_i|\leq \max\{N,\lambda x_i^2\}$. Then suppose $i_1,i_2,\cdots,i_t$ have been select. Consider the smallest $m^*\notin \bigcup_{j=1}^t I_{i_j}$ and select $i_{t+1}$ such that $m^*\in I_{i_{t+1}}$. Obviously, $x_{i_{t+1}}^3\leq m \leq \sum_{j=1}^t \max\{N,\lambda x_{i_j}^2\} + 1$.

Solution 2([[dyadic_decomposition]]): Consider $n=N,N+1,…,8N$.

A useful trick for order estimations: "$\sum_{i=1}^\infty a_i$ converges" => "There are $O(n)$ terms $a_i$ of order $n^{-1}$"

---

Consider a 2025 × 2025 grid of unit squares. Matilda wishes to place on the grid some rectangular tiles, possibly of different sizes, such that each side of every tile lies on a grid line and every unit square is covered by at most one tile. Determine the minimum number of tiles Matilda needs to place so that each row and each column of the grid has exactly one unit square that is not covered by any tile.

[Solution](https://web.evanchen.cc/exams/IMO-2025-notes.pdf)

2026 IMO P3: Let $n$ be a positive integer. Liu Bang and Xiang Yu have a stick of length $1$ and want to divide it between themselves. Liu marks at most $n$ points on the stick, and then Xiang marks at most $n$ points on the stick. The marked points are distinct. Then, the stick is cut at all marked points, creating a number of pieces. Afterwards, they take turns claiming any unclaimed piece of the stick, with Liu going first. Each player’s goal is to maximise the total length of their own pieces.

^271304

Hint: $\frac{2^n}{2^{n+1}-1}$. First let's prove Liu's strategy: divide the stick into $2^i \epsilon$ for $i=0,1,\cdots,n$ where $\epsilon=2^{n+1}-1$. After Xiang's divisions, the sticks are $b_1\geq b_2 \geq \cdots \geq b_k$. We need to prove that $b_1 + b_3 +\cdots \geq \frac{2^n}{2^{n+1}-1}$. It would be good if we can select part of them and piece together into Liu's sticks.

