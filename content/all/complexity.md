---
id: complexity
title: complexity
aliases: []
tags:
  - complex
---

Chaos measures unpredictability, while complexity measures the structured organization of information. Complexity is typically higher between complete order and complete randomness/chaos, rather than increasing monotonically with chaos.

## Mesure the Edge of chaos

- Lyapunov exponent $\lambda \approx 1$. The structure is maintained. The future is partly predicable. But it also has some changes.

> [!note]
> A dynamical system that preserves phase-space volume can still exhibit chaos, e.g. Arnold's cat map.

## Measure the complexity

- Bennett’s logical depth measures how much computational history is needed to produce an object from a nearly minimal description.
- Crutchfield’s statistical complexity is the entropy of the causal states -- the minimal predictive states needed to capture all information from the past that is relevant for predicting the future
- spatial correlation function $C(r)= \langle s(x)s(x+r)\rangle - \langle s\rangle^2$ where $\xi$ is the correlation length. A system at the edge of complexity has $\xi\rightarrow\infty$
- Mutual information $I(X_t;X_{t+\tau})>0$


