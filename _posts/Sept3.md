
## Anomaly detection 
We model p(x) and p(x_test) < \eps, then flag anomaly 

### Gaussian Distribution 
x ~ N(\mu, \standard deviation^2)

p(x) = 
p(x1; mu1, sq1) * p(x2; m2, sq2) ... = product of all p

Algorithm: 
1. choose features that you might think indicative 
2. fit parameters 
3. compute p(x)
the product(of two pdfs) is the result 


#### Developing and evaluating an anomaly detection system 
Assume we have some labelled data, of anomalous and non-anomalous examples, 
for training set, unlabeled and it's ok to let anomalous to slip in 
then use labelled set to test cross validation and test 

algorithm 
1. fit model p(x) on training set
1. predict on cross validation / test example 

evaluation metrics: big-four / precision, recall / F score 


#### Choosing features 
we use different features, like **different order, log** to make data distributed more Gaussian 
we choose feature that make usually large/small value in event of anomaly 

### Recommender System

#### Content-based Recommender system
use a vector to describe the degree of class(like romance, action)
we can treat every user as a linear regression problem 
to learn all users(all thetas)
just add a summation to all linear regressions 

#### Collaborative Filtering 
feature learning: 
when we have a series of theta for every users, we can infer the features (which are how romantic a movie is)

##### algorithm 
instead of switching between estimating x and estimating theta, we optimize a general equation such that 

J(x, theta) = 1/2 * sum(theta*x - y)^2 + regulation term of theta + regulation term of x 

1. initialize x and theta to small random values 
2. minimize using gradient descent 

#### low rank matrix factorization 
we can have a matrix that contain all the predictive rating for users/movies 
and we compute it as 
X * Theta'
>In mathematics, low-rank approximation is a minimization problem, in which the cost function measures the fit between a given matrix (the data) and an approximating matrix (the optimization variable), subject to a constraint that the approximating matrix has reduced rank. 

##### finding movies j related to i 
we use Euclidean distance 

##### Implementation Details 
If we do predictive matrix and collaborative filtering directly, for a new user without any information will minimize J by setting every parameter to 0.

To solve this problem, we use mean normalization. 
we subtract average rating of every matrix and learn theta and x through this new matrix. 