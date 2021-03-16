---
layout: post
title: Exploring endangered languages with pandas
subtitle: Tutorial
gh-repo: lorenanda/world-languages
gh-badge: [star, fork, follow]
tags: [linguistics, data]
comments: true
---

![Crepe](https://s3-media3.fl.yelpcdn.com/bphoto/cQ1Yoa75m2yUFFbY2xwuqw/348s.jpg){: .mx-auto.d-block :}

On the occasion of the International Mother Language Day (21st February), I wrote an essay (in French) about the importance of preserving endangered languages and I thought of pairing that with a data science challenge. In this simple project, I analysed and visualised the global distribution of language families and dialects.

* Topic: Exploratory Data Analysis & Visualisation
* Libraries: pandas, matplotlib
* Dataset: World Language Family Map
* Code: GitHub

# Setup
The first step in the exploratory analysis is to read in the data and get an overview of the features: how many rows and columns are included and what are the names of the columns.

```python
import pandas as pd
df = pd.read_csv('languoid.csv')
df.head(10)
df.shape
list(df.columns)
```

And here is the same code yet again but with line numbers:

{% highlight python linenos %}
import pandas as pd
df = pd.read_csv('languoid.csv')
df.head(10)
df.shape
list(df.columns)
{% endhighlight %}

The dataset contains 23243 observations and 18 language features, but for this project I am interested in only three features: level, name, and status. To make things easier, I select only these three features and create a new dataframe with the subset data:

```python
lns_df = df[['level', 'name', 'status']]
```

# Exploratory Analysis
## Overview

I start the exploratory analysis with an overview of the selected features in lns_df, so I want to see how many unique values each feature has:

```python	
lns_df['level'].unique()
```

Level is a categorical variable with three levels:

* dialect: a particular form of a language which is peculiar to a specific region or social group.
* family: a group of languages related through descent from a common ancestral language or parental language.
* language: an official language spoken in a region.

```python	
lns_df['status'].unique()
```

Status is a categorical variable with 6 levels. They are based on UNESCO’s Language Vitality and Endangerment framework that establishes six degrees of vitality/endangerment. From safest to extinct, these are:

* safe: language is spoken by all generations; intergenerational transmission is uninterrupted.
* vulnerable: most children speak the language, but it may be restricted to certain domains (e.g., home).
* definitely endangered: children no longer learn the language as mother tongue in the home.
* severely endangered: language is spoken by grandparents and older generations; while the parent generation may understand it, they do not speak it to children or among themselves.
* critically endangered: the youngest speakers are grandparents and older, and they speak the language partially and infrequently.
* extinct: there are no speakers left.

## Language level

Next, more specifically I want to see how many language families, languages, and dialects are in the dataset:

```python	
lang_sum = pd.value_counts(df['level'].values, sort=False)
```

There are 8444 language families, 4268 languages, and 10531 dialects. It makes sense that there are way more dialects than languages and language families, since a language family encompasses several languages, which in turn have different dialects. It’s easier to put these numbers into perspective by visualising them:

```python		
import matplotlib.pyplot as plt
%matplotlib inline  
lang_sum.plot(kind='bar')
```

## Language status

Find the total number of languages in each status:

```python	
status_sum = pd.value_counts(lns_df['status'], sort=True)
status_sum.plot(kind='pie')
```

Over 80% of languages in the dataset are safe, which leaves 14% of data on endangered languages to analyse. Of these, most are extinct, and the fewest are critically endangered. Now let’s get a summary table of languages in each level by status:

```python	
level_status = pd.crosstab(df.level, df.status)
level_status.plot(kind='bar', stacked=True)
```

## Endangered languages

After getting an overview of the language status and level situations, I want to see what specific languages are in each group. Specifically, I was curious what language families were extinct:

```python		
ext_fam = df[(df.level == 'family') & (df.status == 'extinct')]
ext_fam_names = ext_fam[['name']]
```

There are three extinct language families: Chimakuan, Djiwarli-Thiin, and Garrwan.

# To be continued

This exploratory analysis is only a starting point, there are many other questions you can explore from this dataset. For example, find what dialects are critically endangered, what is the geographic distribution of endangered languages, or maybe analyse and visualise the data with other libraries than pandas and matplotlib. Have a look at my Jupyter notebook and play around with the data!

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
