---
id: linearization
title: linearization
aliases: []
tags:
  - nonlinear-dynamics
---

## Global Linearization

Linearize every system at the cost of infinite dimensions. Consider a nonlinear dynamical system $x_{t+1}=f(x_t)$.

Koopman operator defines how functions of the state evolve, $(\mathcal{K}g)(x)=g(f(x))$.

Perron-Frobenius operator defines how the distribution $\mu$ of the state evolve, $(\mathcal P\mu)(A) \;:=\; \mu\!\left(f^{-1}(A)\right)$ where $A$ is a measurable set.

$\mathcal{K}$ and $\mathcal{P}$ are dual, $\langle Ug,\rho\rangle = \langle g,P\rho\rangle$.

## Local Linearization

Obvious
