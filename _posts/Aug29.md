# Notes From Beginning(II)

## Classification 
Classification is different from Regression such that it is not actually a linear function. It depends on small number of labeled discrete values. 

### Hypothesis Representation
To represent 0<h_\sigma(x) < 1, we can pass the equation \theta^T x into a **logistic function** g, such that h_theta(x) = g(\theta^Tx), where z = \theta^Tx, g(z) = \frac{1}{1+e^{-z}}
Then this Sigmoid Function can map any real number to [0,1]

##### Relation to probability
This h_\theta(x) gives the probability:
>h_\theta(x) = 0.7 gives that it has 0.7’s probability to output 1. 
h_\theta(x) represents the probability that outputs 1
### Decision Boundary
For discrete binary classification that output 0 and 1, 
h_theta > 0.5 -> y=1
h_theta < 0.5 -> y=0
Luckily, we have z = 0, to have g(z) = 0.5 and the rest is fixed for h_\theta(x). 

### Cost Function 
We cannot use the cost function in linear regression, 
then it is not a convex function, then J has many local maximum/minimums. 

cost = -log(h_\theta(x)) if y = 1  (1)
and  = -log(1-h_\theta(x)) if y = 0 (2)
then it can be convex and have a global max/min

#### Intuition 
Cost = 0: if y = 1 and h_\theta(x) = 1
while 
h_\theta(x) \rightarrow 0, then cost \rightarrow \inf 
    a large penalty cost

#### A simplified Cost Function 
Cost (h_theta(x), y) = -y (1) - (1-y) (2)
and we can do gradient descent based on that 

#### Multiclass Classification 
We can divide y = {0 ... n} problem into n+1 binary classification problems 

#### Reducing Overfitting Problem 
we can reduce the weight by adding some terms in J such that 
J = J + 1000 * \theta_3 + 1000 * \theta_4

### Regularization 
The specific equations can be found on the webpage. Because I cannot write equations here, using latex format is not quite reader friendly. 

#### Linear Regression 
It has two parts, unregularized \theta_0 and the rest and regularized the rest. We penalize each theta by a factor \lamda \ \m.  
The related normal equation can also do the same. 
It is a small number. 
