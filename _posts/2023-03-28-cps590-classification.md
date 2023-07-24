---
layout: default
title: Data Science:Classification
---
# Classification
## Machine Learning
- Supervised Learning
- Unsupervised Learning
## Models
### Decision Tree
#### Which Attribute is the Best?
Greedy Algorithm (is it optimal?) \\
Question: Which attribute lead to good division? \\
How to define good? How to compare two divisions? \\
How to define purity of a dataset?
$$Entropy(S)=\sum_{i=1}^c{-p_ilog_2p_i}$$
Information Gain: How does the partitioning help us improve purity?
$$Gain(S,A)=Entropy(S)-\sum_{v\inValue(A)}{\frac{|S_v|}{|S|}Entropy(S_v)}$$
Find the attribute with the largest gain.
#### Natural Bias
Devision tree tends to favor attributes with many values. E.g. Weather forcasting with attribute date.
##### Solution
Gain Ratio:
$$GainRatio(A)=\frac{Gain(A)}{SplitInfo_A(D)}$$ \\
$$SplitInfo_A(D)=-\sum_{i=1}^v\frac{|D_j|}{D}log_2{\frac{|D_j|}{|D|}}$$


#### Drawbacks
- The optimal splitting is NP-hard
#### Gini Index
Measure inequality \\
In a dataset, the more inequal means purer.
$$Gini(T)=1-\sum_{j=1}^n{p_j^2}$$
### ID3
### C4.5
### C5
### CART
