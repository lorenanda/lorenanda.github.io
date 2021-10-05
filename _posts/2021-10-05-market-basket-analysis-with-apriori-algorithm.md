---
layout: post
title: Market basket analysis with the Apriori algorithm in Python
subtitle: Project
tags: [data science, projects]
comments: true
---

In my previous post, I wrote about . In this post, I'll build on that marketing example and introduce a new algorithm, Apriori, 
from Giuseppe Bonaccorso's book[$$^1$$](#references).

- [Market Basket Analysis](#market-basket-analysis)
- [Theory: Apriori algorithm](#theory-apriori-algorithm)
- [Practice: Apriori algorithm for marketing](#practice-apriori-algorithm-for-marketing)
- [References](#references)

## Market Basket Analysis
Given a set of products $$P = \{p_1, p_2, ..., p_n\}$$, a transaction $$T_i$$ is a subset of $$P$$, expressed as $$P \supseteq T_i = \{p_i, p_j, ..., p_k\}$$. A collection of transactions (or database) is a set of subsets, $$T_i$$, expressed as $$C = \{T_1, T_2, ..., T_p\}$$.

Now, given a transaction containing a set of items, what is the probability of another item $$p_t$$ being bought? Easier put, if a customer purchased lemons and salt, what product are they likely to purchase next (or how likely is it that they will purchase a bottle of tequila for the mix)?

This is the question at the core of market basket analysis, which aims to mine all existing association rules expressed as $$if (p_i, p_j, ..., p_k) \in T_g \Rightarrow P(p_t) \gt \pi$$. than a discriminant threshold $$\pi$$

## Theory: Apriori algorithm
The Apriori algorithm was proposed by Agrawal and Srikant (1994)[$$^2$$](#references).

> Apriori is an efficient solution for performing market basket analysis on large transaction data sets. It enables discovery of the most important association rules existing in the dataset, so as to plan optimal marketing strategies. Classical applications are product segmentation and promotion planning.

> The apriori algorithm uncovers hidden structures in categorical data. The classical example is a database containing purchases from a supermarket. Every purchase has a number of items associated with it. We would like to uncover association rules such as {bread, eggs} -> {bacon} from the data. This is the goal of association rule learning, and the Apriori algorithm is arguably the most famous algorithm for this problem.

## Practice: Apriori algorithm for marketing

First of all, we need to install the Python library [`efficient-apriori`](https://pypi.org/project/efficient-apriori/):

```python
pip install efficient-apriori
```

Now we can mine the shopping transaction data set introduced in the previous post. We want to detect all rules that have a maximum length of 2. 

```python
from efficient_apriori import apriori

_, rules = apriori(transactions,
                   min_support = 0.15,
                   min_confidence = 0.75,
                   max_length = 3,
                   verbosity = 1) #show messages throughout the learning process
```

The code above outputs the following result:

```
Generating itemsets.
 Counting itemsets of length 1.
  Found 100 candidate itemsets of length 1.
  Found 100 large itemsets of length 1.
 Counting itemsets of length 2.
  Found 4950 candidate itemsets of length 2.
  Found 1672 large itemsets of length 2.
 Counting itemsets of length 3.
  Found 14634 candidate itemsets of length 3.
  Found 170 large itemsets of length 3.
Itemset generation terminated.

Generating rules from itemsets.
 Generating rules of size 2.
 Generating rules of size 3.
Rule generation terminated.
```

This code output describes the steps enumerated in the theoretical part. The Apriori algorithm defines the item sets, starting with 1 and ending with 3 (the set limit), filters out the elements with support below 0.15 (the set threshold), and generates rules from the item sets. Now we want to see the generated rules:

```python
print("Number of rules: {}".format(len(rules)))
for r in rules:
    print(r)
```

The code above returns the following result:

```
Number of rules: 233
{P92} -> {P36} (conf: 0.750, supp: 0.240, lift: 1.923, conv: 2.440)
{P23} -> {P20} (conf: 0.769, supp: 0.200, lift: 2.137, conv: 2.773)
{P93} -> {P33} (conf: 0.765, supp: 0.260, lift: 2.012, conv: 2.635)
{P19, P64} -> {P10} (conf: 0.750, supp: 0.150, lift: 1.875, conv: 2.400)
{P10, P20} -> {P64} (conf: 0.789, supp: 0.150, lift: 2.134, conv: 2.992)
{P10, P64} -> {P31} (conf: 0.773, supp: 0.170, lift: 1.981, conv: 2.684)
{P10, P31} -> {P64} (conf: 0.810, supp: 0.170, lift: 2.188, conv: 3.307)
{P33, P39} -> {P10} (conf: 0.750, supp: 0.150, lift: 1.875, conv: 2.400)
...
```

This means that the Apriori algorithm found 233 rules with confidence between 0.75 and 1.00, and support between 0.15 and 0.26 (close to the set value 0.15). The results can be read like this: 
- If a customer bought product 92, there is a 75% chance that they will buy product 36.
- If a customer bought the products 10 and 31, there is an 81% chance that they will buy product 64.

The high confidence is helpful for excluding all the rules with a low probability. However, confidence is not enough. We should also consider the **lift** value, which is calculated as:

$$L(I) = \frac{C(I)}{S(B)} = \frac{S(I)}{S(A)S(B)}$$



-----
## References
1. Bonaccorso, G. (2020). Clustering and Unsupervised Models for Marketing. In: *Mastering Machine Learning Algorithms*, 233–246. UK: Packt Publishing.
2. Agrawal, R.  & Srikant, R. (1994). Fast Algorithms for Mining Association Rules in Large Databases. In: *Proceedings of the 20th International Conference on Very Large Data Bases (VLDB '94)*, 487–499. Morgan Kaufmann Publishers Inc.