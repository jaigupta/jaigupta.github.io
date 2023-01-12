---
categories: ["nlp"]
published: false
---

# Text Editing models

## LaserTagger
- [paper](https://arxiv.org/abs/1909.01187)
- Create a fixed vocabulary of tokens that can be inserted.
- At every position, predict tags KEEP/DELETE, along with a token from the above vocab that can be inserted.

## Felix
- [paper](https://aclanthology.org/2020.findings-emnlp.111.pdf)
- sample efficient and fast inference time.
- Three steps:
  - *Encoding*: Encode sentence using BERT.
  - *Tagging*: A tagger uses encoder output and outputs tag for each token. target for cross entropy loss will be KEEP/INSERT/DELETE.
  - *Pointing*: Produce $\pi(i)$ in parallel for every token taking into input:
    1. encoder hidden state.
    2. embedding of output from tagging model $t_i$.
    3. positional embedding of $i_{th} token.
    - Scaled dot product attention between token of above output is used for pointer to next token $\pi(i)$.
  - The output of the pointing network when combined with the tagger is a text fragment that contains INSERT tags.
  - A separate bert model is used to assume the insert tags as masked tokens and predict them similar to the MLM task.

## EdiT5
- [paper](https://arxiv.org/abs/2205.12209)
- Encoder encodes the input tokens.
- tagger uses above encoding to predict KEEP/DELETE.
- pointer produces reordering amongst the tokens with keep.
- decoder predicts positions to insert (using special tokens, or just numbers?) and then the text to insert.