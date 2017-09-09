# Machine Learning x Intrusion Detection 
Yesterday I visited a predictive analysis lab and a network security lab in Siemens Ltd,. An idea (of course covered by many researches) crossed my mind and I do want to see how the hybrid of these two concepts, machine learning and network security, generates wonderful results. As a result, this blog is going to discuss feasibility of their combination.  

The system that we want to build is called **Intrusion Detection System(IDS)**, which can detect different types of malicious network communications and computer usage. There are two types of IDS: 
* anomaly detection: a branch of novelty detection, which measures the derivation from normal system
* misuse detection: a comparison algorithm to previously known attacks 

## An analysis for intrusion detection 
In Sommer and Paxson's work in 2010, they believe there is a discrepancy between two detection methods mentioned above. The misuse detection is extensively used that signature system scans network traffic for characteristic byte sequences, while anomaly detection is rarely used. I will cover commonly studied techniques in the latter section in Tsai et al's paper. Sommer and Paxson list many reasons that other machine learning algorithms do not work for intrusion detection. Based on my own experience in novelty detection, I don't think "outlier detection" which one class classification is different from traditional classification algorithms, and high cost of errors, (they compare with other applications, like spam detection that we talked a few days ago). I think the true reason is about semantic gap: we might know the combination of traffic, ip visit, login name might result in an alarm for novelty case, but this novelty case might not directly point out either "this is an attack" or "why there is an alarm". 
* many security constraints are a site-specific property. As a result, access from an enterprise, or organization might differ: a situation, although diverse, can be labelled manually. However,there is another situation:
    > environment might tolerate peer-to-peer traffic as long as
it is not used for distributing inappropriate content, and
that it remains “below the radar” in terms of volume. 
* I did research before on "why there is an alarm". The method I tried was to find corresponding variables by time-series(or other dimension) correlation analysis. 
(Suddenly this occurred to me: why don't I just write about it: from novelty detection to reasoning)

As a result, Sommer and Paxson believe a big failure for many conference submissions is the failure to understand data and results in a system. For example, knowing the real network traffic is important and we need to watch out for true positive and true negative cases. Based on these concerns, they believe machine learning approach is hard to be applied effectively in intrusion detection. It works only if insights are offered. As a result, I use Tsai et al.'s review of methodologies. 

## References
Tsai, Chih-Fong, et al. “Intrusion Detection by Machine Learning: A Review.” *Expert Systems with Applications*, vol. 36, no. 10, 2009, pp. 11994–12000., doi:10.1016/j.eswa.2009.05.029. 

Sommer, Robin, and Vern Paxson. “Outside the Closed World: On Using Machine Learning for Network Intrusion Detection.” *2010 IEEE Symposium on Security and Privacy*, 2010, doi:10.1109/sp.2010.25. 