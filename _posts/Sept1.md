# Notes From Beginning(V)
## Support Vector Machine(SVM)
### Optimization Objective 
Alternative view of logistic regression: 
if y=1, we want h(x) = 1, which \theta*x >>0
The cost function for y=1 is -log(1/1+e^-z)
    we can simplify the curve by two lines and make them function cost_1(theta*.x) and cost_0
then the support vector machine is 

min_\theta (1/m) \sum {y*cost_1 + (1-y) cost_0} + regularization term 
we can omit 1/m because it does not influence result 

and a readjustment to regularization term to 
min_\theta (1/m) **C*** \sum {y*cost_1 + (1-y) cost_0} + regularization term

C = 1\lambda

for the appendix term theta^2 
we use theta^T theta 

### Intuition: large margin intuition 
Because of the boundary we draw, we cannot use the results 
-\eps < 0 < \eps and we want to judge the result beyond this range 
then the C * 0 = 0

if C is large, then it will be greatly influenced by outliers 
As a result, there is a tradeoff between bias and variance 
C(small lambda)   large       low bias, high variance
                  small       high bias, low variance 
variance          large       high bias, low variance: features will vary smoothly

#### mathematics behind 
we convert theta*x to a dot product such taht 
p * ||theta|| > 1 if y = 1 
p * ||theta|| <= -1 if y = 1 
to minimize ||theta|| 
we need to maximize the projection p of x into vector theta

### Kernel
a complex equation(like high order equation) will be computationally expensive, so we use the proximity of landmarks 
which similarity function is called kernel, 
k(x, l^i)
i is the ith landmark 
which is computed by Gaussian kernel 
k = exp(- Euclidean distance/ 2*variance^2)

#### Where do we get landmarks 
we use every training example as landmarks 
and have m similarity functions. 
Then for every x, we generate a **feature vector** that 
contains m's similarity components of these similarity equations 

then we no longer use polynomials theta^T x but feature vector f^Tx

### In practice 
#### specifics
one need to specify
    choice of parameters C 
    choice of kernel(similarity function)
        no kernel == linear kernel when y=1 if theta^T >= 0
        Gaussian Kernel, then need to choose variance 
            do not make feature scaling on it(metric different)
        Mercer's theorem

#### multi-class classification
Use existing or one-vs-all

#### Choosing between logistic regression and SVM
when n is large: use logistic or SVM without kernel 
if n is small m is intermediate, use SVM is Gaussian kernel 
    (when m is 10-10 000)
if n is small m is large, add more features or use both