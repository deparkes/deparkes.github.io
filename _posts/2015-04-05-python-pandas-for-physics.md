---
layout: post
title: Python Pandas for Physics
date: 2015-04-05 07:56:57.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- data
- python
tags:
- analysis
- data
- pandas
- python
author:
  display_name: deparkes
permalink: "/2015/04/05/python-pandas-for-physics/"
---
<h1>Python Pandas for Physics</h1>
The <a href="https://pandas.pydata.org/">Pandas package</a> brings advanced data structures and data analysis tools to python. It was initially concieved for use in the world of finance, but can it be of any use to us interested in physics?
For some time I've been trying to get to the stage that I can use python for all my scripting and data analysis, replacing programs like <a href="https://uk.mathworks.com/products/matlab/">Matlab </a>and <a href="https://www.originlab.com/">Origin</a>. I've found <a title="3 Python Alternatives to Matlab" href="{{site.baseurl}}/2015/02/28/python-alternatives-to-matlab/">python distributions</a> that have a similar development environment to Matlab, and the search is now on for packages that simplify the process of data analysis, manipulation and visualisation.
My needs are relatively modest: I don't need to do much more than <strong>load, manipulate </strong>and<strong> plot small data files</strong>. I wonder if such a powerful package as pandas can also satisfy these requirements.
<h3><a href="https://pandas.pydata.org/pandas-docs/stable/">Get the Pandas Python Package</a></h3>
You might also want to consider the <a title="The Stoner Python Package" href="{{site.baseurl}}/2015/02/17/the-stoner-python-package/">Stoner python package</a> - a 'home-grown' analysis package made at the university of Leeds. It's not as polished or well supported as pandas, but it was built from the ground up as a physics analysis package.
<h1>Pandas For Physics</h1>
Much of the power of pandas comes from its '<a href="https://pandas.pydata.org/pandas-docs/dev/generated/pandas.DataFrame.html">DataFrame</a>' data structure. The columns of this 2d table can be labelled, and contain different data types.
To explore how it might be useful, I've run through a few common tasks I've encountered in physics research. For this I'm using the <a title="3 Python Alternatives to Matlab" href="{{site.baseurl}}/2015/02/28/python-alternatives-to-matlab/">Anaconda python distribution</a>.
<h3><a href="https://gist.github.com/deparkes/d76b093a034d496ea196">For the impatient: Get the gist of this post on github</a></h3>
<h2>Loading data (from csv)</h2>
More or less any analysis task begins with loading from a data file. I've <a title="Python Tips: How to Load Data Into Python" href="{{site.baseurl}}/2014/11/23/how-to-load-data-into-python/">previously </a>tried to find a simple. standard way to load data into python, but pandas seems to be one of the simplest so far:

```python
mydata = pd.read_csv('data.dat')
```

<strong><a href="https://pandas.pydata.org/pandas-docs/dev/io.html">More on loading data with pandas.</a></strong>
<h2>Display Columns</h2>
Once we've loaded the file into our python session, we can display it very easily too:

```python
print(mydata.head())
```

The ".head()" just shows the first 5 lines of our data - useful if we are trying to read a large file!
<h2>Simple Statistics</h2>
It's also a quick job to output basic statistics about the different columns of data in our file:

```python
print(mydata.describe())
```

which will output statistics like mean, standard deviation, maximum and minimum, etc.
<h2>Plot Your Data</h2>
Plotting data is crucial to any data analysis package. Pandas utilises on the matplotlib plotting package, and as with the other examples we've seen, plotting is very easy:

```python
fig = plt.figure()
mydata.plot(x='x column', y='y column', style='-')
```

We select which columns to plot using the column heading labels. This makes it very easy to keep track of exactly which data we are plotting.
<strong><a href="https://pandas.pydata.org/pandas-docs/dev/visualization.html">More on Plotting with Pandas</a></strong>
<h2>Add New Column</h2>
It's all well and good being able to load and view existing data, but also important is being able to add new columns.
In this example I add a new column to an existing data frame. I create a new column filled with data made by finding the cosine of an angle defined in an existing column. We define in advance the function to apply to the data in the first column.

```python
def dcos(theta):
    theta = theta*(math.pi/180)
    return math.cos(theta)
mydata['New Column1'] = pd.Series(mydata["Theta"].apply(dcos), index=mydata.index)
```

<strong><a href="https://synesthesiam.com/posts/an-introduction-to-pandas.html#bulk-operations-with-apply">More on adding new columns to a Pandas data frame</a></strong>
<h2>Save Data to A File</h2>
As with reading from a file, writing to a file is very easy with pandas:

```python
mydata.to_csv('Newcsv.dat')
```
really easy to do, data comes out really nicely.
<strong><a href="https://pandas.pydata.org/pandas-docs/dev/generated/pandas.DataFrame.to_csv.html">More on saving data frames to a file.</a></strong>
<h1>Pandas Tutorials</h1>
I've gone through a few of the simpler tasks you might need, but to really explore what Pandas could do for you, you should <a href="https://pandas.pydata.org/pandas-docs/stable/">download it </a>and have a go yourself. Pandas is well supported, and well documented, so you'll be able to find plenty of examples to help you out.
Here are a few guides to help get you started:
- <a href="https://pandas.pydata.org/pandas-docs/dev/basics.html">https://pandas.pydata.org/pandas-docs/dev/basics.html</a>
- <a href="https://pandas.pydata.org/pandas-docs/dev/10min.html">https://pandas.pydata.org/pandas-docs/dev/10min.html</a>
- <a href="https://pandas.pydata.org/pandas-docs/dev/cookbook.html#cookbook">https://pandas.pydata.org/pandas-docs/dev/cookbook.html#cookbook</a>
- <a href="https://www.gregreda.com/2013/10/26/working-with-pandas-dataframes/">https://www.gregreda.com/2013/10/26/working-with-pandas-dataframes/</a>
- <a href="https://synesthesiam.com/posts/an-introduction-to-pandas.html">https://synesthesiam.com/posts/an-introduction-to-pandas.html</a> (This one was particularly helpful)
