---
id: nn_init
title: initialization in neural networks
aliases: []
tags: []
---

Adjusted learning rates and activation multipliers are equivalent. We'll use former here.

Forward stability requires $||W_{\text{in}}||_{\text{RMS}} = \Theta(1/\sqrt{d_{in}})$, $||W_k||_{\text{RMS}} = \Theta(1/\sqrt{d})$, $||W_{\text{out}}||_{\text{RMS}} = \Theta(1/d)$.

Then the gradient is $||\nabla_{W_{\text{out}}}\mathcal L||_{\text{RMS}} = \Theta(1)$, $||\nabla_{h_{k+1}}\mathcal{L}||_{\text{RMS}} = \Theta(1/d)$, $||\nabla_{W_{k}}\mathcal L||_{\text{RMS}} = \Theta(1/d)$, $||\nabla_{h_{k}}\mathcal L||_{\text{RMS}} = \Theta(1/d)$, $||\nabla_{W_{\text{in}}}\mathcal L||_{\text{RMS}} = \Theta(1/d)$.

Backward effectiveness requires $\Theta(1)= \langle \Delta, \nabla \rangle=\langle \mu\nabla,\nabla \rangle =\mu||\nabla||_{\text{RMS}}^2 \cdot \#\{\text{elements}\}$. Therefore, $\mu_{W_{\text{out}}}=\Theta(1/d)$, $\mu_{W_{k}}=\Theta(1)$ and $\mu_{W_{\text{in}}}=\Theta(d/d_{\text{in}})$. 

The relative changing rates of the hidden matrix and the output matrix are different.
$$
\frac{\|\Delta W_{\mathrm{out}}\|_{\mathrm{RMS}}}
{\|W_{\mathrm{out}}\|_{\mathrm{RMS}}}
=\Theta(1),\qquad
\frac{\|\Delta W_k\|_{\mathrm{RMS}}}
{\|W_k\|_{\mathrm{RMS}}}
=\Theta(d^{-1/2}),\qquad
\frac{\|\Delta W_{\mathrm{in}}\|_{\mathrm{RMS}}}
{\|W_{\mathrm{in}}\|_{\mathrm{RMS}}}
=\Theta(d_{in}^{-1/2})
$$

Interestingly, this means even in the layers except the last one, the weight is almost unchanged over the course of the training. But note that this does not mean features are unchanged as well. So we cannot say this implies a slow-fast separation of the training dynamics. In fact, this can be shown from the operator norm more explicitly.

$$
\frac{\|\Delta W_{\mathrm{out}}\|_{\mathrm{op}}}{\|W_{\mathrm{out}}\|_{\mathrm{op}}} =\Theta(1),\qquad
\frac{\|\Delta W_k\|_{\mathrm{op}}}{\|W_k\|_{\mathrm{op}}} =\Theta(1),\qquad
\frac{\|\Delta W_{\mathrm{in}}\|_{\mathrm{op}}}{\|W_{\mathrm{in}}\|_{\mathrm{op}}} =
\Theta\!\left(
\frac{\sqrt{d/d_{\rm in}}}{1+\sqrt{d/d_{\rm in}}}
\right)
$$
