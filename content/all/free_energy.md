---
id: free_energy
title: "free energy"
aliases: []
tags:
  - thermodynamics
---

## Minimization of Free Energy

### Method 1: Consider the Whole System

Consider a system $A$ and a sufficiently large heat reservoir $B$. Combining them gives an isolated system. Then 

$$
\begin{aligned}
\Delta S_{\mathrm{tot}}
&=\Delta S_A+\Delta S_B\\
&=\Delta S_A-\frac{\Delta U_A}{T}\\
&=-\frac{1}{T}\Delta(U_A-TS_A).
\end{aligned}
$$

So we can define the Helmholts free energy as $U-TS$

Also

\begin{aligned}
\Delta S_{\mathrm{tot}}
&=\Delta S_A+\Delta S_B\\
&=\Delta S_A+\frac{\Delta U_B+p\Delta V_B}{T}\\
&=\Delta S_A-\frac{\Delta U_A+p\Delta V_A}{T}\\
&=-\frac{1}{T}\Delta(U_A+pV_A-TS_A)
\end{aligned}

yields Gibbs free energy.

### Method 2: Canonical Ensemble

In the canonical ensemble, the ratio of the probabilities of these two types of states is $\frac{P(B)}{P(A)} =\frac{\Omega_1 e^{-\beta E_1}}{\Omega_0 e^{-\beta E_0}}$. Taking the logarithm yields the Helmholts free energy.

Similarly,

| External constraints | Ensemble | Potential minimized at equilibrium |
| --- | --- | --- |
| Fixed $U, V, N$ | Microcanonical | Maximize $S$ |
| Fixed $T, V, N$ | Canonical | $F = U - TS$ |
| Fixed $T, p, N$ | Isothermal–isobaric | $G = U + pV - TS$ |


