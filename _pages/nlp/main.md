---
title: ML on Text
layout: single
published: false
categories: ["nlp"]
---
# ML on Text

## Architectures
- BiDAF
- QANet
- Ruminating Reader
- BERT
- Open GPT
- MTDNN
- Word2Vec
    - 2 Approaches: CBOW and skip-gram used to train network.
- Glove
    - Focuses on co-occurance. The embedding essentially takes into occount co-occurance count of neighbors better than Word2Vec.
- FastText
    - Uses char n-grams to find embedding.
    - Better than Word2Vec for unseen words.
    - Can provide with embedding even if word was not seen in training corpus.

## Use Cases
### Language Modeling
### Question Answering 
### POS Tagging
### Sentence Embedding

- Deep Averaging Network: Average of embedding of every word + feed forward + classification head.
- Universal Sentence Encoder:
    - Model #1: Transformer based encoding + sum up from every word + classification head. (Slow as it is quadratic in length of sentence).
    - Model #2. average(Fixed Unigram & Bigram coding) + feed forward + classification head. (Fast as it is linear in length of sentence).

### Question Answering
- Dense Phrase Representation: https://arxiv.org/pdf/2012.12624.pdf
    
## Datasets
- https://github.com/niderhoff/nlp-datasets