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

## Query Generation
Query Generation works great for training the model on synthetic data with huge improvement in metrics.

## DSI
- Index document directly as parameters of the model.
- Original paper pretrained on chunks from the input document.
- Better strategy is to [generate queries for the document](https://arxiv.org/pdf/2206.10128.pdf) and finetune using the query set.
- Use Doc2Query for Query generation. Use random sampling instead of beam search for diversity.
- Semantic ids can be used where all documents are clustered into $k$ clusters. And then each cluster is further subcategorized into $k$ clusters if needed.
- When using Semantic string ids, it might be better to use ideas from [Neural Corpus Indexer](https://arxiv.org/pdf/2206.02743.pdf) paper's section 3.3 where they designed $$Prefix-aware weight-adaptive decoder$$. The main idea is that for doc ids 112, 121, 132, each of the two have different semantic meaning in their cluster's space and it might not be a good idea to use the same embedding/token in the vocabulary for all of them.
- Use constrained decoding to not generate bad documents.
- 

## Retrieval / Ranking Performances


| $$NQ_{320k}$$  |  Hits@1 | Hits@10 |
|----------------|---------|---------|
| NCI (T5 Base)  |  88.72  | 95.84   |
| DSI (T5 Base)  |  27.40  | 56.60   |
| DSI (T5 XXL)   |  40.40  | 70.30   |
|----------------|---------|---------|


| MSMarco passages | Hits@1 | Hits@10 |
|------------------|--------|---------|
|                  |        |         |
|------------------|--------|---------|
