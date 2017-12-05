---
layout: post
title: A study of Backpropagation 
date: 2017-8-25
author: Kaiyuan Chen
catalog: true
tags:
    - Machine Learning

---

# A study of Backpropagation 
As usual, the definition of backpropagation algorithm on wikipedia is 
>Backpropagation is a method used in artificial neural networks(ANN) to calculate the error contribution of each neuron after a batch of data (in image recognition, multiple images) is processed.

### Artificial Neural Network 
To explain ANN, it is a multilayered neural network under supervised learning and find best maps of a set of input to their correct output. 

### Loss Function 
It is just like reconstruction error, or cost function, that calculates the network output and expected output. 

>The input vector is propagated forward through the network, layer by layer, until it reaches the output layer. The output of the network is then compared to the desired output using loss function. The resulting error value is calculated for each of the neuron in the output layer. 

### Contribution of each neuron
This algorithm has two phases: propagation and weight update. 

#### Propagation
This step is to calculate a loss function and use error values to calculate gradient of loss function. 

#### Weight Update
Known the gradient of loss function, the algorithm updates weights to minimize it. 

#### Hadamard project 
It is a binary operation looks like a ⊙ b. It is element-wise or entry-wise operation, which can take place in two m*n matrices. 

## Intuition 
Backpropagation is to calculate partial derivative of cost function w.r.t weight or w.r.t bias. The idea for backpropagation is that if one can minimize the cost function by moving the weight/bias to the opposite sign of the cost function's derivative. Backpropagation offers a way to compute the loss function's partial derivative of each neurons. 

## Equations 
The equations for backpropagation are presented in [1](http://neuralnetworksanddeeplearning.com/chap2.html)
Inserting equations here seems to be complicated. 

But I will still present a pseudo code similar to Professor Andrew Ng: 

For each pair{x, y} in training set:

    1. set a(1) = x
    2. perform forward propagation to compute activation level a in level 2-L, where L is the total number of layers 
    3. using difference of a(L) and y to compute loss function
    4. compute backward 
    5. update weight by accumulating partial derivatives


## References 
https://mattmazur.com/2015/03/17/a-step-by-step-backpropagation-example/

http://neuralnetworksanddeeplearning.com/chap2.html

Backpropagation algorithm, Backpropagation intuition Andrew Ng, coursera.org 

Wikipedia 