---
id: entropy
title: entropy
aliases: []
tags:
  - thermodynamics
  - information-theory
---

There are several distinct notions of entropy, and it is important not to conflate them.

The entropy in thermodynamics is defined to provide a micro-dynamical explanation of the 2nd law of thermodynamics. Although they are defined differently, their leading-order terms are often the same in many models.

### Boltzmann's approach

Boltzmann's approach thinks macrostates supervene on microstates and there's an appeal to typicality. Let the microstates of an element in the system constitute a set $\Omega_\mu$. Then the number of microstates of a system with $N$ elements is $|\Omega_\mu|^N$ which is a very large number. For brevity of calculation (1. we prefer additions to multiplications 2. a physical quantity needs to have a unit, but this number is so large that attaching any unit to it would still make it meaningless), let's take the logorithm of it. We define $S_B(\Gamma(X))=k\ln |\Gamma(X)|$ where $X$ is a microstate and $\Gamma(X)$ is the set of all microstates that considered to have the same macrostate as $X$, $k$ is a constant to make the physical quantity dimensional($\ln|\Gamma(X)|$ is dimensionless).

Suppose $P V=Nk_BT$. In reversible isothermal expansion, $\Delta S_T=Nk_B\ln\frac{V_2}{V_1}$. Then consider from the perspective of statistical physics. For an ideal gas, if the volume accessible to each particle increases from $V_1$ to $V_2$, then, under an appropriate discretization of phase space, the number of possible spatial microconfigurations scales as $V^N$. Then $\Delta S_B =Nk\ln\frac{V_2}{V_1}$. If we want to make $\Delta S_B=\Delta S_T$, we have to choose $k=k_B$. Therefore, $S_B(\Gamma(X))=k_B\ln |\Gamma(X)|$.

A useful approximation to the Boltzmann entropy in the large-particle-number limit. 
$$
\begin{align*}
S_B&=k_B\ln\frac{N!}{\prod_{j=1}^{\ell}n_j!}\\
&=k_B\left(N\ln N-\sum_{j=1}^{\ell}n_j\ln n_j\right)
+O(\ln N)\\
&=Nk_b\ln N-Nk_B\sum_{j=1}^{\ell}p_j\ln p_j
+O(\ln N).
\end{align*}
$$

The first term is constant if we fix $N$ and the second term contains Shannon entropy.

### Gibbs' approach

Consider an ensemble of infinitely many copies of the same system. The distribution is $\rho(x,t)$. A measurement of a property $f$ takes some amount of time, which is "infinite" compared to molecular processes. So our measurement is the time average of $f^*(x)$. For ergodic systems, we have $\langle f \rangle f^*(x)$. We define the Gibbs entropy as $S_G = -k \int_\Omega \rho(x,t) \ln \rho(x,t) dx$.

Let $W=\frac{N!}{\prod_{j=1}^{\ell}n_j!}$. If the ensemble is uniformly distributed over these $W$ microstates, then $S_G=-k\sum_{x\in \Omega} \frac 1W \ln \frac 1W=k\ln W$, which is exactly the Boltzmann entropy. Therefore, we choose $k=k_B$. Ultimately, we have $S_G = -k_B \int_\Omega \rho(x,t) \ln \rho(x,t) dx$.

#STRATEGIC
Problem: I don't think Gibbs' approach explains the 2nd law of thermodynamics.

### Continuous space

Replace "number of states" with "phase-space volume." So we need a measure, for example $d\mu(\Gamma)=\frac{d^{3N}q\,d^{3N}p}{N!h^{3N}}$. 

Why dividing $N!$? The set of configurations satisfying $z_1=z_2$ has zero measure in the full twelve-dimensional phase space. And we want to identify the physically distinquishable microstates. 



### Application

We can use $\text{maximize}\quad S = k_b \sum_{j=1}^{\ell}n_j\ln n_j$ s.t. $\sum_j n_j = N$ and $\sum_j \varepsilon_j n_j = U$ to derive the Maxwell-Boltzmann equilibrium distribution $n_j = \frac{N}{Z} e^{-\varepsilon_j / kT}$.

