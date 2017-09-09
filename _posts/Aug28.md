# Notes From Beginning(I)
## Introduction

#### Supervised Learning and Unsupervised Learning 
* Supervised Learning: know what results should look like 
* Unsupervised Learning: have no idea 

#### Classification and Regression 
* Regression: predict results within a **continuous** output 
* Classification: predict in **discrete** output 

#### Model Representation
Training set is represented by (x^i, y^i) where i \in [1,m] and m is the number of training examples.

#### Cost Function 
The cost function is an average difference of all the results of the hypothesis with inputs from x's with actual output of y's. 

#### Multiple Features
x^i_j the value of feature j in the ith training example 
where hypothesis is 
h_theta(x) = \theta_0 + \theta_1 x_1 ... +\theta_n x_n
or written as matrix multiplication form

#### Overfitting 
adding extra features might be overfitting, while adding little will be underfitting. 

##### Solution 
* Reducing number of features 
* Regularization
    * keep all feature but reduce magnitude 

## Gradient Descent 
To estimate parameters of hypothesis function, we can use Gradient Descent. For two-dimensional case, points on the same contour on the contour map will have same loss cost. Thus, finding the equation with smallest loss cost is the same as finding the minimum value on the contour map. 

One assumption for this algorithm is that depending on where one starts on the graph, one could end up at different points. We start from some \theta_0, \theta_1 and iteratively repeat j=0 and j=1 until convergence

\theta_j \leftarrow \theta_j - \alpha \pd J(\theta_0, \theta_1)
 
to find the minimum J(\theta_0, \theta_1) where \alpha represents learning rate(step taken) and we calculate partial derivatives by h_theta - y^i 

#### Intuition 
\theta_1 \leftarrow \theta_1 - \alpha \pd J(\theta_1)
* positive slope: \pd is positive, then minus number to make \theta_1 go backward 
* vise versa

if \alpha is small, then gradient descent is slow;
if \alpha is too large, it may overshoot the minimum and fail to converge
if the derivative is approaching minimum, the pd is small thus the step taken is also small 

#### Batch Gradient Descent 
>Each step of gradient descent uses all the training examples.

### Gradient Descent for Multiple Variables 
Repeat Gradient Descent equation for n features. 

Because all the parameters \theta will descent more quickly on small ranges(they are all based on a ratio), we can keep them in a range. Also, there are two techniques:

#### Feature Scaling 
dividing the input values by the range(max-min) thus resulting the new range in 1.  
#### Mean Normalization 
subtracting the average value 

These are very common in statistics. 

#### Polynomial Regression 
We can combine the features by adding another feature to be quadratic, cubic or square root. Just need to keep in mind the range will be amplified for high order equations. 

### Normal Equation 
Another way of minimizing cost function J is by normal equation. By this way, we do not need to iterate or do feature scaling. 
The equation is 

\theta = (X^T X)^{-1} X^T y
The complexity of Normal Equation is O(n^3), due to the need for inverse the matrix, while the iterative method is O(kn^2)

#### Noninvertibility 
Common issue for nonivertible is 
* Redundant features 
* too many features 