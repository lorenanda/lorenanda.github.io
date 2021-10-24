---
layout: post
title: Market basket analysis with the Apriori algorithm in Python
subtitle: Tutorial
tags: [data science, projects]
comments: true
---

In my [previous post]({% post_url 2021-10-03-spectral-biclustering-for-marketing-in-python %}), I wrote about using spectral biclustering for making product recommendations. In this post, I'll build on that marketing example and use the Apriori algorithm for analyzing product purchases This example is, again, taken from Giuseppe Bonaccorso's book *Mastering Machine Learning Algorithms*[$$^1$$](#references).

<details>
    <summary><strong>Table of contents</strong></summary>
    <a href= "#market-basket-analysis">Market Basket Analysis</a><br>
    <a href= "#theory-apriori-algorithm">Theory: Apriori algorithm</a><br>
    <a href= "#practice-apriori-algorithm-in-python">Practice: Apriori algorithm in Python</a><br>
    <a href= "#references">References</a>
</details>


## Market Basket Analysis
Market basket analysis is a data mining technique used by retailers to understand purchasing patterns of their customers. This technique is usually applied on large data sets, such as purchase history in a supermarket, and can reveal how products are grouped and what products are likely to be purchased together.

![market basket analysis](https://upload.wikimedia.org/wikipedia/commons/4/4a/AffinityAnalysis.png)

In formal terms, given a set of products $$P = \{p_1, p_2, ..., p_n\}$$, a transaction $$T_i$$ is a subset of $$P$$, expressed as $$P \supseteq T_i = \{p_i, p_j, ..., p_k\}$$. A collection of transactions is a set of subsets, $$T_i$$, expressed as $$C = \{T_1, T_2, ..., T_p\}$$.

Now, given a transaction containing a set of items, what is the probability of another item $$p_t$$ being bought? In other words, if a customer purchased lemons and salt, what product are they likely to purchase next (or how likely is it that they will purchase a bottle of tequila for the mix)?

This is the question at the core of market basket analysis, which aims to mine all existing association rules expressed as $$if (p_i, p_j, ..., p_k) \in T_g \Rightarrow P(p_t) \gt \pi$$. This expressions means that for a transaction of products, the probability of finding the item $$P(p_t)$$ is greater than a discriminant threshold $$\pi$$.

## Theory: Apriori algorithm
The Apriori algorithm was proposed by Agrawal and Srikant (1994)[$$^2$$](#references) as a solution for performing market basket analysis on large transaction data sets. This algorithm can reveal the most important association rules in the dataset, thus guding the planning of marketing strategies, such as product segmentation or promotion.

Given the maximum number of items in a transaction, the Apriori algorithm proceeds in 4 steps:
1. **Computing** the support of all products $$S(p_i)$$
2. **Removing** all items with $$S(p_i) \lt \pi$$ (with $$\pi \gt 0$$, since we are not interested in products that are rarely sold).
3. **Analyzing** all couples, triplets, and so on, and applying the same filter.
4. **Splitting** the results of each pass (item sets) into disjointed subsets to make up the association rules.  
   The association rules have the form of logical implications in modus ponens: $$if A \Rightarrow B$$ and $$A$$ is true, $$B$$ is also true. Practically, an association rule is, for example: `{bread, hummus} -> {avocado}`.  
   Given the association rules, we also need to know the confidence of a rule, i.e. how frequently the consequent is true when the whole rule is true. The confidence of a rule is represented as an item set: $$C(I) = \frac{S(I)}{S(A)}$$, where $$S(I)$$ is the support of the item set before the split and $$I$$ has been split into $$A$$ and $$B$$.

The Apriori algorithm has proven to be simple and effective in practice. However, it also has the drawback that it needs larget thresholds for very large datasets. Therefore, it's recommended to segment the customers and apply Apriori to to each subset of transactions.

## Practice: Apriori algorithm in Python
Let's put the theory into practice! For this example, we have a data set that contains information about 100 users and 100 transactions (purchases) of 100 different products. Every purchase has a number of items associated with it. For example, Purchase 1 consists of two products (Product 2 and Product 5), Purchase 2 consists of five products, and so on. We want to know what other product could be associated with each transaction.

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

This code output describes the steps enumerated in the [theoretical part](#theory-apriori-algorithm). The Apriori algorithm defines the item sets, starting with 1 and ending with 3 (the set limit), filters out the elements with support below 0.15 (the set threshold), and generates rules from the item sets. Now we want to see the generated rules:

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

The high confidence is helpful for excluding all the rules with a low probability. However, we should also consider the **lift** value, expressed as: 

$$L(I) = \frac{C(I)}{S(B)} = \frac{S(I)}{S(A)S(B)}$$

The lift value $$L(I)$$ represents the ratio between the joint probability of the rule and the product of the probabilities of the antecedent and consequent. 

The lift will always be greater than or equal to the confidence. As $$C(I) = L(I)S(B)$$, the smaller $$S(B)$$ is, the larger $$L(I)$$ has to be. The lift value of 1 indicates that all transactions contain the element(s) in $$B$$–the ideal case. In real-world cases, this is almost impossible, so the lift is generally greater than 1 and is reasonable in the range (1.5, 2.5).

On the other hand, the support value $$S(B)$$ of 1 indicates a trivial rule, that most transactions contain the specific product (for example, shopping bags).

Keep this in mind when setting the threshold for lift and, better yet, define an interval.

-----
## References
1. Bonaccorso, G. (2020). Clustering and Unsupervised Models for Marketing. In: *Mastering Machine Learning Algorithms*, 233–246. UK: Packt Publishing.
2. Agrawal, R.  & Srikant, R. (1994). Fast Algorithms for Mining Association Rules in Large Databases. In: *Proceedings of the 20th International Conference on Very Large Data Bases (VLDB '94)*, 487–499. Morgan Kaufmann Publishers Inc.