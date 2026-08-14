---
tags:
  - complex
  - nonlinear-dynamics
aliases: []
id: Complex_System
---

"*Bifurcations and Phase Transitions in the Origins of Life*" introduced some complex system researches in biology. 

Takeaways:
- The spontaneous symmetry breaking of chirality only requires simple rules as long as there are mechanisms that enable *exponential proliferation* and *equal annihilation*. $\Phi$ represents CPC(Constant Population Constraint) condition below: 
$$
\begin{align*}
\frac{d x_{1}}{dt} &= \mu x_{1} - \beta x_{1}x_{2} - x_{1}\Phi(x_{1},x_{2}) \\
\frac{d x_{2}}{dt} &= \mu x_{2} - \beta x_{1}x_{2} - x_{2}\Phi(x_{1},x_{2})
\end{align*}
$$
- If there are mechanisms that enable *exponential proliferation* and *interactive equal proliferation*, then it reaches a stability of the 2-member hypercycle. 
$$
\begin{align*}
\frac{d x_{1}}{dt} &= \mu x_{1} + \Gamma x_{1}x_{2} - x_{1}\Phi(x_{1},x_{2}) \\
\frac{d x_{2}}{dt} &= \mu x_{2} + \Gamma x_{1}x_{2} - x_{2}\Phi(x_{1},x_{2})
\end{align*}
$$
- In quasi-species theory, the dominance of longer genome sequences requires lower error threshold. Application:
	- RNA replicator has a higher error rate than DNA. That's why complex life forms choose DNA as genetic material. Only RNA virus carries genetic information on RNA.
	- Increasing the error rate of replication is a way to kill bacteria.
- As the type of molecules and related reactions increases, there is a critical point at which large connected networks of reactions are inevitable, resulting in a autocatalytic cycle. This theory is based on [Erdos-Renyi model](https://en.wikipedia.org/wiki/Erdős–Rényi_model).
