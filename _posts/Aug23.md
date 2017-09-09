# Machine Learning in Spam Filtering (I)

I studied novelty detection for the last two months. Distinguishing  a novel pattern from many studied patterns can be a new step for me from one-class classification to general machine learning methods. I believe spam filter can be a good start. I will structure this blog by a review by Guzella and Caminhas[1].

I ran into this problem when I worked on ClassUCLA project: its latter iterations can send email to predefined accounts. Because of the privacy issues, I decide not to release those versions. At first I chose to use STMP servers of my Yahoo and a few other large companies' email account, but most of my emails were classified as spam email and failed to sent them. 

## The reason for data-driven spam filtering 
The old fashion way to do this is to filter certain keywords. For example, users can define keyword "stranger" such that all emails that have word stranger will be classified as spam email. However, spammers began to adopt content "obfuscation" to avoid these user defined filters, for example, using "sch001" instead of "school".  
The challenge faced by all spam filter is high cost of true-negative rate. 

## Basic Technique
For text-based spam filtering, it is more likely to do a text categorization or plagiarism detection. The following five steps are used to preprocess the information
1. tokenization: extract words
2. lemmatization: extract key words 
3. stop-word removal: remove common words like "to", "a", "for"
4. representation: convert the remaining information into machine learning algorithm input 
5. feature selection: selecting most representative features from previous steps

### Bag of Words(BoW) representation
A vector is usually used to represent a text. This technique is usually called bag-of-words. Given a set of _priori_ or predefined terms {t_1, t_2 ... t_N}, information can be represented by a N-dimensional feature vector. The feature vector can be formed token  by 
* a sliding window through a sequence of characters
* the number of occurrence of certain word, or n-gram model
and the feature can be represented by 
* binary representation: if certain word exist 
* frequency representation: the number of occurrences of that feature 
* term frequency-inverse document frequency: a log-based indication based on documents. 

Then we extract features by, for example, calculating information gain. We can calculate a frequency score to each term and select terms with highest core. Then we evaluate the difference of term-frequency variance for this document and that for all documents in the training set. By extracting features, we can focus more on meaningful and important features. 

The problem for this algorithm is similar to many probabilistic approaches: it can be represented with minimal space and ran with minimal time, but its cannot be trained online. As a result, the model cannot learn new spam messages by itself.


## Naïve Bayes 
Algorithms in this category are all based on Bayesian framework, which P(c|x)P(x) = P(x|c)P(c). P(x|c) is that when message belongs to c is known, the probability that x is in that message. P(x) is a _priori_ probability of a message by x. 
The P(c), P(x|c), P(c|x) are computable by multiplying all components together by product rule or total probability rule. 

### Sahami et al. and Graham
Both of these two algorithms are abased on 
Sahami et al. generate a feature vector based occurrence of selected feature, while Graham select N words that have maximum probabilities. 
However, both of them can be considered as Naive Bayes because they are just calculating possibilities. 

### Other Bayesian Practices 
Just for the sake of convenience, this section will go through some of works mentioned by Guzella and Caminhas. I will keep my further updates in similar algorithms that I found or I think of to other dates or other blogs. 

* Interpolated Language Model: Medlock(2006): it considers subject and body of the email. The classification relies on 
> This classification of a message relies on aggregating a static(the entire training data) and a dynamic(periodically re-training with new data) component. 
* Uncertainty Sampling:Segal et al.(2006): it is not quite based on Sahami et al.'s usage of Bayesian Framework. It is a iterative classifier 
> that outputs the confidence in the classification of all messages and request true labels of some of the messages that have the smallest confidence
* Dynamic Personalization: Segal(2007): it considers a heterogeneous setting for every users and takes into account for a global filter and a personal filter. 

## References 
Guzella, Thiago S., and Walmir M. Caminhas. “A Review of Machine Learning Approaches to Spam Filtering.” _Expert Systems with Applications_, vol. 36, no. 7, 2009, pp. 10206–10222., doi:10.1016/j.eswa.2009.02.037. 

## Notes and Take away
This is just a start for me. I will update what I read, what I think and this will be what I write. Because I am just a beginner and I will limited to my schedule, deadlines and potential unseen events, stopping to update is the least thing I want. Thus I sometimes divide things up and keep updating.  

## A list for latter researches 
ANN
Bayesian 

