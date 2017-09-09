## Regression 
*K-fold cross-validation* randomly splits the training set into 10 distinct subsets called folds and train 9 folds and evaluate 1 fold. 

## Classification 
Classification using MNIST dataset 

### Dataset 
this can be downloaded through sk learn 
the dictionary structure has 
DESCR : discription
data : array  row:instance column:feature 
target : labels 

The previous parts of sections introduce classification accuracy: 
it has confusion matrix, which has a clean prediction(never see the data during training) on big fours 

I ran into problems (I haven't figure out why), it says training error, although I just changed a straight line code into a class based one

Then I ran a one-hundred fold cross value set evaluation 
the time took super long, because it has to train it one by one 
The result sticks to 95%
[ 0.96672213  0.93843594  0.91347754  0.90848586  0.96505824  0.95673877
  0.97171381  0.95174709  0.93843594  0.91846922  0.89351082  0.95507488
  0.91181364  0.95341098  0.93178037  0.95008319  0.91680532  0.96339434
  0.94675541  0.95174709  0.9484193   0.95        0.94666667  0.93
  0.92166667  0.965       0.96333333  0.96666667  0.95666667  0.95333333
  0.97333333  0.96333333  0.95833333  0.865       0.96333333  0.965
  0.96833333  0.94833333  0.96333333  0.89        0.89666667  0.91666667
  0.94        0.95833333  0.96        0.94333333  0.965       0.92166667
  0.96833333  0.95        0.965       0.97833333  0.96833333  0.97
  0.97166667  0.97666667  0.96833333  0.96166667  0.985       0.94666667
  0.95333333  0.95333333  0.96        0.97        0.95666667  0.96666667
  0.96333333  0.97333333  0.97833333  0.96333333  0.95833333  0.965
  0.95333333  0.96333333  0.95666667  0.965       0.96166667  0.97
  0.97166667  0.96327212  0.95492487  0.97328881  0.95993322  0.96160267
  0.96994992  0.96327212  0.95659432  0.96661102  0.95826377  0.97495826
  0.95659432  0.94657763  0.95492487  0.95993322  0.96661102  0.95492487
  0.96327212  0.96661102  0.95659432  0.95158598]

  ### Confusion matrix 
  confusion matrix: the general idea is to count the number of times instances of class A are classified as class B.

  Here we use 
  ```python 
from sklearn.model_selection import cross_val_predict
y_train_pred = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3)
```
to perform a N0fold cross validation. As noted, this is a clean prediction

With this number, we can evaluate, precision, recall, true positive and etc

for example, to evaluate F1 score: 
```python 
from sklearn.metrics import f1_score
f1_score(y_train_5, y_pred)
```
>To extend your life, you need to recall all 10 surprising events from your memory. So, recall is the ratio of a number of events you can correctly **recall** to a number of all correct events.
>precision is a measure of how many positive predictions were actual positive observations. It is that events you can correctly recall to a number all events you recall 
[Interesting explanation](https://www.quora.com/What-is-the-best-way-to-understand-the-terms-precision-and-recall)

### Choosing a threshold 
There is a tradeoff between precision and recall. The more recall(lower the threshold), the lower the precision is. 
```python 
y_scores = sgd_clf.decision_function([some_digit])
>>> array([ 161855.74572176])
>>> threshold = 0
y_some_digit_pred = **(y_scores > threshold)**
array([ True], dtype=bool)
```

I ran into the problem(as most of people did) about dimensionality

then I went to the issues on github and found 
one used 
y_scores = y_scores[:,1]
to reduce the dimensionality and solved it about the line 
```python 
y_scores = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3,
method="decision_function")
```
>I believe what's supposed to happen is that when SGDClassifier has 2 classes its decision function returns a single dimension arrray, but when there are greater than 2 classes it returns an ndarray where the first column signifies the class. In my instance 0 is supposed to be the binary false.
see in https://github.com/ageron/handson-ml/issues/81

After this problem, everything is normal 

**One way to compare classifiers is to measure the area under the curve (AUC). A perfect classifier will have a ROC AUC equal to 1, whereas a purely random classifier will have a ROC AUC equal to 0.5. **

### Multi-class classification 
OvO one vs one and do binary classification 
OvA one vs all(rest)

for N classes, algorithm needs to train N*(N-1) binary classifiers

#### Error Analysis 
as we have a confusion matrix, we can visualize by 
```python 
plt.matshow(conf_mx, cmap=plt.cm.gray)
plt.show()
```
Then we compute error rates by dividing number of images(like normalizing)

### KNN & Multi-label classification 
for multi output classification, like recognizing how many people on a photo, we can sue knn to solve that problem.