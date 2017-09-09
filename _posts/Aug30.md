# Notes From Beginning(III)

## Neural Network 
### Representation 

* Neuron: computational unit 
* Dendrites: input
* axon: output 
* layers: hidden layer, input layer(layer 1), output layer 
* weights: \theta(parameters in \theta^Tx)
* activation function: logistic function that we used before
* bias unit a_0

As a result, the model looks like an input vector is passed into a neuron, then output a hypothesis function. 

[layer 1] -> [layer2] -> [layer 3]

#### Notations 
a_i^j activation of unit i in layer j
\Theta^j matrix of weights controlling function mapping from layer j to layer j+1

Then 
a_1^2 = g(\Theta^1_10 x0 + \Theta^1_11 x1 +\Theta^1_12 x2 +\Theta^1_13 x3 )

the dimension of \Theta is 
s_{j+1} * (s_j + 1)

#### Vector Representation 
**z**^j = **\Theta** ^{j-1} **a**{j-1}

#### Intuition 

[] -30
[] +20 -> []   g(-30 + 20 x_1 + 20 x_2) 
[] +20

grouping these neurons together and form more complex logic gates 

##### Multiclass classification 
having a vector(rather than a number) as output 
and output for object A should be [0, 0, 0, 1] rather than [1, 2, 3, 4]


### Learning 
#### Cost Function 
{training set (x^m, y^m)}
L: total number of layers
s_l: number of units in layer l

Binary classification: one output 0 or 1
Multi class classification: K classes where y \in \R^K

The cost function will be a generalized version of logistic regression
**by adding K component together** 

#### Back Propagation Algorithm 
\delta_j^l error of node j in layer l
\Delta_{ij}^l compute partial derivative of equation [1]
 
goal: minimize the cost function J

in a four-layered neural network
Forward propagation: 
a^1 = x 
z^2 = \Theta^1 a^1
a^2 = g(z^2)
z^3 = \Theta^2 a^2
...

Then back propagate: 
l = 4
\delta^4 = a^4_j - y_j
\delta^3 = (\Theta^3)^T\delta^4 .* g'(z^3)

**dJ/d\Theta_{ij}^l = a_j^l \delta_i^{l+1}** [1]

##### in Practice  
###### Unrolling parameters 
vector = [Theta1, Theta2, Theta3]
call reshape(vector(#range), size, size)

##### Gradient Checking 