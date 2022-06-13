---
layout: single
published: false
categories: ["ml2"]
---
# ML Model Architectures

## Squeeze Net

## Attention Augmented Convolutional Networks
Paper link: [https://arxiv.org/pdf/1904.09925.pdf](https://arxiv.org/pdf/1904.09925.pdf)

- Given an input tensor of shape $$(H, W, F_{in})$$, we flatten it to a matrix $$X \in R^{HW×F_{in}}$$ and perform multihead attention as proposed in the Transformer architecture. The
output of the self-attention mechanism for a single head $$h$$ can be formulated as:

$$O_h = Softmax\left(\frac{(XW_q)(XW_k)^T}{\sqrt{d_k^h}}\right)(XW_v)$$

- The outputs of all heads are then concatenated and projected again.

$$MHA(X) = Concat[O_1, O_2, ..., O_{Nh}]W^o$$

- Use two-dimensional relative positional embedding as sin-cos one does not work well.
- Final output is concatenation of Conv and MHA

$$AAConv(X) = Concat[Conv(X), MHA(X)]$$