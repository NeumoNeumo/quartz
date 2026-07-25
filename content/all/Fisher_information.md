---
tags:
  - statistics
  - information-theory
  - machine-learning
  - AI
aliases: []
id: Fisher_information
---
# Fisher information

## Inspiration

In frequentist statistics, we maximize the likelihood to get the optimal parameters. However, this approach only considers the single optimal point which cannot tell us how certain we are about the optimality which can be describe in Bayesian statistics. It is apparent that **a likelihood function with a larger curvature at its maxima indicates more certainty of the optimal parameters.** Fisher information exactly measures the certainty by taking expectation of Hessian matrix at the maxima of the likelihood function.

As shown in [wiki](https://en.wikipedia.org/wiki/Fisher_information):

> [!cite] 
> In mathematical statistics, the Fisher information (sometimes simply called information) is a way of measuring the amount of information that an observable random variable $X$ carries about an unknown parameter $\theta$ of a distribution that models $X$. 

Note that the dividing line between parameters and data is vague -- if A is depend on B, then we can say B is the parameter of A and A is the data generated from a distribution parameterized by B. For instance, B can be the real length of box and A can be the measured length of the box.

## Definition

Use $\boldsymbol{\theta}$ to denote the parameter and $\{\boldsymbol x_i\}_{i=1}^n$ to denote the observable random variable. The likelihood is $L(\boldsymbol x, \boldsymbol\theta) = \prod_{i=1}^n p(\boldsymbol x_i | \boldsymbol\theta)$. The score function is $S(\boldsymbol\theta)=\frac{\partial \ln (L)}{\partial\boldsymbol\theta}$.

Then the *Fisher information* is defined as ^585138
$$
\begin{align*}
I(\boldsymbol \theta) &= - \mathbb E_{\boldsymbol x \sim p(\boldsymbol x | \boldsymbol \theta)} [\nabla_{\boldsymbol \theta} ^ 2 \ln L] \tag 1\\
&= \mathbb E_{\boldsymbol x \sim p(\boldsymbol x | \boldsymbol \theta)}[S^2(\boldsymbol\theta)] \tag 2\\
&= \text{Var}_{\boldsymbol x \sim p(\boldsymbol x | \boldsymbol \theta)}[S(\boldsymbol \theta)] \tag 3
\end{align*}
$$
**Proof** of (1) to (2): 
$$
\begin{align*}
\mathbb E[\nabla ^ 2 \ln L]
=& \mathbb E\left[\frac{\nabla^2L}{L} - \left(\frac{\nabla L}{L} \right)^2 \right] \\
=& \int p(\boldsymbol x | \boldsymbol\theta) \frac{\nabla_{\boldsymbol\theta}^2 L}{p(\boldsymbol x | \boldsymbol\theta)}  \mathrm d \boldsymbol x
- \mathbb E[S^2(\boldsymbol\theta)] \\
=& \nabla_{\boldsymbol\theta}^2 1 
- \mathbb E[S^2(\boldsymbol\theta)] \\
=& - \mathbb E[S^2(\boldsymbol\theta)] \\
\end{align*}
$$
**Proof** of (2) to (3): 
$$
\begin{align*}
\text{Var}[S(\boldsymbol \theta)] 
= \mathbb E[S^2(\boldsymbol \theta)] - \mathbb E^2[S(\boldsymbol \theta)] 
\end{align*}
$$
and
$$
\begin{align*}
\mathbb E[S(\boldsymbol \theta)]
&= \int p(\boldsymbol x | \boldsymbol\theta) \frac{\partial \ln (L)}{\partial\boldsymbol\theta}  \mathrm d \boldsymbol x \\
&= \int p(\boldsymbol x | \boldsymbol\theta) \frac{\nabla_{\boldsymbol\theta} L}{p(\boldsymbol x | \boldsymbol\theta)}  \mathrm d \boldsymbol x \\
&= \nabla_{\boldsymbol\theta} 1 \\
&= 0
\end{align*}
$$
The result is intuitive because it means $\boldsymbol \theta$ is an optimal parameter.


## Properties

1. **Cramér–Rao bound** in the scalar unbiased case: Suppose $\theta$ is an unknown deterministic parameter that is to be estimated from $n$ independent observations (measurements) of $x$, each from a distribution according to some probability density function $f(x;\theta)$. The variance of any _unbiased_ estimator $\hat{\theta}$ of $\theta$ is then bounded by the reciprocal of the Fisher information:
$$
\text{Cov}(\hat\theta) \geq \frac 1 {I(\theta)}
$$
where
$$\displaystyle I(\theta )=n\operatorname {E} _{p(X|\theta )}\left[\left({\frac {\partial \ln f (X;\theta )}{\partial \theta }}\right)^{2}\right]$$
(We have added an $n$ here because $X$ only represents one data point here.)

> [!note] Catch-22
> We need $\theta$ to estimate the lower bound. But if we know $\theta$, why bother estimating it? In practice, we first give an empirical estimation of $\theta$ by LLN(law of large numbers) and then we use that parameter to calculate $I(\theta)$.

2. $$ \mathbb{E}_x \text{KL}(p_{w'}(y|x) \| p_w(y|x)) =\frac 12 \delta w \cdot F \delta w + o(\delta w^2) $$
$$F:=\mathbb{E}_{x\sim\hat{Q}(x)}\mathbb{E}_{y\sim p_{w}(y|x)}\left[\nabla_{w}\log p_{w}(y|x)\nabla_{w}\log p_{w}(y|x)^{T}\right]$$

> [!note]
> KL divergence is not a metric but it acts like a Riemannian metric locally. In short, Fisher information matrix is the Hessian matrix of KL divergence in the parameter space. This is the core of information geometry. The GD in information geometry is NGD(Natural Gradient Descent). $\nabla_w \log p_w(y|x)$ is called *score function*.

## Disambiguity

Let $J_n=\frac{\partial f_n}{\partial\theta}\in\mathbb R^{C\times D}$. Then:

| Object | Formula | Uses |
| --- | --- | --- |
| True Fisher, $F$ | $\frac{1}{N}\sum_n J_n^\top \mathcal I_nJ_n$ | model-sampled labels |
| Empirical Fisher, $F_{\text{emp}}$ | $\frac{1}{N}\sum_n J_n^\top g_ng_n^\top J_n$ | observed labels |
| GGN, $G$| $\frac{1}{N}\sum_n J_n^\top B_nJ_n$ | output-space Hessian |
| Hessian, $H$ | $G+R$ | GGN plus residual |
| NTK, $\Theta$ | $\Theta_{nm}=J_nJ_m^\top$ | function-space kernel |

where

$$
g_n=\nabla_{f_n}\ell(f_n,y_n),
\qquad
B_n=\nabla_{f_n}^2\ell(f_n,y_n),
$$

and

$$
\begin{align*}
\mathcal I_n
&=-\mathbb E_{\tilde y\sim p_\theta(\cdot\mid x_n)}
\left[
\nabla_{f_n}^2 \log p_\theta(\tilde y\mid x_n)
\right]\\
&=\mathbb E_{\tilde y\sim p_\theta(\cdot\mid x_n)}
\left[
\nabla_{f_n}\log p_\theta(\tilde y\mid x_n)
\nabla_{f_n}\log p_\theta(\tilde y\mid x_n)^\top
\right] \\
&=\text{Var}_{\tilde y\sim p_\theta(\cdot\mid x_n)}
\left[
\nabla_{f_n}\log p_\theta(\tilde y\mid x_n)
\right]
\end{align*}
$$

For negative log-likelihood losses, $\mathcal I_n =\mathbb E_{\tilde y\sim p_\theta(\cdot\mid x_n)} [B_n(\tilde y)].$ Therefore, $F =\mathbb E_{\tilde y\sim p_\theta} [G(\tilde y)].$

For common exponential-family likelihoods with natural-parameter network
outputs, $B_n$ does not depend on the label. Then $F=G$. But generally, $F_{\mathrm{emp}}\neq F$ and
$F_{\mathrm{emp}}\neq G$.

The true Fisher and the GGN are both $D\times D$ matrices, where $D$ is the
number of parameters. For modern neural networks, $D$ is usually too large for
the full matrix to be explicitly stored or inverted. **K-FAC** approximates these matrices using layerwise Kronecker-factored structure.

## Fisher information Application

**Chicken and rabbit problem**: There are $\theta_{c}$ chickens and $\theta_r$ rabbits in a cage. We observe that there are $x_{leg}$ legs and $x_{head}$ heads. Given that the observation error $err_{leg},\, err_{head}$ comply to zero-mean normal distributions with variation $\sigma_{leg}, \, \sigma_{head}$ respectively. In order to estimate $\theta_c$ and $\theta_r$ better, should we pay more attention when counting heads or counting legs?

*Answer*: variables $x$ are determined by parameters $\theta$ and errors $err$. The information matrix is
$$
I = 
\begin{bmatrix}
\frac4{\sigma^2_{leg}}+\frac1{\sigma^2_{head}} & \frac8{\sigma^2_{leg}}+\frac1{\sigma^2_{head}} \\
\frac8{\sigma^2_{leg}}+\frac1{\sigma^2_{head}} &
\frac{16}{\sigma^2_{leg}}+\frac1{\sigma^2_{head}}
\end{bmatrix}
$$

If we use $\text{Tr}(I)$ to determine the belief of the estimation, counting legs is more important. If using $\det(I)$, they are equally important.

## Reference
-  [Limitations of the Empirical Fisher Approximation for Natural Gradient Descent](https://arxiv.org/abs/1905.12558)
-  https://zhuanlan.zhihu.com/p/589273267
-  https://zhuanlan.zhihu.com/p/589311732
-  https://zhuanlan.zhihu.com/p/589321752
