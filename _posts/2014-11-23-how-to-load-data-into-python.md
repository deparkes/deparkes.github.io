---
layout: post
title: 'Python Tips: How to Load Data Into Python'
date: 2014-11-23 19:01:27.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- data
- python
- python tips
author:
  display_name: deparkes
permalink: "/2014/11/23/how-to-load-data-into-python/"
---
In this post we'll look at three different ways of how to load data into python. Loading date is the crucial first step before carrying out any data analysis or processing.
We'll look at methods that use just the core python modules, and those that use 'numpy', a numerical computing module for python.
The script and data files used in this article are available at this github <a href="https://github.com/deparkes/PythonTips/tree/master/LoadDataFiles" target="_blank">repository</a>.
<h1>A word on numpy</h1>
If you haven't already I recommend installing <a href="http://www.numpy.org/" target="_blank">numpy</a>, a numerical programming module for python. Numpy will come in handy later for analysing our imported data, so by directly importing into a numpy-ready format we can be ready to continue to analyse and process the imported data.
You can either do this as a single module or as part of a scientific python distribution (my preferred option).
It's common practice to "import numpy as np", so we can use a shorthand in our scripts. We use that convention in the scripts in this post.
<h1>How to load in data with python</h1>
We're going to look at three different ways we can load in data using python. There are many other ways you could do this, but I've tried to pick out three of the most useful.
<h2>1. cvs read</h2>
The first method we'll look at uses the csv module, which is available in the core python install.
This is a powerful and versatile module, and we will only use a small amount of it here, but it shows you how it works in principle.

```python
csv_file = csv.reader(open'data.csv','rb')
```

One of the nice things about this method is that with the column headings also listed as comma separated values, we have no problems importing those directly into our list.
The cvs_read data object is iterable, so we can carry out further processing on it later. In this case we'll just display each line of the list in turn.

```python
for row in csv_file:
    print row
```
Get the code for this example <a href="https://github.com/deparkes/PythonTips/tree/master/LoadDataFiles" target="_blank">here</a>.
<h2>2. numpy.loadtxt</h2>
Next we look at the first of our numpy approaches. Using numpy to load our data has the advantage of being ready to process further with numpy once the data is imported.
numpy.loadtxt is the simplest of the two numpy functions we look at here and offers the fewest options for customisation.

```python
data = np.loadtxt("data.csv", delimiter=',', skiprows=2)
```

We use the skiprows option to tell numpy how many rows of non-data to skip.
The data is loaded in as a numpy array, which can be manipulated with numpy. In this example though we will just print the imported data.
Get the code for this example <a href="https://github.com/deparkes/PythonTips/tree/master/LoadDataFiles" target="_blank">here</a>.
<h2>3. numpy.genfromtxt</h2>
This function, also part of the numpy module, is a more advanced and capable version of loadtxt, above. With this function we have more control over how exactly we import the data, and can deal with some variation in data formats.
This example shows how we might use this function to load data saved as plain text. This data also has two header lines, which might contain user information or a time and data stamp for example.

```python
data = np.genfromtxt("data.csv", dtype=None, delimiter=',', names=True, skip_header=2)
print 'Data\n'
print(data.dtype.names)
print(data)
```

The genfromtxt function can deal with column headings in a way loadtxt cannot.
First we'll use "names=True" to tell the function automatically determines the column headings, which we can access in data.dtype.names.
We can also set the column heading names from within the python script itself by telling the function the name of a list containing the column headings.

```python
names = ["xdata", "y1", "y2", "y3"]
data= np.genfromtxt("data.csv", dtype=None, delimiter=',', names=names, skip_header=0)
print 'Data\n'
print(data.dtype.names)
print(data)
```
Get the code for this example <a href="https://github.com/deparkes/PythonTips/tree/master/LoadDataFiles" target="_blank">here</a>.
<h1>Conclusion</h1>
We've seen three different ways of how to load data into python. There are others, but these give a few simple ways of accessing the data.
Remember: you can access the files used in this article from the PythonTips github <a href="https://github.com/deparkes/PythonTips/tree/master/LoadDataFiles" target="_blank">repository</a>.
</div>
