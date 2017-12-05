---
layout: post
title: Multi-task Sequence to Sequence Learning 
date: 2017-11-26
author: Kaiyuan Chen
catalog: true
tags:
    - Machine Learning
    - Paper Review
    - NLP
---

# Multi-task Sequence to Sequence Learning 
By sequence to sequence model, we have three basic settings 
* one-to-many settings 
* many-to-one setting
* many-to-many settings

for multi-task learning. 

### one-to-may
have one encoder in common, such as translation and parsing
and have multiple decoders 

for example, input is a sequence of English words, 
a separate decoder can generate translation in German,tags in parsing and same sequence of English words. 

### many to one
only one decoder is shared, such as image captioning 

### Many-to-many 
multiple input encoder <=> multiple output decoder 

### Unsupervised 
autoencoder helps less in terms of perplexities but more on BLEU scores compared to skip-thought.

### Datasets 
all of them are on machine translations 
