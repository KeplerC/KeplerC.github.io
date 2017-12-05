---
layout: post
title: Unsupervised Neural Translation Machine Translation
date: 2017-11-30
author: Kaiyuan Chen
catalog: true
tags:
    - Machine Learning
    - Paper Review
    - NLP
---

# Unsupervised Neural Translation Machine Translation
Artetxe, Cho


Traditionally NMT requires large parallel corpus. This method relies on unsupervised cross-lingual embeddings. By a shared encoder for both translation encoder, the entire system is trained using monolingual data and reconstruct the input. 


### Keywords 
cross-lingual word embedding: TODO:next paper 
low resource neural machine translation: independently translation by a pivot language A->B->C to translate from A to C 

### Method 

two layer encoder & two layer decoder: only one encoder shared by both languages 
* dual structure: handle both directions together 
* shared encoder: This universal encoder is aimed to produce a language independent representation of the input text, which each decoder should then transform into its corresponding language
* fixed embedding: pre-trained


                decoder for its own language -> reconstruct the other lanuage
                
shared encoder ->into language independent embedding 

                (when inference, replace) decoder for the target language


#### denoising: 
optimizes the probability of encoding a noised version of the sentence with shared encoder and reconstruct using L1 encoder. It
exploit dual structure of machine translation. The shared encoder can reconstruct its own input.

#### backtranslation: 
Iit translates the sentence in inference mode(encoding with shared & decoding with L2) and optimizes with probability of encoding the probability of translated sentence with shared encoder and recovering the original setence with L1 encoder. 

### Thoughts 
This paper uses the method that we are familiar with, which reconstruct the input in unsupervised learning. It has two part that worthwhile considiering: 
* pre-trained embedding(which is key to my paper)
* a reconstruction that can translate from one to the other, in a totally unsupervised way. 

If we can construct the embedding of time series in some way, and this way might offer a way to train a generative model that does the way for us. 