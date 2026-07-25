---
tags:
  - math
aliases: []
id: Linear_Algebra
---

## Basics
- $\text{vec}(AXB) = (B^\top \otimes A)\text{vec}(X)$

## Tips
- When you are trying to prove a statement about integers, try to use rank(e.g. Sylvester's rank inequality), dimension of space, and the number of generalized eigenvectors/eigenvalues.
- commutativity is related with shared eigenspace. e.g. [this](https://zhuanlan.zhihu.com/p/719998975), Jacobson's lemma, [this](https://math.stackexchange.com/q/3379715/1131110), w-commutativity
- Consider the cyclic subspace when studying the linear dependence of $A, A^2, \cdots$. Remember how cyclic subspace decomposition is related with root subspaces, minimal polynomial and annihilating polynomials? ([this](https://www.zhihu.com/question/38787752/answer/2735490414) and [this](https://zhuanlan.zhihu.com/p/1913989372681884725))
- Trace is very useful in commuting variables. It can be applid to a scalar number directly. It also gives a rough estimation for the eigenvalue of a PD matrix. e.g. Given $x\sim N(\mu,\Sigma)$ then $\mathbb E[x^T H x] = tr(\Sigma H) + \mu^T H \mu$.
- $(E[a])^2 = E[aa']$ and $||E[A]||_F^2 = tr[E[A]E[A]^T] = tr[E[A]E[A']^T] = tr[E[AA'^T]] = E[tr[AA'^T]]$. This is used in the derivation of HSIC.
- PCA的方差最大化问题是 Ky Fan 最大原理的一个应用，而这些定理是 Courant–Fischer min-max principle 的高维形式。Ky Fan norm正是从这里出现的，正如vector norm诱导出的matrix norm
- Express the matrix in another form. e.g.
    - $\operatorname{rank}(A) = p \iff \exists B \in \mathbb{R}^{n \times p},\; C \in \mathbb{R}^{p \times n},\; \operatorname{rank}(B) = \operatorname{rank}(C) = p,\; A = BC.$
    - If $A \succeq 0$ then $A=B^2$
    - SVD: espacially useful in ML. It decomposes the optimization/dynamics of each dimension.
        - e.g. [Exact solutions to the nonlinear dynamics of learning in deep linear neural networks](https://arxiv.org/abs/1312.6120) uses SVD to derive the training dynamics on each direction of singular vectors. 
        - e.g. [This post](https://kexue.fm/archives/10592) uses SVD to show that Muon is the optimizer under 2-matrix-norm. This post also shows the power of SVG in calculating Frobenius inner product.

## Properties
- If $AB=kBA$ where $k\neq 0$, then $A$ and $B$ are simultaneously triangularizable. If we additionally have both $A$ and $B$ are diagonalizable and $k=1$, then they are simultaneously diagonalizable.
- $A$ and $B$ are simultaneously congruent diagonalization iif there exists a PD symmetric matrix $H$ such that $AHB=BHA$.
- In algebraically closed fields, any invariant subspace can be decomposed into a direct sum of generalized eigenspaces of the operator restricted to that subspace.
- On eigenvalues: 
    - Rigidity: 
        - Courant-Fischer min-max principle: Eigenvalues are stationary values of the energy function on a unit sphere. No matter linear constraints (Cauchy's interlace theorem) or small perturbation(Weyl's inequality), the energy function will not be changed dramatically, thus keeping the eigenvalues stable.
        - Cauchy's interlace theorem: rigidity of the spectrum under spatial constraint. Imagine you constrain a string of beads at a specific point, which is mathematically equivalent to taking a principal submatrix
        - Weyl's inequality: rigidity of the spectrum under perturbation
- $\min_{W_k \dots W_1 = W} \frac{1}{k} \sum_{i=1}^k \|W_i\|_F^2 = \|W\|_{S_{2/k}}^{2/k}$. This is used in proving the low rank of DNN under weight decay [[neural_networks#^851862|here]].

Some useful tricks are in [[dynamical_system]].

