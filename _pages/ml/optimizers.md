---
layout: single
published: false
categories: ["ml2"]
---
# Optimizers

## Adam
Store first and second moment for all variables.

<img src="adam_algo.png" width="350" />

## Adafactor
We cannot have O(n) space complexity for just storing the params of the optimizers. Adam stores first and second moment of every variable.

Let $$V_{n*m}$$ be a variable, then Adafactor proposes to use just $$O(n+m)$$ space by:
- Get rid of first moment (set $$\beta_1 = 0$$).
- Storing the second momemnt in factored form such that $$V_{ij} = [RS^T]_{ij}$$, where $$R$$ and $$S$$ are column matrices.

<img src="adafactor_algo.png" width="350" />

#### Reference
- [Adafactor: Adaptive Learning Rates with Sublinear Memory Cost](https://arxiv.org/pdf/1804.04235.pdf)
