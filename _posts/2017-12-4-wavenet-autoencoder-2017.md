---
layout: post
title: Neural Audio Synthesis of Musical Notes with WaveNet Autoencoders
date: 2017-12-4
author: KC
catalog: true
tags:
    - Machine Learning
    - Paper Review
---

# Neural Audio Synthesis of Musical Notes with WaveNet Autoencoders
Engel et al.

### Contributions 
WaveNet-style autoencoder model that conditions an autoregressive decoder on temporal codes learned from the raw audio waveform.
Nsync: a large-scale dataset for exploring neural audio synthesis of musical notes.

### Autoencoder 
this is the only thing that we really care about here. 

The encoder produces an embedding with Z=f(x) from raw audio waveform. Then we shift the same input and feed it into the decoder, which reproduce the waveform. 

Downsampling in the encoder occurs only in the average pooling layer. The embeddings are distributed in time and upsampled with nearest
neighbor interpolation to the original resolution before biasing each layer of the decoder.

During inference, the decoder autoregressively generates a single output sample at a time conditioned on an embedding and a starting palette of zeros

https://github.com/tensorflow/magenta/blob/master/magenta/models/nsynth/wavenet/h512_bo16.py

#### Baseline: Spectral Autoencoder
The baseline convolutional autoencoder: it forces a compressed representation on entire note. 

### which is good
they give source code for base line and autoencoder's code.
