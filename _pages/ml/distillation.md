---
layout: single
published: false
categories: ["ml2"]
---
# Distillation

## Teacher Student

$$L(x, y) = H((1-\alpha)y + \alpha P^T(x), P^S(x))$$

You may also use temperature. See [Self-Knowledge Distillation](https://arxiv.org/pdf/2006.12000.pdf).

## Self Distillation

$$L(x, y) = H((1-\alpha)y + \alpha P^S_{i \lt t}(x), P^S_{t}(x))$$
- [Self-Knowledge Distillation](https://arxiv.org/pdf/2006.12000.pdf)
