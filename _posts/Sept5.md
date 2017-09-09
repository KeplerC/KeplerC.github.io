## Chapter II End-to-End

first we fetch the tgz file from https://raw.githubusercontent.com/ageron/handson-ml/master/ 
by wget, then untar it to produce a Common separate value file. 


### Loading data and showing them
Then we write a function that loads csv data 

```python
def load_housing_data(housing_path = HOUSING_PATH):
    csv_path = os.path.join(housing_path, "housing.csv")
    return pd.read_csv(csv_path)
```

and show them by 

```python
def give_a_quick_view(data):
    print ("__________housing's head____________")
    print (data.head())
    print ("_________ table information________")
    print (data.info())
    print ("__________Data's descrpition_______")
    print (data.describe())

    data.hist(bins=50, figsuze=(20, 15))
    plt.show()
```

  longitude  latitude  housing_median_age  total_rooms  total_bedrooms  \
0    -122.23     37.88                41.0        880.0           129.0   
1    -122.22     37.86                21.0       7099.0          1106.0   
2    -122.24     37.85                52.0       1467.0           190.0   
3    -122.25     37.85                52.0       1274.0           235.0   
4    -122.25     37.85                52.0       1627.0           280.0   

### Create a test set 
#### Naive approach
We randomly choose 20% of dataset, set them aside as test sets.
(to detect overfitting)
to do this, we call permutation and use [:] to split indices 
#### a stable one 
use hash table 
we add a housing ID by

```python
    housing_with_id = housing.reset_index() #add an index column
    
# build a hash table by 
    hash(np.int64(indentifier).digest()[-1]<256 * 0.2>)
# and build test_set by 
    data[id_column].apply(lambda id_: (above hash funct))
```

#### A simpler one by kl learn

```python
from sklearn.model_selection import train_test_split
train_set, test_set = train_test_split(housing, test_size=0.2, random_state=42)
```

and we can use my self defined function to plot it 


#### stratified sampling
Although this part is not implemented in code, I will learn from this lab report
we divide population into homogenous subgroups called strata, and sample from each subgroups

Use 

```python 
    housing["median_income"].hist()
```

normalize it and choose from each subgroups 

### Exploring data
Scatter plot is a good way of showing data
I used two of the plotting methods that the book offers 

```python
    housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.1)
```

```python
    housing.plot(kind="scatter", x="longitude", y="latitude", alpha=0.4,s=housing["population"]/100, label="population", c="median_house_value", cmap=plt.get_cmap("jet"), colorbar=True,)
    plt.legend()
```

to generate beautiful graphs 

#### correlations 
we find standard correlation pcc to find correlations between these data
```python
    corr_matrix = housing.corr()
    #and find closest correlationers by 
    corr_matrix["median_house_value"].sort_values(ascending=False)
```

another way of doing this is use panda's plotting technique 

Based on that we can even experiment on combination of factors (like rooms per household)

through my self-defined function 
```python 
def correlation(data, label):
    return data.corr()[label].sort_values(ascending=False)  
```
we can generate a same result from book 
median_house_value    1.000000
median_income         0.688075
total_rooms           0.134153
housing_median_age    0.105623
households            0.065843
total_bedrooms        0.049686
population           -0.024650
longitude            -0.045967
latitude             -0.144160

### Data Cleaning

#### Missing features 
**Machine learning algorithm cannot work with missing features**

to solve this problem, the book offers three ways of doing this: 
```python 
housing.dropna(subset=["total_bedrooms"]) # option 1
housing.drop("total_bedrooms", axis=1) # option 2
median = housing["total_bedrooms"].median()
housing["total_bedrooms"].fillna(median) # option 3
```

as name suggests, first one is get rid of corresponding districts, the second one is to ignore this whole attributes and the option 3 is the set to (mean, 0, median, etc)

or use sklearn 

```python
from sklearn.preprocessing import Imputer
imputer = Imputer(strategy="median")
```

#### text and categorical attributes 
We preprocess the other label, ocean_proximity by labelling it.
we can use pipeline for it by 

```python
from sklearn.pipeline import Pipeline
from sklearn.preprocessing import StandardScaler
from sklearn.pipeline import FeatureUnion

num_attribs = list(housing_num)
cat_attribs = ["ocean_proximity"]

num_pipeline = Pipeline([
('imputer', Imputer(strategy="median")),
('attribs_adder', CombinedAttributesAdder()),
('std_scaler', StandardScaler()),
])

cat_pipeline = Pipeline([
('selector', DataFrameSelector(cat_attribs)),
('label_binarizer', LabelBinarizer()),
])

full_pipeline = FeatureUnion(transformer_list=[
("num_pipeline", num_pipeline),
("cat_pipeline", cat_pipeline),
])

housing_num_tr = num_pipeline.fit_transform(housing_num)
```

>You framed the problem, you got the data and explored it, you sampled a training set and a test set, and you wrote transformation pipelines to clean up and prepare your data for Machine Learning algorithms automatically.

We can self define transformers by initializing three major methods in a class 
```python
__init__
fit()
transform()
```

### Train model 
It is very very easy to use libraries to do that. like 
```python 
from sklearn.linear_model import LinearRegression
lin_reg = LinearRegression()
lin_reg.fit(housing_prepared, housing_labels)

#or 

from sklearn.tree import DecisionTreeRegressor
tree_reg = DecisionTreeRegressor()
tree_reg.fit(housing_prepared, housing_labels)
```