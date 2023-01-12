---
title: Summarization
categories: ["nlp"]
---

# Notes:
- Don't use dropout, you will be forcing the model to hallucinate.

## Dataset & Metrics

### xsum

|   | Rouge-1 | Rouge-2 | Rouge-L |
|---|---|---|---|
| SOTA (Narayan et al., 2021)   | 47.80 | 25.06 | 39.76 |
| Pegasus (Zhang et al., 2020)  | 47.21 | 24.56 | 39.25 |
| T5 base (Sascha et al., 2021) | 42.96 | 20.38 | 35.10 |
| T5 xxl  (Sascha et al., 2021) | 48.83 | 25.96 | 40.70 |
|---|---|---|---|


### CNN DailyMail

|   | Rouge-1 | Rouge-2 | Rouge-L |
|---|---|---|---|
|SOTA (Dou et al., 2020) | 45.94 | 22.32 | 42.48 |
|PEGASUS (Zhang et al., 2020) | 44.17 | 21.47 | 41.11 |
|T5 xxl (Raffel et al., 2019) | 43.52 | 21.55 | 40.69 |
|T5 base (Sascha et al., 2021) | 43.09 | 20.67 | 39.96 |
|T5 xxl (Sascha et al., 2021) | 45.32 | 22.60 | 42.17 |

### SAMSum

|   | Rouge-1 | Rouge-2 | Rouge-L |
|---|---|---|---|
| SOTA (Rohde et al., 2021) | 53.01 | 28.27 | 48.84 |
| T5 base (Sascha et al., 2021)   | 49.38 | 24.16 | 44.88 |
| T5 xxl (Sascha et al., 2021)    | 53.10 | 28.73 | 48.94 |
