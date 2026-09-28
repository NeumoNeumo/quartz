---
id: qm_cm
title: "Similarity between QM and CM"
aliases: []
tags:
  - quantum_mechanics
  - classical_mechanics
---

#TODO
pruning

More information https://chatgpt.com/g/g-p-6a28f2b7ec2881919aee4ffe05b53d19-fun/c/6ab92047-2038-83e8-a966-3c0e87a087a7

The following discussion uses a single particle with Hamiltonian $H=p^2/(2m)+V(q)$ as an example.

### 1. Position, momentum, and canonical relations

In classical mechanics, position and momentum are coordinates in phase space, satisfying

$$
\{q,p\}=1.
$$

In quantum mechanics, they become operators satisfying

$$
[\hat q,\hat p]=i\hbar.
$$

This is one of the most fundamental correspondences used in constructing quantum theory. However, one should note that one cannot simply replace **any** Poisson bracket in a classical expression with a commutator. When more complicated products of $q$ and $p$ are involved, operator ordering problems also arise.

Example: https://chatgpt.com/g/g-p-6a28f2b7ec2881919aee4ffe05b53d19-fun/c/6ab92047-2038-83e8-a966-3c0e87a087a7

### 2. Hamilton’s equations and the Heisenberg equation

For a classical observable $A(q,p,t)$, its rate of change along a trajectory is

$$
\frac{dA}{dt}=\{A,H\}+\frac{\partial A}{\partial t}.
$$

In quantum mechanics, the corresponding equation in the Heisenberg picture is

$$
\frac{d\hat A}{dt}
=\frac{1}{i\hbar}[\hat A,\hat H]
+\frac{\partial\hat A}{\partial t}.
$$

Taking $A=q,p$, the classical equations give

$$
\dot q=\frac{p}{m},\qquad \dot p=-V'(q).
$$

The quantum equations give the corresponding operator equations:

$$
\dot{\hat q}=\frac{\hat p}{m},\qquad
\dot{\hat p}=-V'(\hat q).
$$

Thus, the structures of the two sets of equations of motion are remarkably similar.

### 3. Newtonian motion and Ehrenfest’s theorem

Taking expectation values of the above quantum operator equations gives

$$
\frac{d\langle\hat q\rangle}{dt}
=\frac{\langle\hat p\rangle}{m},\qquad
\frac{d\langle\hat p\rangle}{dt}
=-\langle V'(\hat q)\rangle.
$$

This is **Ehrenfest’s theorem**. It looks very similar to Newton’s laws, but in general,

$$
\langle V'(\hat q)\rangle\ne V'(\langle\hat q\rangle).
$$

Therefore, the center of a quantum wave packet does **not** always follow a classical trajectory exactly. If the wave packet is sufficiently narrow and the potential varies slowly over the region occupied by the packet, we can approximately make this identification and recover classical motion. For potentials up to quadratic order, this closure relation is exact.

### 4. The Schrödinger equation and the Hamilton–Jacobi equation

Classical mechanics can also be formulated in terms of the action function $S(q,t)$, which satisfies the Hamilton–Jacobi equation:

$$
\frac{\partial S}{\partial t}
+\frac{(\nabla S)^2}{2m}+V=0.
$$

In quantum mechanics, write the wave function as

$$
\psi=\sqrt{\rho}\,e^{iS/\hbar}.
$$

Substituting this into the Schrödinger equation and separating the real and imaginary parts gives, from the real part,

$$
\frac{\partial S}{\partial t}
+\frac{(\nabla S)^2}{2m}+V
-\frac{\hbar^2}{2m}
\frac{\nabla^2\sqrt{\rho}}{\sqrt{\rho}}
=0.
$$

Compared with the classical Hamilton–Jacobi equation, there is only one additional term at the end, often called the **quantum potential term**. When this term is negligible compared with the other terms, the classical equation is recovered. This correspondence reveals why the classical approximation works in the short-wavelength limit, or when the action is much larger than $\hbar$.

### 5. Phase-space probability distributions and the Wigner function

The classical Liouville density $f(q,p)$ that you mentioned is defined on phase space. The quantum density matrix can also be represented as a function on phase space through the **Wigner transform**. In one dimension,

$$
W(q,p)=\frac{1}{2\pi\hbar}
\int dy\,e^{-ipy/\hbar}
\left\langle q+\frac y2\middle|\rho\middle|q-\frac y2\right\rangle.
$$

In this way, the classical distribution $f(q,p)$ and the quantum state $W(q,p)$ have a direct formal correspondence. The evolution equation of the Wigner function also approaches the Liouville equation in the appropriate classical limit.

However, $W$ is **not necessarily non-negative everywhere**, so it cannot always be interpreted as a “classical probability density in which particles possess definite position and momentum simultaneously.” This difference precisely reminds us that a correspondence does not mean that the objects in the two theories are completely identical.

In summary, these relationships can be viewed as several levels of correspondence:

| Classical mechanics | Quantum mechanics |
|---|---|
| $q,p;\ \{q,p\}=1$ | $\hat q,\hat p;\ [\hat q,\hat p]=i\hbar$ |
| $\dot A=\{A,H\}$ | $\dot{\hat A}=[\hat A,\hat H]/(i\hbar)$ |
| Hamilton–Jacobi equation | Phase equation from the Schrödinger equation |
| Liouville density $f(q,p)$ | Density operator $\rho$ and Wigner function $W$ |

