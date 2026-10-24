---
id: direct_sum_product
title: "direct sum and direct product"
aliases: []
tags:
  - math
  - category-theory
---

coproduct本身不能解释为什么直和不能取无限支撑，例如在集合范畴中disjoint union我们就直接take it for granted了，从来没有问过所谓的“为什么没有无限支撑”问题。问题源于具体范畴（尤其是finitary algebraic categories）本身所要求的结构。我们先来看coproduct的定义

存在态射 $\iota_i:M_i\to \bigoplus_i M_i$，使得对任意 $X$ 和任意一族 $f_i:M_i\to X$，存在唯一 $f:\bigoplus_iM_i\to X$，满足 $f\circ\iota_i=f_i$

我们在使用$f$之前会先过一个嵌入映射$\iota_i$，并且我们要求没有信息损失，因此我们希望存在一个object “不重叠地包含” $\text{im}(\iota_i)$的最小object，并且这个object上只要每次能够单独承载一个$\text{im}(\iota)$就好了，而这个object就是余积。于是最自由的情况下，我们得到的就是集合范畴的disjoint union，但阿贝尔群范畴和向量范畴这些附加了结构的范畴不能让这个object中只包含那些元素，还需要让那些元素在相关运算下保持封闭，于是才有了有限支撑，但也仅此而已。问向量空间中的直和为什么没有无限支撑就像问整数加法群中包含2的最小子群为什么不包含实数一样——什么是实数？我们的论域中从来就没有实数。

如果我们将态射$A\rightarrow B$视为用B中的元素去给A中的元素染色，那么积就是把$M_i$看成颜料，一系列（这个量词听上去是至多可数无穷的，但读者应该能理解也可以是不可数的）到$M_i$的态射对应一系列染色操作，而积空间中的一个object就是一套染色方案，我们要考虑所有可能的染色方案，这种所有的可能性在向量空间中自然就对应无限支撑；而余积是把$M_i$看成瓷砖，一系列$M_i$射出的态射对应一系列染色操作，而余积空间中的一个object对应一套染色方案，我们只要求把瓷砖排在一起，染色的颜色信息被编码在$f$中了，而信息的读取则交给$\iota$，而且每次只由$\iota$取一块查$f$，于是作为中间对象的“排在一起”的瓷砖则很轻松，能span出有限支撑那还是范畴结构的功劳呢，要不直接摸鱼成disjoint union了。

product是信息的总体存储空间(将这个态射叫$f$)，逐个读出（将这个态射叫$\iota$），所以存储空间要够大；coproduct则压根没存信息，它只能算做了个wrapper。数据大头都是在$f$上的，但仅仅因为preimage与image的差异就让product与coproduct迥然不同（还有映射基数的计算中$|A|^{|B|}$，两者地位完全不一样）。以此观之，image与preimage的差异就像夫妻与夫妻肺片的差异一样大啊，尽管它们在形态上经常长得差不多，比如都是集合或都是群。
