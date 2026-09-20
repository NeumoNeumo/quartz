---
id: intelligence
title: intelligence
aliases: []
tags: []
---

## Definition

There's a saying "compression is intelligence" in the field. But compression merely builds a bridge between the real world and the representation world. What we need is not just compression, but representations in which the patterns governing how the features change are easy to analyze. For example, we may model a projectile as a point mass (compression) and then use Newton’s laws of motion to calculate its trajectory (ease of analysis). By contrast, if we simply compress the data with zstd, the compressed result is not amenable to meaningful manipulation or reasoning; that alone does not constitute intelligence.

The claim that "compression is intelligence" is much like the ancient belief that "the heart is the seat of consciousness": in both cases, the most conspicuous feature of a system is taken to characterize the system as a whole. In LLMs, that conspicuous feature is the NLL loss. What makes the idea particularly seductive is that LLMs model conditional probabilities, so prediction and compression are effectively equivalent concepts within this framework. It is therefore not surprising that people are led to mistake compression for intelligence itself.

In my opinion, *intelligence is the ability of a system to achieve goals efficiently across a broad range of environments*.This is similar to Simon and Newell’s view of intelligence in their 1975 Turing Award lecture paper: an intelligent system must adapt its behavior to the task environment and achieve its goals despite limitations on its computational capacity. "efficiently" corresponds to "limitations" and "broad" corresponds to "adapt".


