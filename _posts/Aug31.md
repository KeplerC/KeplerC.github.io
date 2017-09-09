# Notes From Beginning(IV)
## Applying Machine Learning Algorithm 
There are a few practical approaches to 
* Getting more training examples: Fixes high variance
* Trying smaller sets of features: Fixes high variance
* Adding features: Fixes high bias
* Adding polynomial features: Fixes high bias
* Decreasing λ: Fixes high bias
* Increasing λ: Fixes high variance.

### Evaluating a hypothesis 
We can divide data into a training set and a test set and a **cross validation set**.
The procedure is:
1.	Learn \Theta and minimize J_{train} (Theta)
2.	Compute the test set error J_{test}(Theta)
The cross validation set is to avoid overfit. 

### Bias and Variance 
* The training error will decrease as we increase the degree of polynomial
* high bias is underfitting both J_{train} and J_{CV} will be high, and J is similar 
* high variance is overfitting. J_{train} will be low and J_{CV} is much higher

Diagnosing Neural Networks
* A neural network with fewer parameters is prone to underfitting. It is also computationally cheaper.
* A large neural network with more parameters is prone to overfitting. It is also computationally expensive. In this case you can use regularization (increase λ) to address the overfitting.
Using a single hidden layer is a good starting default. You can train your neural network on a number of hidden layers using your cross validation set. You can then select the one that performs best. 
Model Complexity Effects:
* Lower-order polynomials (low model complexity) have high bias and low variance. In this case, the model fits poorly consistently.
* Higher-order polynomials (high model complexity) fit the training data extremely well and the test data extremely poorly. These have low bias on the training data, but very high variance.
* In reality, we would want to choose a model somewhere in between, that can generalize well but also fits the data reasonably well.

### Machine Learning System Design 
To strategize to design a system, we need to choose features of the email(e.g. a vector of words)
1. start a simple algorithm 
2. plot learning curve to see more data/feature 
3. error analysis 

#### Error Analysis 
Consider what type of training set, then how to add features to classify them correctly
Also, we need numerical evaluation metric(like cross validation error) to determine the algorithm's performance 

* skewed classes: we have a lot more examples from one class than the other
    * for example: one have cancer's chance is 0.05%, so just predict 0!


##### Precision/Recall

| Index         | Actual Class True 1                     | Actual Class False 0 |
| ------------- |:------------------------------------: | ----------:|
| Predicted Class 1             | True positive    | False Positive|
| Predicted Class 0             | False Negative  | True negative    |

If the prediction is correct, then true
If algorithm predicts positive, then positive

>Precision = True positive / # predicted positive
>when we predict y = 1, how many actually have y = 1
>
>Recall = True positive / # actual trues  
how many have y=1 in all samples

##### Trading precision and recall 
We adjust threshold higher to reach high precision and lower recall. 
For example, we want to tell patients they have cancer when they really do. Thus, we lift the threshold. 
If we want to avoid false negatives, we need to get alarmed by setting a lower threshold, and have high recall & low precision. 

**F score**: 2 * RP/(R+P)

##### How many data do we need
large data rationale: assume feature has sufficient information to predict (if the feature is not enough, then the algorithm cannot get it)
    then many parameters, many hidden units 
    then J_train will be super small (low bias)
very large training set: unlikely to overfit (lower variance)