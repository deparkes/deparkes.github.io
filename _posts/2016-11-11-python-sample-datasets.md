---
layout: post
title: Python Sample Datasets for Datascience and Machine Learning
date: 2016-11-11 15:00:04.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
tags:
- data
- datascience
- datasets
- pandas
- python
- seaborn
- sklearn
- test data
author: deparkes
permalink: "/2016/11/11/python-sample-datasets/"
---
Find out where to find sample datasets for playing with data in Python. If you're testing or validating a model or analysis for data science or machine learning, it can be useful to have some sample data to play with. R has the <a href="https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html">datasets package</a> which makes loading sample datasets easy, but it's not so obvious what to do in python - this post shows you some of the options.

<h2>Load csv files from the internet</h2>
A simple way to get sample datasets in Python is to use the pandas 'read_csv' method to load them directly from the internet. To do this just put the address of your target csv dataset as the argument to read_csv:

```python
import pandas as pd
data = pd.read_csv("https://www.ats.ucla.edu/stat/data/binary.csv")
```

You can actually use this method to <a href="https://vincentarelbundock.github.io/Rdatasets/datasets.html">load the datasets</a> found in the r datasets package - just copy the link to the csv files. It's a bit clunkier than the R package, but it does give you easy access to the data.<code><span class="kwd">
</span></code>
<h2>Use The Seaborn Library</h2>
<a href="{{site.url}}/2015/05/05/seaborn-python-plotting-library/">Seaborn</a> is primarily a plotting library for python, but you can also use it to access sample datasets. The example below loads the iris dataset as a pandas dataframe (the iris dataset is <a href="https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/iris.html">also available in R</a>).

```python
import seaborn.apionly as sns
iris = sns.load_dataset('iris')
```

Find out more about this method <a href="https://stackoverflow.com/questions/28417293/sample-datasets-in-pandas">here</a>.
<h2>Use the sklearn package</h2>
<a href="https://scikit-learn.org/stable/">Sci-kit-learn</a> is a popular machine learning package for python and, just like the seaborn package, sklearn comes with <a href="https://scikit-learn.org/stable/datasets/">some sample datasets</a> ready for you to play with.
You can access the sklearn datasets like this:

```python
from sklearn.datasets import load_iris
iris = load_iris()
data = iris.data
column_names = iris.feature_names
```

If you like to use pandas to work with your data, then you'll also want to do something like this to get the sklearn data into a pandas dataframe:

```python
import pandas as pd
df = pd.DataFrame(iris.data, iris.feature_names)
```

Let me know if you have any better ways to access sample datasets in python.
