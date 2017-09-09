### Large scale machine learning 

Larger training set will have better results, which can be shown from learning curve. 

Problem with gradient descent: 
    for every iteration, it has to sum up 10000000... numbers (batch gradient descent: iterate through the whole data set)

#### stochastic gradient descent
we do only cost on one hypothesis and calculate J by average
randomly shuffle dataset(then the order will be fine)
repeat{
    for i=1...m{
        theta_j = theta_j - alpha (h - y).x
    }
}
General idea: we do first training example to fit first example a little bit better, and then the second example and make the second example a little better

batch will go from one point the move to the center of level curve
but stochastic will go zigzag; we decrease learning rate over time 
to make it converge

##### convergence 
we can plot e.g.1000 iterations and taking average
(because another new example might be better or worse)

#### mini-batch gradient descent 
batch gradient descent: use m example every iteration
stochastic: use 1 example every iteration 
mini-batch: use b examples, where b is user-defined
    vectorization can be more efficient than others

#### Online Learning
Repeat forever{
    get (x, y) online 
    update theta using (x,y)
}
it can adapt the preference of users 


#### Map Reduce and data parallelism 
split training set into different pieces and doing batch gradient descent separately and combine the results 



### OCR

Photo Character Recognition Pipeline
* Text detection
* character segmentation
* character classification 

#### Sliding window
taking a rectangular patch throughout the image
need to define step size and then take larger/smaller image patch 

For text detection, 
use a classifier to find where text has highest probability 
then use expansion method to determine the sliding window of the image

then we use a 1D sliding window to go through image patch to find gaps: character segmentation 

#### Application 
##### artificial data synthesis 
we produce a letter in different background and have different picture as synthetic data

##### Introducing distortions 
we can distort the training set to create more 
another application is speech recognition, also have a lot of noisy background 

however, having same value again and again will result a same theta

Discussion
* make sure to have a low bias classifier 
* "how much work would it be to get 10x as much data as we currently have" 


##### ceiling analysis 
the earlier the stage it is, the more influencial the stage is. 
i.e.
the ceiling the the next stage is determined by the previous stage

