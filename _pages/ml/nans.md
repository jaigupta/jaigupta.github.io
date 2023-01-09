---
layout: single
published: false
categories: ["ml2"]
---

# Nans in training

## Causes of loss ending up with nan.
### undefined losses for some values
- For example, using l2 norm on a variables that can be 0 due to padding. grad of $$\sqrt(x)$$ is nan at 0.


### nans that should be masked out
- suppose a loss is inf/nan for some portion of the input but you take care of masking it before summation. This is still problematic.