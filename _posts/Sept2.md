# Notes From Beginning(VI)
## Unsupervised Learning 
supervised learning: given a set of label and find a hypothesis, like {x^n, y^n}
but unsupervised learning is just {x^n}

### K-means algorithm 
1. random initialize K cluster centroids 
2. assign every points to K cluster
    1. take the min ||x^i - \mu_k||
3. move cluster to the new centroid  
    1. 1/n * [all the n vectors ]

#### Optimization objective 
To minimize the square distance between data point to centroid 
for the first step, minimize J w.r.t clusters 
for the second step, minimize J w.r.t mu 

#### Random Initialization 
K < m 
randomly pick K training examples,
set mu_1 ... mu_k equal to these K examples 

K means can end up with different solutions 
so we try to use K means multiple times and pick clustering that gave lowest cost 

#### choosing number of clusters 
* elbow method: cost decrease from rapidly to more slowly 

### PCA
#### Motivation for dimensionality reduction 
##### Data compression 
project high dimension to low dimension 
speed up, reduce memory
##### Data Visualization 
the axis usually be meaningless 

#### algorithm formulation 
Generally speaking it is to find a low dimensional structure that has smallest distance.Then we use a coordinate on that dimension to describe the original data set. 
It is not linear regression. 

we compute by covariance matrix 
\Sigma = 1/m \Sigma_i x^i * x^i ^T
computing **Singular Value Decomposition**
eigenvector 
[U, S, V] = svd(Sigma)

if we want to reduce it to n dimensions to k dimensions, 
just take the first k vectors of U

U_{reduce} is a n * k matrix 
when we take the transpose and take new coordinates by z = U_r * x 

###### Mean normalization and feature scaling can be applied 

###### Reconstruction
x_approx = U_reduce * z 
            u * k    k*1
            n * 1

###### choosing k 
choose the smallest value that 
average square of error / average square x <= 0.01(99% of variance is retained)

in USV, the S matrix is diagonal matrix that, calculating above value is 
1 - \frac{\sum^**k** Sii}{\sum^**n** Sii}

##### supervised learning speedup
For supervised learning， 
we extract all the x as input vector, then we apply PCA and reduce dimension
with this dimension's value, we have a new and much lower dimension's training set
Finding a mapping from x -> z 
Mapping should be defined only on training set, and then be applied to cross validation and test sets. 

* compression
    * reduce space 
    * speed up
* visualization 

bad use: use it to avoid overfit, it might throw away valuable information(the rest 1%)