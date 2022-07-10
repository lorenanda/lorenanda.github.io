---
layout: post
title: January's regression challenge for Kaggle playground
gh-repo: lorenanda/kaggle-playground
gh-badge: [star, fork, follow]
tags: [data science, Python, tutorials]
comments: true
---


At the beginning of the new year 2021, Kaggle created a new format of competitions aimed at beginners. On the 1st of each month, a month-long Playground competition is launched, where you can practice your ML skills on simple tabular datasets. Apart from competitive experience, the top 3 teams get to win some Kaggle merchandise!

## Exploratory Analysis

[January's challenge](https://www.kaggle.com/c/tabular-playground-series-jan-2021) is about regression and contains a tabular dataset split into train and test sets.

The train set contains 300.000 data points with 14 features (continuous between 0 and 1) and 1 target variable (continuous between 6 and 10). The test set, used for making predictions, contains 200.000 data points with the same 14 features. The results are evaluated with the [RMSE score](https://en.wikipedia.org/wiki/Root-mean-square_deviation).

First of all, I did a quick exploratory analysis. I was mainly interested in the correlation matrix, since in datasets with lots of features like this one, it’s likely that some of the variables are correlated – and it turned out this was the case:

![Matrixplot](blog_images/kaggle-challenge-jan-matrix.png)

## Machine Learning Models

Moving on to the modelling part, I first split the train set further into a train and test set, then tried out four models:

- **Linear Regression** just for fun, though I expected it to be too simplistic for this data set.
- **Random Forest Regressor** with and without Recursive Feature Elimination. Contrary to my expectation, I got a better score with all features included.
- **Gradient Boosting Regressor** with 100 estimators and a depth of 5 was slightly better that RFR.
- **XGBoost with GridSearchCV** for finding the optimal hyperparameters. As expected, this model performed best, with little tweaking and from what I see it’s widely used in Kaggle competitions.

## Results

I submitted the predictions made by each model on Kaggle and here are the RMSE scores I achieved:

**MODEL** | **RMSE**
XGBoost | 0.69995
Gradient Boosting | 0.70723
Random Forest Regressor | 0.71094
Random Forest Regressor + RFE | 0.71459
Linear Regression | 0.724

My best score placed me on position **281 out of 913**. As always, there’s room for improvement, maybe by tweaking the XGBoost hyperparameters or trying out other models.

In conclusion, though the data set was uninformative and not really insightful, this Kaggle challenge was a good exercise for trying out regression models.
