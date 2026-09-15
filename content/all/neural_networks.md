---
id: neural_networks
title: Neural Network
aliases:
  - Neural Network
tags:
  - AI
---

## Tricks

- 可以使用free probability theory的工具更方便地计算随机矩阵的**乘积**或**求和**或经过**激活函数**后的谱 [^12]
- 可以用Generalized Gauss-Newton approximation, GGN，近似Hessian矩阵 $H \approx J^T \nabla^2 L_{loss} J$。
- 如果直接自下而上构建mechanistic theory不方便，可以试试自上而下构建normative theory，也可以在本层级构建effective theory

## Facts

同transformer族模型的最终 Loss 几乎只与总参数量、计算量（但不能太小，因为有一段欠拟合的常数loss区）和数据量（假设数据质量保持不变）有关，而对具体的深度/宽度比例呈现出极大的鲁棒性（在一定范围内）。[^1]

给定计算量下，参数量和数据量应该以 1:1 的比例同步增加以获得最好的性能。[^2]

在FFN中，考虑训练中不同层的hidden states的输出频率变化。一开始差别不大，深层的高频分量比低层稍微多一点；随训练进行，深层低频分量显著变多，浅层低频分量显著减少，直到深层的低频分量多于浅层的[^3]。考虑我们输入一个圆形轨迹，最后会输出什么，显然输出函数复杂度随深度指数级增大，浅层参数的波动会对结果造成很大影响[^29]。一些对抗攻击的文章也显示模型对浅层扰动更敏感[^30]。

#todo
https://chatgpt.com/c/69ee36aa-dcb0-83e8-ab36-250cbf5722f3 文章声称$\lambda_{\max}$ 能很好地衡量训练损失曲面在最陡方向上的“尖锐程度”，但不能可靠地衡量模型泛化能力。又是一篇universal weight subspace吗？它用测试集上的训练表示所谓的泛化能力，这合理吗？可以让AI来批判一下。

- 预训练后的模型停在多任务平均loss较低的位置，但这不一定对于单个任务是最好的。随模型规模增大在此点周围随机扰动给下游任务带来更好的表现的概率也越大，当然我们可以想象如果模型足够大，它的优化足够好，那么随机扰动带来的提升也是有限的。[^27] 随机扰动有时可以隧穿GD难以跨越的loss山峰,[^33]

- 随模型规模增大，fine-tuning时effective DOF会变小。[^28]

- mode connectivity: 深层网络中的最优解往往可以通过training&testing loss几乎不变的连续曲线连接起来[^4]。 其实，模型的loss basin不是平底锅，而是维数接近网络参数量的就像细胞骨架一样的高维复杂流形。这些方向中很多是由于网络的缩放不变性与置换不变性导致的守恒量对应的方向。一个有趣的事实是随机初始化后训练得到的两个过参数化的模型的参数往往存在一个置换能将它们权重匹配[^5]，在置换后的空间中线性插值也能使得模型效果不变。

- Subliminal Learning经验上观察到如果让一个带有特定隐性偏好（例如“喜欢猫头鹰”或“带有潜在恶意”）的 Teacher 模型生成完全无关的格式化数据（如纯数字序列或代码片段），并在严格过滤掉任何相关语义词汇后用于蒸馏同参数的 Student 模型，Student 依然会继承这种隐性偏好 [^16]。它反映的是模型行为模拟对参数的影响，具体来说，就是相似参数的两个模型，其中一个模拟另一个的输出行为，则它们的参数会更加靠近，也因此它们在其它任务上的表现也会趋近。其实人也有类似的机制，当我们在临摹某些书法大家的作品时是可以感受其为人的——所谓字如其人——于是在学习其字帖的时候也会受其性格的感染。类似的还有用人造的符号语言做pre-pretraining[^31]，以及emergent misalignment/alignment[^32]。

#todo
- [ ] 更多内容：https://gemini.google.com/app/8f7207707a2d6352 https://gemini.google.com/app/0728971d7fc90683 https://gemini.google.com/app/7e9c51e9193c477d https://gemini.google.com/app/65651655acc73178 https://gemini.google.com/app/5981a2dc703e075d https://chatgpt.com/c/69eb78be-e8d0-83e8-a5a7-075830e920e6 https://chatgpt.com/c/69eb6d30-ff6c-83e8-87c9-d3ccb5eb89f6 https://chatgpt.com/c/69eb4f32-d024-83e8-9d15-8cdd3fcd9984 https://chatgpt.com/c/69edb3d6-adb0-83e8-8160-4bf4fcba3e18 https://chatgpt.com/c/69eb6d30-ff6c-83e8-87c9-d3ccb5eb89f6 https://chatgpt.com/c/69f0665b-7f28-83e8-83bc-0764ec1f7ef7 https://gemini.google.com/app/a1cab97df8bdf24e https://gemini.google.com/app/55aa420eb9b48f95 https://chatgpt.com/c/69f2bb60-36e4-83e8-834b-f6f67f87fb37 https://chatgpt.com/c/69eb48f0-50f0-83e8-b03b-e8a99cbab0e5
- [ ] weight decay对low rank应该有促进作用，有没有理论框架对其进行分析？例如tensor program框架下如何看待low rank与weight decay？在没有wd的时候，模型会表现出low rank吗？
经过海量预训练后，权重 $W_0$ 会停留在损失地形的一个**高维平坦流形（而非严格极小值点）**附近。此时的 Hessian 矩阵呈现明显的低秩结构：由于数据的核心特征，存在极少数极大的特征值（极度敏感方向）；同时由于模型的过参数化、架构对称性以及 Softmax 的饱和效应，存在海量接近于零甚至为零的特征值（极度平坦方向）；此外，还夹杂着少量负特征值（意味着其实是鞍点区域）。这可以解释[The Universal Weight Subspace Hypothesis](https://arxiv.org/abs/2512.05117)为什么不同的任务学到的LoRA的主成分很大程度上是重叠的。从NTK的角度说(如果lora调整不是很大)，模型的动力学是由NTK中的最大的那几个特征值主导的，因此低秩不足为奇(推导可见[此](https://gemini.google.com/share/a2ed81daecbc))。

如果直接对图像做PCA，通常得到低频的傅立叶基。但如果我们给模型加上稀疏性要求，它就可以学到局部特征。这是因为在傅立叶基下，局部的信号需要用一大堆全局傅立叶基来拟合，但如果使用诸如Gabor filter的局部特征，则更快捷。[]

随着模型变大，hidden state协方差的spectrum的entropy线性增长而其Participation Ratio增长更缓慢[^25]。不要把 FFN 宽度当作“越大越好”的单调旋钮，而应把它看作 尾部容量与核心主导模式容量之间的权衡

有研究[^18]用Dyson Brownian motion建模随机矩阵的特征值的演化，显式给出了RBM的特征值动力学。又在神经网络模型中empirical计算特征值的归一化间距分布，符合Wigner surmise(顺便一提，无限宽矩阵的归一化间距分布实际上是由Fredholm 行列式给出的，但那太复杂了，Wigner surmise是一个简洁的近似。又顺便一提，同分布并不代表同间距分布，例如直线上的泊松点过程与晶格分布)，说明Dyson Brownian motion在神经网络中可能也是存在的。我的评价：梯度实际上是low rank的，实际上并不符合Dyson Brownian motion的噪声各向同性假设。

weight decay可以诱导低秩的原因：
- weight decay对矩阵而言相当于Feobenius norm，也就是对矩阵奇异值大小的regularization。
- 注意到$\min_{W_k \dots W_1 = W} \frac{1}{k} \sum_{i=1}^k \|W_i\|_F^2 = \|W\|_{S_{2/k}}^{2/k}$，因此多层线性网络在weight decay下的优化相当于对整个系统的low rank的优化，网络越深这种现象会因为$S_{2/k}$范数而越明显。^851862 [^23]

#todo
在大奇异值方向上微调[^21]类似于对full fine-tuning的一个近似，相比于传统LoRA，它直接对其了奇异值方向因而有更快的收敛速度。然而，正如在memory研究中经常发现的“调整主路会导致遗忘”，直接进行这样的微调可能会损失预训练时的性能(“马嘉祺效应”[^24]便是后训练时“嘉祺”token被淹没而导致的)，所以也有选择在小奇异值方向上进行微调的[^20]，效果甚至更好。这也启示我们，有时候不加约束地end-to-end未必是最优的。CorDA[^22]则是他们的task-aligned version，调的不是权重矩阵的奇异值方向而是输入的相关性矩阵与权重矩阵的乘积。但这个式子的合理性存疑，这一点在后续工作中有更多讨论 https://chatgpt.com/c/69ff3aca-7a00-83a2-98c6-708105490fdc
^105453

这篇文章[^19]指出muP下Hessian的训练中的sharpness(最大Hessian特征值)的曲线几乎重合，而NTK则不是，所以muP scaling起来练起来比较模型的loss曲线比较一致。

#todo
数据的训练数据的顺序(例如curriculum learning)能像改架构与超参数一样对模型的训练产生显著影响吗？是不是可以从神经马太效应的角度解释？

#todo
Implicit Bias of Dropout: https://arxiv.org/pdf/1806.09777

#todo
- [ ] 理论上如何处理的
此文[^17]从理论与实验上均证明了更小的batch size, 更高的lr，以及weight decay都可以增强SGD中让参数矩阵low rank的bias

工程应用：GaLore(Gradient Low-Rank Projection)[^13]每隔一段时间计算全量梯度矩阵的前几项左右主奇异向量，优化器只需要记录低维矩阵$\tilde{G}_{t+\Delta t} = P_t^T G_{t+\Delta t} Q_t$，于是节约显存；ReLoRA(High-Rank Training Through Low-Rank Updates)[^14]不断重新初始化与合并LoRA。

理论应用：梯度的low rank特性在分析中有时也很有用，例如简化动力学分析过程，只考虑少数的几个主成分而不是整个矩阵，再例如在范数上可以认为$||\nabla_W L||_* =\Theta (|| \nabla_W L||_2)$ 当$L$的尺寸趋向无穷。

> [!Note]
> entry-wise norm, induced/operator norm, Schatten norm都有自己的$L_p$ norm，都可记作$|W|_p$，但它们是不同的。例如Schatten norm的$||W||_\infty$等于induced norm的$||W||_2$

- Loss landscape超乎想象地复杂，对于任意一个图片你都能在loss空间中找到一个二维界面与这张图片一样。[^6]

- 嵌入原则(embedding principal)对认为小的子网络嵌入在更宽的网络中是更退化的，也就是Hessian matrix的特征值为0的重数更大的，也就是占据更多空间的，因此更容易跑到小的子网络中，获得性能的提升 [^7]。这与LTH有类似之处的，后者也表示越宽的网络包含有效子网络的可能性越大。

- 乐观估计认为大模型的很多参数变动对输出的影响是同质化、高度重叠的，因此其有效参数并没有那么大，尤其是在参数凝聚的时候，于是可以使用更少的样本对目标函数进行拟合 [^8]。这似乎与SLT的观点有类似之处。
  
- 数据与模型匹配中的不稳定区域是存在的，即当数据的复杂度和多样性都处于中间水平时，模型可能会在训练中反复横跳于死记硬背与泛化之间，并因不同的随机种子最终两极分化地收敛为死记硬背或泛化 [^9]。这可能显示了内部回路的赢者通吃，就像相变一样。

#todo
- 多层网络中浅层一般收敛更快。尽管可能浅层的梯度辐值更小，但它们的landscape更平坦，使得梯度更可预测。此外，浅层偏向于拟合低频特征，深层则高频。[^10]在训练过程中，随着网络深度的增加，更深层所面临的“有效目标函数”会越来越向低频方向偏移 [^11]。关于为什么在良好的初始化的情况下深层的网络的收敛速度比浅层网络更慢的更多信息 https://gemini.google.com/app/b39ff2e6cf48732f

- 这篇文章[^15]指出随着神经网络训练，其内部交互网络的多重分形谱逐渐变宽，这体现了模型内部连接模式异质性的提升；多重分形谱整体向左移动（即不规则性指标降低）说明其稀疏性在不断增强 ([这里](00-Attachments/multifractal.html)有一个不错的可视化)。但我对它对神经元距离的定义不太满意。另外，这种表现一般是危机或相变的标志，例如2008金融危机爆发前夕及期间的标普500、DDoS中的流量、震前能量涨落等。

#todo
我认为另一个研究前景的可能是最优batch size与其它参量的关系以及分形动力学（有可能是multifractal） https://gemini.google.com/app/1244d3a05282f6ec https://gemini.google.com/app/13cef90729e5f64f https://gemini.google.com/app/5294c2f6902abf79 https://gemini.google.com/app/53cb521148354551

小模型会优先把有限神经元/表示维度分配给高频、低复杂度任务；罕见任务的梯度信号稀疏，常被其它更新覆盖。大模型容量更大，常见任务被学到后其梯度变弱，因而较不干扰罕见任务。[^26]

Johnson-Lindenstrauss引理说明神经网络随机初始化下的前向是近似保距的，当然，Saxe早就通过实验证明了多层串联会导致坍缩维度叠加，到后面就不等距了。如果考虑relu，那么充分宽神经网络会以高概率满足
$$ \left| \|\rho(Mx)-\rho(My)\|^2 - \left[ \frac12\|x-y\|^2 - \|x\|\|y\|\psi(x,y) \right] \right| \le\delta $$
其中$\psi(x,y) = \frac1\pi \left( \sin\theta-\theta\cos\theta \right), \theta=\angle(x,y)$，离得远的反而聚得更多[^35]。这其实很自然，因为如果两个向量是相反的，那么其中必有一者被完全压缩。

## Concepts

#todo
fisher information, Hessian, NTK, GGN关联与辨析，参考https://gemini.google.com/app/e6e9443b5f0f0005

实际上fisher就是梯度协方差

https://chatgpt.com/c/69eb72ca-afbc-83e8-9c99-0cc82a6459c8

## Ref

[^1]: [Scaling Laws for Neural Language Models](https://arxiv.org/abs/2001.08361)
[^2]: [Training Compute-Optimal Large Language Models](https://arxiv.org/abs/2203.15556)
[^3]: [Deep frequency principle towards understanding why deeper learning is faster](https://arxiv.org/abs/2007.14313)
[^4]: [Loss Surfaces, Mode Connectivity, and Fast Ensembling of DNNs](https://arxiv.org/abs/1802.10026)
[^5]: [Git Re-Basin: Merging Models modulo Permutation Symmetries](https://arxiv.org/abs/2209.04836)
[^6]: [Loss Patterns of Neural Networks](https://arxiv.org/abs/1910.03867)
[^7]: [Embedding Principle: a hierarchical structure of loss landscape of deep neural networks](https://arxiv.org/abs/2111.15527)
[^8]: [Optimistic Estimate Uncovers the Potential of Nonlinear Models](https://arxiv.org/abs/2307.08921)
[^9]: [Sometimes I am a Tree: Data Drives Unstable Hierarchical Generalization in LMs](https://arxiv.org/abs/2412.04619)
[^10]: [Which Layer is Learning Faster? A Systematic Exploration of Layer-wise Convergence Rate for Deep Neural Networks](https://openreview.net/forum?id=wlMDF1jQF86)
[^11]: [Deep frequency principle towards understanding why deeper learning is faster](https://arxiv.org/abs/2007.14313)
[^12]: [The Emergence of Spectral Universality in Deep Networks](https://arxiv.org/abs/1802.09979)
[^13]: [GaLore: Memory-Efficient LLM Training by Gradient Low-Rank Projection](https://arxiv.org/abs/2403.03507)
[^14]: [ReLoRA: High-Rank Training Through Low-Rank Updates](https://arxiv.org/abs/2307.05695)
[^15]: [Neuron-based Multifractal Analysis of Neuron Interaction Dynamics in Large Models](https://openreview.net/forum?id=nt8gBX58Kh)
[^16]: [Subliminal Learning: Language Models Transmit Behavioral Traits via Hidden Signals in Data](https://arxiv.org/abs/2507.14805)
[^17]: [SGD and Weight Decay Secretly Minimize the Rank of Your Neural Network](https://arxiv.org/abs/2206.05794)
[^18]: [Dyson Brownian motion and random matrix dynamics of weight matrices during learning](https://arxiv.org/abs/2411.13512)
[^19]: [Super Consistency of Neural Network Landscapes and Learning Rate Transfer](https://arxiv.org/abs/2402.17457)
[^20]: [MiLoRA: Harnessing Minor Singular Components for Parameter-Efficient LLM Finetuning](https://aclanthology.org/2025.naacl-long.248)
[^21]: [PiSSA: Principal Singular Values and Singular Vectors Adaptation of Large Language Models](https://arxiv.org/abs/2404.02948)
[^22]: [CorDA: Context-Oriented Decomposition Adaptation of Large Language Models](https://arxiv.org/abs/2406.05223v3)
[^23]: [Representation Costs of Linear Neural Networks: Analysis and Design](https://proceedings.neurips.cc/paper/2021/hash/e22cb9d6bbb4c290a94e4fff4d68a831-Abstract.html)
[^24]: [Jiaqi's phenomenon](https://www.zhihu.com/question/2017049686331127666/answer/2036149386116342692)
[^25]: [Spectral Scaling Laws in Language Models: How Effectively Do Feed-Forward Networks Use Their Latent Space?](https://arxiv.org/abs/2510.00537)
[^26]: [Why Larger Models Learn More: Effects of Capacity, Interference, and Rare-Task Retention](https://arxiv.org/abs/2605.29548)
[^27]: [Neural Thickets: Diverse Task Experts Are Dense Around Pretrained Weights](https://arxiv.org/abs/2603.12228)
[^28]: [Intrinsic Dimensionality Explains the Effectiveness of Language Model Fine-Tuning](https://arxiv.org/abs/2012.13255)
[^29]: [On the Expressive Power of Deep Neural Networks](https://arxiv.org/abs/1606.05336)
[^30]: [Training Robust Deep Neural Networks via Adversarial Noise Propagation](https://arxiv.org/abs/1909.09034)
[^31]: [Training Language Models via Neural Cellular Automata](https://arxiv.org/abs/2603.10055)
[^32]: [Reinforcement learning towards broadly and persistently beneficial models](https://alignment.openai.com/beneficial-rl)
[^33]: [When does RandOpt work?](https://kindxiaoming.github.io/blog/2026/randopt/)
[^34]: [Emergence of simple-cell receptive field properties by learning a sparse code for natural images](https://www.nature.com/articles/381607a0)
[^35]: [Comments on "Deep Neural Networks with Random Gaussian Weights: A Universal Classification Strategy?"](https://arxiv.org/abs/1901.02182)
