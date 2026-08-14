---
id: combinatorics
aliases: []
tags:
  - combinatorics
---

## Methods

- [[select_a_representative]]
- [[randomness]]
- Language mutation:
    - Proof mutation: For example, https://blog.neumo.top/posts/basic_ops_game/ and https://zhuanlan.zhihu.com/p/1992751090786116988
        - Simplify your current proof: Eliminating unecessary mess will make essential structures arise, which may give you some insights. 
        - Exchange the order of your assumptions
        - Modify some words
    - Condition mutation:
        - Make it stronger, weaker, etc.
        - Formalize the combinatorial condition and think when you can use it. e.g. [[2021_CTST#^722055]]

## Catogories

### Existence problem

See [[existence_problem]]

### Multi-step Games

Keywords: optimal strategy, game theory

How to prove that a strategy is the optimal?
- Adjustment method. The philosophy behind the method is the following: Proofs are expressed through language, so if we want to find a better strategy, we also need to describe that strategy in words. However, a general strategy is difficult to articulate in language. Therefore, we need to rely on a sequence with known properties as a template, modifying and restructuring it to form a description of a better strategy -- much like genetic engineering.
    - Consider a bigger space.
        - Make a discrete action continuous, e.g. [this question](https://zhuanlan.zhihu.com/p/1992751090786116988)
        - Make the value function act on subsets instead of the entire set, e.g. [this question](https://blog.neumo.top/posts/basic_ops_game/)
- Conserved quantity and monotonic quantity. e.g. [Consway's Soldiers](https://en.wikipedia.org/wiki/Conway%27s_Soldiers), 
information theory

How to solve a puzzle in video games?
- Endgame analysis: It is easier to analyze backwards because the endgames of many games(e.g. [parabox](https://en.wikipedia.org/wiki/Patrick%27s_Parabox), [Kami](https://store.steampowered.com/app/272040/KAMI/)) are quite closed or finite. 
- Feasible-region analysis: The items in the game have strong limitations even without considering their interaction with others. For example, in [Sokoban](https://en.wikipedia.org/wiki/Sokoban), a box cannot be pushed to a corner.

### Other Games

How to prove that a real number is the optimal?
- Rewrite the quantity that is easier to derive. 
    - rewriting LHS in exp removes the $\pi/2^n$ on RHS in [[inequality#^272055]]
    - rewriting the sum in alternating sum simplify the $\frac{2^n}{2^{n+1}-1}$ to $\frac{1}{2^{n+1}-1}$ in [[select_a_representative#^271304]].
    - It can also be seen in many derivations of real analysis and inequalities.
- To prove a series of positive numbers has a lower bound.
    - Select part of them that is easier to calculate.
        - Flipping some terms of alternative sums make the calculation reduces to the lengths of Liu's sticks. [[select_a_representative#^271304]]
        - A direct usage is [[select_a_representative#^260220]]
        
