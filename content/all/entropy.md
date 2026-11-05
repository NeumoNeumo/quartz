---
id: entropy
title: entropy
aliases: []
tags:
  - thermodynamics
  - information-theory
---

There are several distinct notions of entropy, and it is important not to conflate them. But all of them are measuring the cardinality of equivalence classes on a log scale.

The entropy in thermodynamics is defined to provide a micro-dynamical explanation of the 2nd law of thermodynamics. Although they are defined differently, their leading-order terms are often the same in many models.

### Boltzmann's approach

Boltzmann's approach thinks macrostates supervene on microstates and there's an appeal to typicality. Let the microstates of an element in the system constitute a set $\Omega_\mu$. Then the number of microstates of a system with $N$ elements is $|\Omega_\mu|^N$ which is a very large number. For brevity of calculation (1. we prefer additions to multiplications 2. a physical quantity needs to have a unit, but this number is so large that attaching any unit to it would still make it meaningless), let's take the logarithm of it. We define $S_B(\Gamma(X))=k\ln |\Gamma(X)|$ where $X$ is a microstate and $\Gamma(X)$ is the set of all microstates that considered to have the same macrostate as $X$, $k$ is a constant to make the physical quantity dimensional($\ln|\Gamma(X)|$ is dimensionless).

Suppose $P V=Nk_BT$. In reversible isothermal expansion, $\Delta S_T=Nk_B\ln\frac{V_2}{V_1}$. Then consider from the perspective of statistical physics. For an ideal gas, if the volume accessible to each particle increases from $V_1$ to $V_2$, then, under an appropriate discretization of phase space, the number of possible spatial microconfigurations scales as $V^N$. Then $\Delta S_B =Nk\ln\frac{V_2}{V_1}$. If we want to make $\Delta S_B=\Delta S_T$, we have to choose $k=k_B$. Therefore, $S_B(\Gamma(X))=k_B\ln |\Gamma(X)|$.

A useful approximation to the Boltzmann entropy in the large-particle-number limit. 
$$
\begin{align*}
S_B&=k_B\ln\frac{N!}{\prod_{j=1}^{\ell}n_j!}\\
&=k_B\left(N\ln N-\sum_{j=1}^{\ell}n_j\ln n_j\right)
+O(\ln N)\\
&=Nk_B\ln N-Nk_B\sum_{j=1}^{\ell}p_j\ln p_j
+O(\ln N).
\end{align*}
$$

The first term is constant if we fix $N$ and the second term contains Shannon entropy.

Consider the following gas-mixing thought experiment: There are two types of ideal gas that behave identically under all ordinary experimental conditions. They are confined in two volumes seperated by a diaphragm. Scientists think the entropy change after removing the diaphragm is 0. However, after years, scientists find a way to distinguish them. So the entropy change should be a positive number.

The formula is the same but with different interpretations, their result is different.

> [!note]-
> Textbooks often present the derivations within the theoretical framework in a clear and orderly manner. However, beginners who lack an understanding of the underlying interpretation may still struggle to understand how the formulas relate to reality.
> 
> Consider the addition of two integers. A textbook might explain how to perform column addition without ever explaining what numbers actually represent. The connection between the question "If you put 3 apples together with 2 apples, how many apples do you have?" and the mathematical expression "3 + 2 = ?" is not self-evident. What lies between the two is precisely interpretation.
> 
> In more complicated problems, this interpretative process can become so bewildering that even trying to identify the source of one's own confusion can generate further confusion. How can you talk about a concept that you yourself can barely grasp? At the same time, how are those who take the connection between "3 apples" and the numeral "3" for granted supposed to realize that this very connection might be difficult for beginners to understand?
> 
> To make matters worse, explaining the interpretation itself may require an even higher level of abstraction. Consider, for example, explaining that the practice of counting is isomorphic to the Peano axioms. This is hardly something a beginner can readily accept.
> 
> If we extend Wittgenstein's reflections in On Certainty to this context, we might say that our confidence in a theory comes from repeatedly verifying its correctness within the corresponding system of verification. However, the legitimacy of the verification system itself is difficult to justify by appealing to anything further.
> 
> (It is not that such a justification is impossible, but, as I mentioned above, it would require an even higher level of abstraction. And abstraction takes us into territory far removed from language. An infinite regress would eventually lead us to a kind of frontier where language almost disappears (some might object that language has not disappeared -- indeed, that is precisely why I say it has disappeared (all right, I admit that this sentence is rather cryptic; see Wittgenstein's private language argument and his account of what constitutes language (anyway, there is one thing you should take away from this: as we move to increasingly meta levels of discussion (as the parentheses grow deeper and deeper), we gradually lose the ability to understand what one another is talking about)))).
> 
> Ultimately, its foundation lies in our form of life.
>
> tldr: If you're struggling to understand your physics textbook, try working through some problems.

### Gibbs' approach

Consider an ensemble of infinitely many copies of the same system. The distribution is $\rho(x,t)$. A measurement of a property $f$ takes some amount of time, which is "infinite" compared to molecular processes. So our measurement is the time average of $f^*(x)$. For ergodic systems, we have $\langle f \rangle f^*(x)$. We define the Gibbs entropy as $S_G = -k \int_\Omega \rho(x,t) \ln \rho(x,t) dx$.

For example, let $W=\frac{N!}{\prod_{j=1}^{\ell}n_j!}$. If the ensemble is uniformly distributed over these $W$ microstates, then $S_G=-k\sum_{x\in \Omega} \frac 1W \ln \frac 1W=k\ln W$, which is exactly the Boltzmann entropy. Therefore, we choose $k=k_B$. Ultimately, we have $S_G = -k_B \int_\Omega \rho(x,t) \ln \rho(x,t) dx$.

Note that in the microscopic evolution, the Liouville's theorem implies $\frac{dS_G}{dt}=0$. Coarse-graining are required in Gibbsian accounts of irreversible behavior.

### Clausius

$S(B)-S(A)=\int_A^B\frac{\delta Q_{\mathrm{rev}}}{T}$.

### Continuous space

Replace "number of states" with "phase-space volume." So we need a measure, for example $d\mu(\Gamma)=\frac{d^{3N}q\,d^{3N}p}{N!h^{3N}}$. 

Why dividing $N!$? The set of configurations satisfying $z_i=z_j$ has zero measure in the phase space. And we want to identify the physically distinguishable microstates. Why physically distinguishable? [Gibbs paradox](https://en.wikipedia.org/wiki/Gibbs_paradox).

Why dividing $h^{3N}$? First we we want $d^{3N}q\,d^{3N}p$ to be dimensionless. But can we divide $\bar h^{3N}$? When calculating the entropy in a system with a fixed particle number. It is OK to do so because the factor will be cancelled out. But chemical potential is influenced by the factor. $\mu_\hbar=\mu_h-3k_BT\ln(2\pi).$ In the reaction $A\rightleftharpoons 2B$, The equilibrium condition is $\mu_A = 2\mu_B$. So $\mu_\hbar$ and $\mu_h$. To explain $h^{3N}$, let's consider what's the microstate number in the scale of quantum mechanics. 

https://chatgpt.com/g/g-p-6a28f2b7ec2881919aee4ffe05b53d19-fun/c/6ae2bf0a-0854-83e8-b67e-c1b31076a8e6
https://chatgpt.com/g/g-p-6a28f2b7ec2881919aee4ffe05b53d19-fun/c/6ae544ff-215c-83e8-b4be-92c804097933
THE GIBBS PARADOX E. T. Jaynes Department of Physics. Washington University
https://www.cpt.univ-mrs.fr/~verga/pdfs/Lebowitz-1993xw.pdf
https://newquanta.com/wp-content/uploads/2026/03/e9878de695b4e58c96e7bea4e79086e8aeba.pdf




### Application

We can use $\text{maximize}\quad S = k_b \sum_{j=1}^{\ell}n_j\ln n_j$ s.t. $\sum_j n_j = N$ and $\sum_j \varepsilon_j n_j = U$ to derive the Maxwell-Boltzmann equilibrium distribution $n_j = \frac{N}{Z} e^{-\varepsilon_j / kT}$.


