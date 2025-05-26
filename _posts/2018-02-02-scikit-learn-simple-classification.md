---
layout: post
title: scikit-learn Simple Classification
date: 2018-02-02 15:30:10.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- classifier
- data science
- machine learning
- scikit-learn
- sklearn
author:
  display_name: deparkes
permalink: "/2018/02/02/scikit-learn-simple-classification/"
---
This post looks at how to build a simple classification model with the python machine learning library <a href="http://scikit-learn.org/stable/">scikit-learn</a>. Building a simple classification model is fairly easy with sci-kit learn, and this post explores some of the default behaviour and sign-posts some extra work that we would want to to ensure robust predictions.
I've tried to strip the code to a minimum to keep things simple. The main steps are:
<ul>
<li>Get data - features and target</li>
<li>Create an instance of an sklearn classifier</li>
<li>Train the classifier using the data</li>
<li>Output predicted classifications</li>
</ul>
Steps for validation and optimisation have been left out.
<h1>Some Sample Data</h1>
I'm going to use one of the <a href="{{site.baseurl}}/2016/11/11/python-sample-datasets/">sample datasets</a> that come with scikit-klearn to run a simple classification. The <a href="http://scikit-learn.org/stable/modules/generated/sklearn.datasets.load_breast_cancer.html">breast cancer dataset</a> is a good example for looking at binary classification.

```python
# Get sample dataset from sklearn datasets
from sklearn import datasets
cancer = datasets.load_breast_cancer()
```

These sample datasets with sklearn are useful for trying out things. If you have your own data then you can substitute them for the X and y variables in the following section.
A 'real world' data set is likely to need further <a href="https://machinelearningmastery.com/data-cleaning-turn-messy-data-into-tidy-data/">preparation and cleaning</a>, such as:
<ul>
<li>Handling categorical data</li>
<li>Cleaning data values</li>
<li>Standardising column names</li>
</ul>
<h1>Simple Classification</h1>
The following is a bare-bones example of classification with scikit-learn. I am using a <a href="http://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html">random forest</a> classifier, but you could change the code to try out <a href="http://scikit-learn.org/stable/auto_examples/classification/plot_classifier_comparison.html">other classifiers</a> too.

The breast cancer example data are used as the X and y variables. X is by convention used to represent the '<a href="https://en.wikipedia.org/wiki/Feature_(machine_learning)">feature</a>' data for the classification model - the characteristics that describe different cases or patients. y is used to represent the target variable - in this case whether the case was found to be cancerous or not.

In sci-kit learn X is a <a href="https://docs.scipy.org/doc/numpy-1.13.0/reference/arrays.ndarray.html">numpy array</a> of shape (m,n), where m is the number of observations and n is the number of features in the feature data. In the breast cancer example m =569 and n = 30. y is a 1d numpy array of shape (m,). As before m = 569. If you are not familiar with numpy 1d and nd arrays you may want to read up on them [<a href="https://stackoverflow.com/questions/22053050/difference-between-numpy-array-shape-r-1-and-r">1</a>], [<a href="https://stackoverflow.com/questions/29241056/how-does-numpy-newaxis-work-and-when-to-use-it">2</a>].
This code outputs the first few actual and predicted classes so you can get an idea for how how well the classifier is performing.

```python
from sklearn.ensemble import RandomForestClassifier
X = cancer.data # (m,n) numpy array
y = cancer.target # (m,) numpy array
# Create an instance of the classifier we want to use
clf = RandomForestClassifier()
clf.fit(X,y)
preds = clf.predict(X)
print(preds[:5,]) # Predicted classes
print(y[:5,]) # Actual classes
pred_proba = clf.predict_proba(X)
print(pred_proba[:5,0]) # Probability of zero
print(pred_proba[:5,1]) # Probability of one
```

<h1>Taking Things Further</h1>
This post has kept has shown only a simple classification approach. There are a number of other things you would probably want to include to check that your classification predictions are accurate and improving model performance.
These refinements include (but are not limited to):
<ul>
<li>Optimising the <a href="https://stackoverflow.com/questions/19984957/scikit-predict-default-threshold">decision threshold</a>
</li>
<li>Tuning <a href="https://en.wikipedia.org/wiki/Hyperparameter_optimization">hyperparameters</a>
</li>
<li>Selecting <a href="https://sebastianraschka.com/blog/2016/model-evaluation-selection-part1.html">the best classifier algorithm</a>
</li>
</ul>
