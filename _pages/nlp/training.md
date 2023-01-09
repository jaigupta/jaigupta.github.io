---
layout: single
published: false
title: Training and Finetuning LLMs
categories: ["nlp"]
---

Below are some default settings used for pretraining/finetuning LLMs.

## Pre-Training
- Adafactor Optimizer ($$lr$$ = 1)
- Dropout=0
- For en C4's span corruption task, use sequence length of input=512, target=114 for T5 base model.


## Finetuning
- Adafactor Optimizer ($$lr$$ = 1e-3)
- Dropout=0.1 for generation tasks or even 0 if there hallucination turns out to be problem, 0.3 for others.