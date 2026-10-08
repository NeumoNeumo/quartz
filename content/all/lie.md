---
id: lie
title: "Lie algebra"
aliases: []
tags:
  - math
---

## Definition
For a Lie group $G$, its Lie algebra is first defined simply as the tangent space at the identity and to define the Lie bracket on $T_e G$, consider the left-invariant vector field $\widetilde X(g)=(dL_g)_eX$ then define $[X,Y]_{\mathfrak g} = [\widetilde X,\widetilde Y](e)$.

For a matrix Lie group, $\widetilde X(g) = (dL_g)_eX=gX$. With this convention, the Lie bracket becomes the usual matrix commutator $[X,Y]=XY-YX$. If we use the right-invariant vector field, the Lie bracket should be $[X^R,Y^R]=-[X,Y]^R$ where $X^R(g)=Xg$. Proof:
$$
\begin{aligned}
[\widetilde X,\widetilde Y]f(g)
&=\widetilde X(\widetilde Yf)(g) -\widetilde Y(\widetilde Xf)(g)\\
&=D(\widetilde Yf)_g[\widetilde X(g)] -\cdots\\
&=D(Df_g[\widetilde Y(g)])_g[\widetilde X(g)] - \cdots \\
&=D^2f_g[\widetilde Y(g), \widetilde X(g)] + Df_g[ D\widetilde Y_g[\widetilde X(g)]] - \cdots \\
&=D^2f_g[\widetilde Y(g), \widetilde X(g)] + Df_g[ D\widetilde Y_g[gX]] - \cdots \\
&=D^2f_g[\widetilde Y(g), \widetilde X(g)] + Df_g[\left.\frac{d}{dt}\right|_{t=0}\widetilde Y(g\exp(tX))] - \cdots \\
&=D^2f_g[\widetilde Y(g), \widetilde X(g)]+Df_g[gXY] - \cdots \\
&=Df_g[g(XY-YX)]
\end{aligned}
$$

Therefore, $[X,Y]_{\mathfrak g} = [\widetilde X,\widetilde Y](e)=XY-YX$

Why do we need Jacobi identity in Lie algebra? https://www.zhihu.com/question/32067616/answer/2010150735887766097

## Application in differential equations


