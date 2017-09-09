
## Decision Trees
we can train a decision tree by 
```python 
from sklearn.datasets import load_iris
from sklearn.tree import DecisionTreeClassifier
iris = load_iris()
X = iris.data[:, 2:] # petal length and width
y = iris.target
tree_clf = DecisionTreeClassifier(max_depth=2)
tree_clf.fit(X, y)
```
and visualize by 
```python 
from sklearn.tree import export_graphviz
export_graphviz(
tree_clf,
out_file=image_path("iris_tree.dot"),
feature_names=iris.feature_names[2:],
class_names=iris.target_names,
rounded=True,
filled=True
)
```
dot -Tpng iris_tree.dot -o iris_tree.png

The prediction of decision tree is basically like binary tree. Based on root node decide on which branch to go. 

* sample: how many training instances it applies to 
* value: how many training instances of each class has node applies to 
* gini: impurities of a node; gini =0 -> all training instances apply to same class

```python
tree_clf.predict_proba([5,1.5])
```

Then for a single node, we evaluate with highest probability

Gini impurity is similar (make no difference) to entropy

**decision tree is nonparametric: it does not make any assumption to data**

#### Regularization 
to avoid overfit
* we can restrict  **max_depth**
* **min_samples_split** the minimum number of samples a node must have before splitting 
* max_leaf_nodes

#### Regression 
The algorithm splits each region in a way that makes most training instances as close as possible to that predicted value

#### Instability
decision tree loves perpendicular to axis, so it will be unstable if training set rotates. Also it is sensitive to variations of training data

## Ensemble Learning and Random Forest
Aggregated answer is better than an expert's answer: ensemble learning. 
> A very simple way to create an even better classifier is to aggregate the predictions of each classifier and predict the class that gets the most votes. This majority-vote classifier is called a hard voting classifier

Aggregating weak leaners and ensemble a strong leaner

from the result of the book and mine, 
LogisticRegression 0.864
RandomForestClassifier 0.872
SVC 0.888
VotingClassifier 0.896
the voting classifier has highest probability 

### Bagging and Pasting 
Besides having different training algorithm, we can also have different random subsets of training set.
    * with replacement: bagging
    * without pasting

> Once all predictors are trained, the ensemble can make a prediction for a new instance by simply aggregating the predictions of all predictors. The aggregation function is typically the statistical mode (i.e., the most frequent prediction, just like a hard voting classifier)

The bagging is as following 
```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier
bag_clf = BaggingClassifier(
    DecisionTreeClassifier(), n_estimators=500,
    max_samples=100, bootstrap=True, n_jobs=-1
)
bag_clf.fit(X_train, y_train)
y_pred = bag_clf.predict(X_test)

```

>ensemble’s predictions will likely generalize much better than the single Decision Tree’s predictions: the ensemble has a comparable bias but a smaller variance (it makes roughly the same number of errors on the training set, but the decision boundary is less irregular)

## Random Forest
Instead of building a BaggingClassifier and passing it a DecisionTreeClassifier, you can instead use the RandomForestClassifier class, which is more convenient and optimized for Decision Trees

The book offers an interesting view for random forest classifier: feature importance: 
```python 
from sklearn.datasets import fetch_mldata
mnist = fetch_mldata('MNIST original')
rnd_clf = RandomForestClassifier(random_state=42)
rnd_clf.fit(mnist["data"], mnist["target"])

def plot_digit(data):
    image = data.reshape(28, 28)
    plt.imshow(image, cmap = matplotlib.cm.hot,
               interpolation="nearest")
    plt.axis("off")
```
plot_digit(**rnd_clf.feature_importances_**)
```python
cbar = plt.colorbar(ticks=[rnd_clf.feature_importances_.min(), rnd_clf.feature_importances_.max()])
cbar.ax.set_yticklabels(['Not important', 'Very important'])

save_fig("mnist_feature_importance_plot")
plt.show()
```

### Boosting 
