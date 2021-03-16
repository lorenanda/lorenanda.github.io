---
layout: post
title: Exploring endangered languages with pandas
subtitle:tutorial
gh-repo: lorenanda/world-languages
gh-badge: [star, fork, follow]
tags: [test]
comments: true
---

On the occasion of the International Mother Language Day (21st February), I wrote an essay (in French) about the importance of preserving endangered languages and I thought of pairing that with a data science challenge. In this simple project, I analysed and visualised the global distribution of language families and dialects.

* Topic: Exploratory Data Analysis & Visualisation
* Libraries: pandas, matplotlib
* Dataset: World Language Family Map
* Code: GitHub

## Setup

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


![Plot](../assets/img/endangered2.png){: .mx-auto.d-block :}

### Notification

{: .box-note}
**Note:** This is a notification box.

### Warning

{: .box-warning}
**Warning:** This is a warning box.

### Error

{: .box-error}
**Error:** This is an error box.
