---
id: LLM
aliases: []
tags:
  - AI
---

## Facts

- 用句子最后一个token的hidden state表示模型对句子的理解，可以认为hidden state分布在一个流形上。流形维数更高意味着死记硬背，反之则泛化。预训练中维数先急剧降低（因为模型一开始什么都不会，呈现出极高的维度），然后又升高（开始死记硬背），又减小（泛化）。在后训练中，SFT与DPO会导致维数升高（提高in-distribution效果，降低ood效果，因为有大量指令风格、语气、安全围栏等内容需要记忆），RLVR则减小（因为在过度优化单一目标，例如数学、代码等）[^1]

#todo
- transformer的平台期主要是因为attention训起来太困难导致的。在此平台期模型的陷入的低秩状态，可能会有例如复读、不同token的表征坍塌的情况。一旦attention训好了，loss下降会很快，造成grokking。如果使用muon，由于抗低秩能力，在平台期间保护了模型的丰富表达能力，从而减小了平台期的停留时间。 [^2] **但在这篇文章中，平台期间，模型没有发生rank的明显下降，但在模型跑出平台期的时候发生了rank的明显下降。这似乎与上一条fact是矛盾的。这是怎么回事？另外，muon似乎能够抵御rank collapse，但似乎有利于generalization的neural condensation正依赖于rank collapse，这是否矛盾？**

- Transformer内部的信息可能并不完全是以lookup table的形式储存的，如果所训练的数据有比较好的结构，则也可能产生像word2vec一样的几何性 [^3]

- Instruction following is not a single capability. When current information conflicts with memory, smaller models are more likely than larger models to trust the current information[^4], possibly because their internal memory is weaker. On the other hand, smaller models are also more prone to misreading rules, missing constraints, and shortcutting reasoning.

LoRA调整的未必是大奇异值的方向。PiSSA调整大的奇异值，MiLoRA调整小的奇异值，CorDA调整任务样本协方差的方向

## Ref

[^1]: [Tracing the Representation Geometry of Language Models from Pretraining to Post-training](https://arxiv.org/abs/2509.23024)
[^2]: [What Happens During the Loss Plateau? Understanding Abrupt Learning in Transformers](https://arxiv.org/abs/2506.13688)
[^3]: [Deep sequence models tend to memorize geometrically; it is unclear why](https://arxiv.org/abs/2510.26745)
[^4]: [Knowledge Conflicts for LLMs: A Survey](https://aclanthology.org/2024.emnlp-main.486/)
[^5]: [Finetuned Language Models Are Zero-Shot Learners](https://arxiv.org/abs/2109.01652)
