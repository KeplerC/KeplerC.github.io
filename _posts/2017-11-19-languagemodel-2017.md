---
layout: post
title: Machine Translation and Language model
date: 2017-11-19
author: KC
catalog: true
tags:
    - Machine Learning
    - Study Notes
    - NLP
---

# Machine Translation and Language model
Encoder-decoder scheme does not encode a whole input into a fixed vector, but encode input sentence into a sequence of vectors and chooses these vector adaptively while decoding translation. 

	• Language model with N-grams 
		○ assign a probability to a sentence 
		○ chain rule 
			§ the order of the word matters 
			§ have start of sentence and EOS
		○ do with log 
			§ because addition is faster than multiplciation 
		○ evaluation 
			§ extrinsic 
				□ external tasks 
				□ accuracy 
				□ perplexity 
					® reduce size (like huffman
					® inverse probability of the test set, normalized
					by the number of words.
					® weighted average branching factor of a language. The branching factor of a language is the number of possible next words that can follow any word.
					® cannot compare between different corpus
		○ Unknown words 
			§ if occureence is 0, we cannot calculate perplexity
			§ out of dictionary 
			§ smoothing
				□ laplace 
					® adjust count by +1 
			§ interpolation 
			§ absolute discount 
			§ kneser-ney algorithm
				look at a held-out corpus and just see what the count is for all those bigrams that had count 4 in the training set.
				
				
				
	• NN based LM
		○ neural probabilistic language model
			§ limitation of Ngram model
			§ continuous space language
		○ LSTM
			§ RNN
			§ variants: Cho
				□ tanh: normalization
	• character word(CW)
		○ require training to optimize infrequent word
		○ word embedding matrix * word 
	• regularzing / optimizing 
		○ non-monotonically triggered Averaged Stocahstic GD
			§ see the loss/perplexity start to drop 
LSTM + cache pointer 