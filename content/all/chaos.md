---
id: chaos
title: chaos
aliases: []
tags: []
---

Devaney's definition of chaos for a continuous map $f: X\rightarrow X$ on a metric space $X$:
- transitive: for all non-empty open subsets $U$ and $V$ of $X$ there exists $k\in \mathbb N$ s.t. $f^k(U)\cap V \neq \varnothing$ 
- the periodic points of $f$ are dense in $X$
- $f$ has sensitive dependence on initial conditions

Interesting fact: If $f: X\rightarrow X$ is transitive and has dense periodic points then $f$ has sensitive dependence on initial conditions. [^1]

Chaos cannot happen in a linear dynamical system on a simply connected space because it does not satisfy transitivity as shown [[interesting_problems#^097194|here]].

> Is the world fundamentally linear, with nonlinearity merely emerging as a result? Just as time itself may be an emergent phenomenon.

This is an ill-posed question. By "fundamentally linear" you mean, within the framework of decoherence, quantum mechanics is entirely unitary and the evolution is linear. But that does not rule out nonlinearity or complexity. Actually, every non-linear system can be represented as a linear system(See [[linearization]]). The trick is to model every state into a new dimension instead of reusing the old dimension. It's widely used in math, e.g. group representation theory from the perspective of module theory, chain groups in homology, and cochain groups in cohomology.

The linear dynamics of quantum mechanics and nonlinear interactions in classical mechanics are phenomena at entirely different levels. In quantum mechanics, the components of a state vector in Hilbert space represent the distribution of the state, whereas in classical mechanics, observables represent properties of the state. Apart from the fact that both are called “representations”, they are fundamentally different in nature.

This explains how to model a complex system into a linear system. But what about the inverse question? How does nonlinearity emerge from a linear system? **Coarse-graining makes nonlinearity and nonlinearity makes chaos.** For example, when we use a mean-field approximation in the Schrodinger euqation of the bose einstein condensate, we get the Gross-Pitaevskii equation, $i\hbar\frac{\partial\phi}{\partial t} = \left[-\frac{\hbar^2\nabla^2}{2m} +V(\mathbf r) +g(N-1)|\phi|^2\right]\phi.$ Note the nonlinear term $|\phi|^2$. ofc, we can further derive the Madelung equations from it, which is a typical example of a complex system.


Actually, linearity is not a big deal.  

[^1]: [On Devaney's Definition of Chaos](https://www.researchgate.net/publication/235605725_On_Devaney's_Definition_of_Chaos)
