---
title: Ranking
categories: ["nlp"]
---

## Types of Models
### Representation based similarity
Generally used in production systems. Two tower approach where every document is indexed based on a representation and the queries have their own tower to calculate the representation. Final score is the similarity score. Examples are:
- DSSM
- SNRM

### Cross Attention: Query Document interation
Cross attention based where document tokens attend query tokens and vice versa. Expensive! Examples are:
- DRMM
- KNRM

### Full Cross Attention
All token in document and query attend every other token. Example: BERT, T5

### ColBERT (Late Interaction)
Two tower approach where we have a bit more complex function than a simple cosine similarity function. This is a tradeoff between latency and contextualization.

### BM25
TF IDF based extraction