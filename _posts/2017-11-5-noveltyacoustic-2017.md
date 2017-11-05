---
layout: post
title: A novel approach for automatic acoustic novelty detection using a denoising autoencoder with bidirectional LSTM neural networks 
date: 2017-11-5
author: KC
catalog: true

---

# A NOVEL APPROACH FOR AUTOMATIC ACOUSTIC NOVELTY DETECTION USING A DENOISING AUTOENCODER WITH BIDIRECTIONAL LSTM NEURAL NETWORKS

This paper introduces unsupervised approaches for acoustic novelty detection. It relies on auditory spectral features (ASF), denoising auto encoder and BSTM RNN to detect novelty events and calculate reconstruction error of the sound. 

I would say this is a conventional reconstruction method in novelty detection. However, it is quite interesting because its implementation on sound. 

### keywords 
autoencoer: NN that consists only one hidden layer
compression encoder: learn a compressed version and extract useful features 
denoising auto encoder: reconstruct the sound 
bidirectional RNN: at each time-step, t, this network maintains two hidden layers, one for the left-to-right propagation and another for the rightto-left propagation.(thus cannot be used online)

### thoughts 
novelty detection of sound: dimension is relatively low, thus can use low dimensional structures, like this autoencoder model. 

Dataset on novelty detection of voice
> PASCAL CHiME: consists of a typical in-home scenario (a living room), recorded during different days and times, while the inhabitants (two adults and two children) per- form common actions, such as talking, watching television, playing, eating. 