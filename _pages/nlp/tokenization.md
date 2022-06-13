---
layout: single
published: false
title: Text Tokenization
categories: ["nlp"]
---

Deep learning models do not directly operate on text. They are trained using gradient optimization of loss where inputs and intermediates are all floating point numbers.

Then how do we process text? Through vocabularies and tokenization.

## Word Vocabularies
The most basic method used for training MLP models is to break the text into words and then create a vocabulary of top $$N$$ most frequent words. A $$N$$ x $$d$$ matrix of floats is then created where $$i_{th}$$ entry in this matrix is the representation for the $$i_{th}$$ word in the vocabulary. This matrix is generally pretrained on a large corpus so that we get a representation for every word so that they represent semantic relationships in the $$d$$ dimensional space.

Similarly, on some tasks, it might also make sense to include bigrams an trigrams in vocabularies.

### OOV words
An important thing to understand is how $$OOV$$ words are handled. These are words that are not present in the top $$N$$ words. A small number of buckets (at times even just 1) is chosen for $$OOV$$ words and a bucket is assigned using some hash function. So if there are $$N_{oov}$$ buckets, and $$H$$ is the hash function chosen, then the bucket for word w is $$H(w) \% N_{oov}$$.

## Tokenization
Since the above pattern can lead to pretty large vocabularies and still have a lot of $$OOV$$ terms, various techniques have been used to break words into smaller chunks that can even remove the need $$OOV$$ buckets since a word can be broken down into chars (or bytes) and each of these smallest units are in the vocabulary. [FastText](https://arxiv.org/abs/1607.04606) (Piotr Bojanowski et al., 2016) uses this for non-contextual word representation.

### Sentencepiece Tokenization
Most of the moderm NLP models (BERT, T5, GPT, and their family) use [sentencepiece tokenizer](https://github.com/google/sentencepiece) to create their vocabularies from large corpora. Over byte/char level models, these models have better throughput since they are able to reduce the input/output sequence length as the input/output sequence can be represented using smaller number of tokens.

### Byte Tokenization
Byte tokenizers just consider every byte in the input as a input token and their vocabulary is hence composed of just the 256 bytes (+ some special tokens). Though sentence piece tokenizers are better since they are able to represent the same input using smaller number of tokens, there are two important factors where byte tokenizers are better:
1. Tokenization using sentencepiece tokenizers is slow due to the way they break the text into tokens, but byte level tokenizers are extremely fast during both encoding and decoding phase. This can become very significant especially if you are dealing with small models which is a requirement in many production models.
2. Sentencepiece vocabulary needs some corpora for creation. So a sentencepiece vocabulary created for one corpora might not work that well for something else (though this is rarely a problem in practise).

_Related Papers_
- [Google's Word2vec](https://arxiv.org/abs/1301.3781) (Tomas Mikolov et al., 2013)
  - Approach #1: Continuous Bag of Word (CBOW) model
    - Find the target word given its context words.
    - Input is multi-hot context of words, and output is softmax over the same vocabulary.
    - There is one inner hidden layer which essentially represents the combined embedding for the input words, and the projection matrix becomes our per word lookup table.
  - Approach #2: Skip-gram model
    - Find context words given a word.
    - Input is one-hot representing the word, and output is softmax over the same vocabulary.
  - Heirarchical Softmax and Negative sampling needed for efficiently computing the loss function.
- [Stanford's Glove](https://nlp.stanford.edu/pubs/glove.pdf) (Jeffery Pennigton et al., 2014)
  - Frequently occurring co-words means just more training examples in Word2Vec.
  - Glove explicitly uses this co-occurrence distribution.
  - Not a neural trained model.
- [FastText](https://arxiv.org/abs/1607.04606) (Piotr Bojanowski et al., 2016)
  - Non contextualized representation similar to Word2Vec and GLove.
  - Operates on char and subword level, so does not have $$OOV$$ words.
  - Requires less training data, so has support for many more languages compared to the above two.
- [BERT](https://arxiv.org/abs/1810.04805) (Jacob Devlin et al., 2016)
  - Contextual word embeddings created using transformer stack.
  - The base for GPT, T5 and other similar family of models.
- [Charformer](https://arxiv.org/abs/2106.12672) (Yi Tay et al., 2021)
  - Uses byte vocabulary with GBST layer
  - GBST(Gradient Based Subword Tokenization) is used for reducing the sequence length.
  - GBST uses 1-D convolution followed by sub-block selection for the reduced sequence length.
- [ByT5](https://arxiv.org/abs/2105.13626) (Linting Xue et al., 2021)
  - Uses byte vocabulary.
  - Pretraining uses masking of ~20 tokens (vs ~3 tokens in sentencepiece)
  - Encoder is 3x deeper than decoder.
  - Slower than Charformer.
- [CANINE](https://arxiv.org/abs/2103.06874) (Jonathan H. Clark et al., 2021)
  - Same as ByT5, but adds downsampling to reduce sequence length.

  