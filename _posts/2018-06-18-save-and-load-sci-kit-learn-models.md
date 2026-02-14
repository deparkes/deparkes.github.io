---
layout: post
title: Save and Load Sci-kit Learn Models
date: 2018-06-18 16:30:13.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags: []
author: deparkes
permalink: "/2018/06/18/save-and-load-sci-kit-learn-models/"
---
Once you have trained a sci-kit learn model it is not obvious how you can deploy it and use it to score unseen data. This post shows you how to save and learn sci-kit learn models so you can execute it against unseen data.
<h1>Train Your Model</h1>
The first step is to train the model we want to deploy. In this example we will make a very simple model using the titanic data set. <a href="{{site.url}}/2018/02/02/scikit-learn-simple-classification/">Read more about training a simple model with sci-kit learn.</a>

```python
import pandas as pd
from sklearn.linear_model import LogisticRegression
# Get data
data = pd.read_csv('https://web.stanford.edu/class/archive/cs/cs109/cs109.1166/stuff/titanic.csv')
# Prepare data for model
X = data[['Age', 'Pclass']]
y = data.Survived.values
# Create and fit model object
clf = LogisticRegression()
clf.fit(X,y)
# Check model score
clf.score(X,y)
```

<h1>Save The Model as a 'Pickle'</h1>
A '<a href="https://pythontips.com/2013/08/02/what-is-pickle-in-python/">pickle</a>' file is a way that python can <a href="https://www.diveintopython3.net/serializing.html">save a data structure</a> to a file (similar to how you might save your progress in a computer game).
Sci-kit learn has its <a href="https://scikit-learn.org/stable/modules/model_persistence.html">own functions</a> for pickling using <a href="https://pythonhosted.org/joblib/persistence.html">joblib</a> which is <a href="https://stackoverflow.com/questions/12615525/what-are-the-different-use-cases-of-joblib-versus-pickle">typically faster</a> when saving larger files.
To save a pickle file we can use 'joblib.dump()':

```python
from sklearn.externals import joblib
# Output a pickle file for the model
joblib.dump(clf, 'saved_model.pkl')
```

The resulting 'saved_model.pkl' is a file on disk made from the 'clf' object.
<h1>Load The Pickled Model</h1>
Once we have a saved pickle file, we can use joblib.load() to load it back in to python.

```python
# Load the pickle file
clf_load = joblib.load('saved_model.pkl')
```

The loaded pickle file becomes an object like any other in the python script.
We can do a simple check that the saved model and the loaded model yield the same performance:

```python
# Check that the loaded model is the same as the original
assert clf.score(X, y) == clf_load.score(X, y)
```

<h1>Bringing It Together</h1>
Here is a combination of the previous snippets, in a single script, which also has a check that the saved and loaded models are doing the same thing.

```python
import pandas as pd
from sklearn.externals import joblib
from sklearn.linear_model import LogisticRegression
# Get data
data = pd.read_csv('https://web.stanford.edu/class/archive/cs/cs109/cs109.1166/stuff/titanic.csv')
# Prepare data for model
X = data[['Age', 'Pclass']]
y = data.Survived.values
# Create and fit model object
clf = LogisticRegression()
clf.fit(X,y)
# Check model score
clf.score(X,y)
# Output a pickle file for the model
joblib.dump(clf, 'saved_model.pkl')
# Load the pickle file
clf_load = joblib.load('saved_model.pkl')
# Check that the loaded model is the same as the original
assert clf.score(X, y) == clf_load.score(X, y)
```

