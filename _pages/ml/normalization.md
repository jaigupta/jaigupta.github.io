# Normaliazation

All all the cases, we assume two types of inputs:
- $$T$$ for textual minibatch of shape [batch_size, seq_length, dim]
- $$I$$ for image minibatch of shape [batch_size, h, w, dim]
- $$X$$ is used when talking about them in common.

## Batch normalization
- Take mean($$\mu$$) and variance($$\sigma$$) reducing across only batch dimension.
- $$X = \gamma \frac{(X - \mu)}{\sigma} + \beta$$ where $$\gamma$$ and $$\beta$$ are learned parameters.

**Cons**
- Not useful if batch size is small which is very common.

## Layer Normalization
- Take mean($$\mu$$) and variance($$\sigma$$) reducing across only feature dimension (dim)
- $$X = \gamma \frac{(X - \mu)}{\sigma} + \beta$$ where $$\gamma$$ and $$\beta$$ are learned parameters.
