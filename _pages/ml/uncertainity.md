---
layout:single
categories: ["nlp"]
published: false
---

# Uncertainity estimation in prediction
- Can a model along with the prediction, provide a confidence measure?
- Some options are Baysian neural network, and ensembles (sample output from mutiple models to get variance).
- One option is to model it as variance in the output (predicted by the model per example) and add that in the loss function.
- Essentially, we want the model to output a distribution. Do $$y$$ gets replaced by $$\mu(y)$$, and in addition we are predicting $$\sigma(y)$$ assuming a gaussian distribution.

## Uncertainity prediction with MSE loss

## Uncertainity prediction with cross entropy loss


## Distance awareness from training examples
- [paper](https://proceedings.neurips.cc/paper/2020/file/543e83748234f7cbab21aa0ade66565f-Paper.pdf)
- Predict the distance from the training examples using RBF kernels on the output labels