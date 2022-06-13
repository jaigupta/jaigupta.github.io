---
categories: ["nlp"]
---

Given that the attention component of Transformers is really expensive to evaluate due to their $$\mathcal{O}(l^2d)$$ complexity, this is yet another attempt to make it faster.

The methodology used here is to break down the softmax(K, V) into the dot product of two separate functions (kernel function). The function here are random cosine features of K and V.

> TODO: Add more math detail here.

This reduces the complexity to $$O(lD^2)$$, but the result is approximate. Here $$D$$ denotes the number of random features and is of almost the same order as $$d$$. D can be increased or decreased. Increasing it will reduce the error in approximation. Decreasing it will reduce the latency.