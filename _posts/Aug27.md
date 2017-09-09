# Machine Learning x Intrusion Detection 

## Tsai et al.: a review of intrusion detection 
Tsai et al. reviews 55 works in intrusion detection and believes most of the current works belong to three types of classifiers: single, hybrid and ensemble. 
* Single classifier includes most of the classifiers that we usually encounter, like k-NN, SVM, SOM, ANN, Baye)sian Networks.
* Hybrid classifier combines, integrate, cascade or preprocess multiple single classifiers to generate better accuracy. 
* Ensemble classifier: ensemble refers to the combination of multiple weak learning algorithm. A weak learner is a classifier that is slightly better than random guessing. Then we can get a strong learner by boosting
     > most boosting algorithms consist of iteratively learning weak classifiers with respect to a distribution and adding them to a final strong classifier. When they are added, they are typically weighted in some way that is usually related to the weak learners' accuracy. After a weak learner is added, the data are reweighted: examples that are misclassified gain weight and examples that are classified correctly lose weight. 

Those graphs can be found on their original published paper. Here are a few key results that are worthwhile discussing:
* SVM and k-NN are most popular for intrusion detection. 
    * I think the importance of SVM is self-evident. SVM is the top two classifier, no slight difference between random forest(RF), as published in [Do we Need Hundreds of Classifiers to Solve Real World Classification Problems? Manuel Fernández-Delgado, Eva Cernadas, Senén Barro, Dinani Amorim](http://jmlr.org/papers/v15/delgado14a.html) As a result, I will go deeper and deeper on SVM and this paper later. 
    * On the other hand, why k-NN, a relatively computationally expensive parametric algorithm drew so much attention? I think the reason is that first, this is a paper published in 2007, such that a lot of good ANNs were not available; second, it is an instance based learning rather than a rule inductive learning algorithm. 
        * Difference between Rule Inductive and Instance based algorithm
            * instance based learning performs explicit generalization and compares with **instances** in memory
            * Rule Generated is opposite to instance based algorithm. It is trained by regression(or other methods) and generates rules rather than instances to store the model. 
        * it is an on-line algorithm that does not require training stage and just searches in specified learning sets. 
* Integration is most popular in Hybrid classifiers. 


## References
Tsai, Chih-Fong, et al. “Intrusion Detection by Machine Learning: A Review.” *Expert Systems with Applications*, vol. 36, no. 10, 2009, pp. 11994–12000., doi:10.1016/j.eswa.2009.05.029. 

Sommer, Robin, and Vern Paxson. “Outside the Closed World: On Using Machine Learning for Network Intrusion Detection.” *2010 IEEE Symposium on Security and Privacy*, 2010, doi:10.1109/sp.2010.25. 