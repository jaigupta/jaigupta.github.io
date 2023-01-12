---
layout: single
published: false
title: Efficient Transformers
categories: ["nlp"]
---

Improving the efficiency of transformers, especially for processing long sequences is a hot area of research. The main papers focus on various sparse attention attention techniques, but there are four important facets that we will look at papers for.

![Transformer architectures](https://d3i71xaburhd42.cloudfront.net/baed71eed57ad462f3ab138d4b1700a738cd5414/3-Figure1-1.png)

### Sparse Attention
Limits the set of tokens each token attends to.
- [Sparse Transformer](https://arxiv.org/abs/1904.10509) (Rewon Child et al., 2019) attended to image pixels only in the same row and column. For text, this would mean local attention along with strided attention. This reduces the complexity to $$\mathcal{O}(n\sqrt{n})$$
- [Adaptive Attention Span in Transformer](https://arxiv.org/abs/1905.07799) (Sainbayar Sukhbaatar et al., 2019) - Learn the attention span of tokens for every layer and for every head. This span is a decaying function of distance. They also experiment with dynamically choosing the attention span based on the input.
- [Reformer](https://arxiv.org/abs/2001.04451) (Kitaev el al., 2020)
  - Locality sensitive hashing to find the nearest neighbors of query and perform attention only with them. $$\mathcal{O}(n\log{n})$$ attention cost.
  - Reversible layers to skip storing output of attention values and save memory.
      - Based on [RevNet](https://arxiv.org/abs/1707.04585)
      - $$(x_1, x_1) \rightarrow (y_1, y_2)$$
      - $$Y_1 = X_1 + Attention(X_2)$$ and $$Y_2 = X_2 + FeedForward(Y_1)$$
      - Backprop: $$X_2 = Y_2 - FeedForward(Y_1)$$ and $$X_1 = Y_1 - Attention(X_2)$$
      - There is some computational overhead due for figuring out the inputs (~33-50%), but memory usage is reduced.
- [Linformer: Self-Attention with Linear Complexity](https://arxiv.org/abs/2006.04768) (Sinong Wang et al., 2020)
  - Attention matrices are low rank.
  - Project $$QK^T$$ to a lower rank.
  - $$softmax(\frac{QK^TE}{\sqrt(d)}) (FV)$$. Here $$E$$ and $$F$$ are $$R^{lk}$$ and $$R^{kl}$$ matrices.
- [Rethinking Attention with Performers](https://arxiv.org/abs/2009.14794) (Krzysztof Choromanski et al., 2020)
  - Proposes Generalized Self Attention for a linear way to approximate similarity kernels $$K(x, y)$$ given that they can be approximated using random features.
  - [Random Features for Large-Scale Kernel Methods](https://people.eecs.berkeley.edu/~brecht/papers/07.rah.rec.nips.pdf)
- [Routing Transformer](https://arxiv.org/abs/2003.05997) (Aurko Roy et al., 2020) - Similar to Reformer, but cluster query and keys using $$K$$-means and then queries only attend to  keys in the same cluster reducing complexity to $$\mathcal{O}(n\sqrt{n})$$.
- [LongFormer](https://arxiv.org/pdf/2004.05150.pdf) (Iz Beltagy et al., 2020)
  - Uses dilated sliding window  with smaller window sizes in the start but larger later given attention is very local in lower layers.
  - Training is also done in 5 phases where sequence length and attention window size increase after each phase. So training is faster at the start. Goes from sequence length of 2048 to 23,040 on the last phase.
- [ETC (Extended Transformer construction)](https://arxiv.org/pdf/2004.08483.pdf) (Joshua Ainslie et al., 2020)
  - Global + Local Attention along with relative position encoding.
  - 2 separate attentions(local to local+global and global to local+global) with separate projection matrices.
  - Improved performance for structured inputs as well.
  - Contrastive Predictive Coding (CPC) as pretraining task that encourages the global tokens to represent summaries.
  - Global tokens are task specific (like one for every sentence).
- [BigBird](https://arxiv.org/pdf/2007.14062.pdf) (Manzil Zaheer et al., 2021)
  - Random attention apart from the local and global attention in ETC.
  ![BigBird attention](https://production-media.paperswithcode.com/methods/Screen_Shot_2021-08-05_at_12.00.02_PM.png)
- [Long T5](https://arxiv.org/pdf/2112.07916.pdf) (Mandy Gua et al., 2022)
  - Makes the definition of global tokens in ETC more flexible with just groups of tokens.
  - Global tokens are constructed by averaging the block tokens (Transient Global Attention) and discarded after attention.
  - Pretraining is borrowed from Pegasus.
  - Pegasus pretraining is tailored for summarization tasks by removing important sentences from the input and asking the model to generate them.

### Recurrence
- [Transformer-XL](https://arxiv.org/abs/1901.02860) (Zihang Dai et al., 2019)
  - Combine RNN like recurrence along with transformer style attention on blocks of inputs.
  - Cache each layer output from previous segment and concatenate it in current segment's corresponding layer's attention.

### Hierarchical
- [HIBERT](https://arxiv.org/abs/1905.06566) (Zhang et al., 2019) - Short for hierarchical BERT, it processes smaller chunks and then combines per chunk embedding to process the complete input.

### Compressed Attention
- [BP-Transformer](https://arxiv.org/abs/1911.04070) (Zihao et al., 2019) - Create binary partitioning tree over inputs and only tokens nearby and parents can be attended.
- [Memory Compressed Attention](https://arxiv.org/pdf/1801.10198.pdf) (Liu et al., 2018) - Reduce sequence length using strided convolution during attention.
- [Star Transformer](https://arxiv.org/abs/1902.09113) (Guo et al., 2019) - Each token attends its immediate left/right tokens and a global token.
- [Compressive Transformer](https://arxiv.org/abs/1911.05507) (Rae et al., 2019) - Combines Star transformer into Transformer-XL compressing inputs that are far away.