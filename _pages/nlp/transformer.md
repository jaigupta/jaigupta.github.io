---
title: Transformers for Text
categories: ["nlp"]
---

## Attention is all you need
- https://towardsdatascience.com/attention-is-all-you-need-discovering-the-transformer-paper-73e5ff5e0634
- $$N$$ layers of Encoder to produce encoder_outputs.
- $$N$$ layers of Decoder with each of them taking the same encoder outputs (from final layer) for $$K$$ and $$V$$ in encoder-decoder attention.


- Three types of atttention:
    - Bidirectional self attention: Self attention in the encoder.
    - Causal attention: Self attention in the decoder to enforce looking at only the previous words.
    - Encoder-Decoder attention: Cross attention from the final encoder output to the decoder.


- In decoder, any operation across length should be carefully handled to not leak information. Hence:
    - Masking in attention
    - LayerNormalization only across the inner dimension
    - All linear layers are pointwise linear (1x1 kernel convolutions)


- Pros:
    - Operations across the length dimension are in parallel.
    - Thanks to no causal attention, all decoding for training time are done in parallel (even in autoregressive style). Hence, training is faster.

## Self-Attention with Relative Position Representations
- https://arxiv.org/pdf/1803.02155.pdf

# Models
- BERT: Encoder only
- GPT family: Decoder only
- T5: Encoder Decoder
- T5.1.1: Following improvements over T5
    - GEGLU activation in feed-forward hidden layer, rather than ReLU.
    - Dropout was turned off in pre-training (quality win). Dropout should be re-enabled during fine-tuning.
    - Pretraining on C4 (no mixing of downstream tasks).
    - No parameter sharing between embedding and classifier layer.
- MT5: Multilingual T5.1.1

## Nucleus Sampling
__https://arxiv.org/pdf/1904.09751.pdf__
- Normal generation samples from top-k top words of vocabulary ($$V'$$) at every step.
- Instead set a threshold probability $$p$$ ans sample from that. The size of $$V'$$ keeps varying.


## DeBERTa
- [DeBERTa](https://arxiv.org/pdf/2006.03654.pdf)
- Two novelities:
    - Disentangled attention: Each word has two representations (content and position).
    - Enhanced mask decoder.

## Funnel Transformer
- Most use cases just need a single output (not sequence), so a lot of wasted computation.
- Keep pooling in between to create a funnel. Reinvest the saved computation in increasing depth.
- https://arxiv.org/pdf/2006.03236.pdf

## mT5
- Large Multilingual T5: https://arxiv.org/pdf/2010.11934.pdf

