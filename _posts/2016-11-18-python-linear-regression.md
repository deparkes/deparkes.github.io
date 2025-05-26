---
layout: post
title: Python Linear Regression
date: 2016-11-18 15:00:34.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- python
tags:
- data
- linear regression
- python
- scipy
- sklearn
- statsmodels
author:
  display_name: deparkes
permalink: "/2016/11/18/python-linear-regression/"
---
A few ways to do <a href="https://en.wikipedia.org/wiki/Ordinary_least_squares">linear regressions</a> on data in python. <a href="https://en.wikipedia.org/wiki/Ordinary_least_squares">Linear regression</a> is a simple and common technique for modelling the relationship between dependent and independent variables. This post gives you a few examples of Python linear regression libraries to help you analyse your data.
Which method is best for  you will probably depend on exactly what you are doing. The scipy method is a bit more 'bare-bones'; the statsmodels method is part of an extensive "traditional" statistics module; while the sklearn approach would probably be best if you are working on a larger machine learning project.
<h4><a href="{{site.baseurl}}/2016/11/11/python-sample-datasets/">Read more about how to load sample datasets into python</a></h4>
<h1>Method 1: Scipy</h1>
Scipy is a python analysis ecosystem that encapsulates a few different libraries such as <a href="http://www.numpy.org/">numpy </a>and <a href="http://matplotlib.org/">matplotlib</a>. Here I've picked out two approaches you could use: linregress and polyfit
<h2>With linregress</h2>
Firstly I'll use the '<a href="http://scipy-cookbook.readthedocs.io/items/LinearRegression.html">linregress</a>' linear regression function.

```python
# load iris sample dataset
import seaborn.apionly as sns
iris = sns.load_dataset('iris')
# import scipy
from scipy import polyval, stats
fit_output = stats.linregress(iris["petal_length"], iris["petal_width"])
slope, intercept, r_value, p_value, slope_std_error = fit_output
print(slope, intercept)
```

To estimate y-values using these fitting parameters we can use the scipy/numpy '<a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.polyval.html">polyval</a>' function:

```python
# use scipy polyval to create y-values from x_data and the
# linregress fit parameters
scipy_fitted_y_vals = polyval([slope,intercept],iris["petal_length"])
```

Which we can plot along with the original data

```python
import matplotlib.pyplot as plt
axes = iris.plot(x="petal_length", y="petal_width", kind="scatter", color="red")
plt.plot(iris["petal_length"], scipy_fitted_y_vals, color='black', linewidth=3)
plt.show()
```

| ![python linear regression - linregress]({{site.baseurl}}/assets/2016/11/red_dots.png) |
|:--:|
| *python linear regression - linregress* |

<h2>With polyfit</h2>
While still using scipy, you can also use the <a href="https://docs.scipy.org/doc/numpy/reference/generated/numpy.polyfit.html">polyfit </a>function. As its name suggests it can be used to fit higher order polynomials, but here we'll just use it for a linear regression:

```python
form scipy import polyfit
# fit with scipy polyfit
(slope, intercept) = polyfit(iris["petal_length"], iris["petal_width"], 1)
scipy_fitted_y2 = polyval([slope, intercept], iris["petal_length"])
import matplotlib.pyplot as plt
axes = iris.plot(x="petal_length", y="petal_width", kind="scatter", color="green")
plt.plot(iris["petal_length"], scipy_fitted_y2, color='black', linewidth=3)
plt.show()
```

| ![python linear regression - polyfit]({{site.baseurl}}/assets/2016/11/green_dots.png) |
|:--:|
| *python linear regression - polyfit* |


<h1>Method 2: statsmodels</h1>
<a href="http://statsmodels.sourceforge.net/devel/index.html">statsmodels </a>is a python module dedicated to statistcal modelling and testing. statsmodels has many advanced fitting and regression libraries, as well as simpler ones like <a href="http://statsmodels.sourceforge.net/devel/examples/#regression">linear regression</a>.
One important way that statsmodels differs from other regression modules is that it <a href="http://stackoverflow.com/questions/20701484/why-do-i-get-only-one-parameter-from-a-statsmodels-ols-fit">doesn't</a> automatically add a constant intercept to the regression - <a href="http://stackoverflow.com/questions/38836465/how-to-get-the-regression-intercept-using-statsmodels-api">we need to do that ourselves</a>.

```python
# load iris sample dataset
import seaborn.apionly as sns
iris = sns.load_dataset('iris')
import statsmodels.api as sm
# fit with statsmodels
# add constant intercept
X = sm.add_constant(iris["petal_length"])
model = sm.OLS(iris["petal_length"], X)
results = model.fit()
statsmodels_y_fitted = results.predict()
```

With statsmodels you can also print out a comprehensive report on fit:

```python
print(results.summary())
```

which gives this output
```
                            OLS Regression Results
==============================================================================
Dep. Variable:                      y   R-squared:                       0.927
Model:                            OLS   Adj. R-squared:                  0.927
Method:                 Least Squares   F-statistic:                     1882.
Date:                Sat, 12 Nov 2016   Prob (F-statistic):           4.68e-86
Time:                        11:08:10   Log-Likelihood:                 24.796
No. Observations:                 150   AIC:                            -45.59
Df Residuals:                     148   BIC:                            -39.57
Df Model:                           1                                         
Covariance Type:            nonrobust                                         
================================================================================
                   coef    std err          t      P&gt;|t|      [95.0% Conf. Int.]
--------------------------------------------------------------------------------
const           -0.3631      0.040     -9.131      0.000        -0.442    -0.285
petal_length     0.4158      0.010     43.387      0.000         0.397     0.435
==============================================================================
Omnibus:                        5.765   Durbin-Watson:                   1.455
Prob(Omnibus):                  0.056   Jarque-Bera (JB):                5.555
Skew:                           0.359   Prob(JB):                       0.0622
Kurtosis:                       3.611   Cond. No.                         10.3
==============================================================================
```
And also plot our data along with the regression line:

```python
import matplotlib.pyplot as plt
axes = iris.plot(x="petal_length", y="petal_width", kind="scatter", color="yellow")
plt.plot(iris["petal_length"], results.predict(), color='black', linewidth=3)
plt.show()
```

| ![python linear regression - statsmodels]({{site.baseurl}}/assets/2016/11/yellow_dots.png) |
|:--:|
| *python linear regression - statsmodels* |

<h1>Method 3: scikit-learn</h1>
This final examples use scikit-learn, a python library which implements a range of machine learning tools for data analysis - including <a href="http://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html#sklearn.linear_model.LinearRegression.fit">linear regression</a>.
scikit-learn (sklearn) is built around numpy arrays rather than pandas dataframes. <a href="http://stackoverflow.com/questions/38105539/how-to-convert-a-scikit-learn-dataset-to-a-pandas-dataset">To get around</a> this we can <a href="http://stackoverflow.com/questions/35723472/how-to-use-sklearn-fit-transform-with-pandas-and-return-dataframe-instead-of-num">reshape </a>the '.values' outputs from the dataframe columns. Once the data is reshaped, the regression is done in much the same way to my other examples.

```python
from sklearn import datasets, linear_model
import pandas as pd
import matplotlib.pyplot as plt
# Reshape dataframe values for sklearn
fit_data = iris[["petal_length", "petal_width"]].values
x_data = fit_data[:,0].reshape(-1,1)
y_data = fit_data[:,1].reshape(-1,1)
# Create linear regression object
regr = linear_model.LinearRegression()
# once the data is reshaped, running the fit is simple
regr.fit(x_data, y_data)
# we can then plot the data and out fit
axes = iris.plot(x="petal_length", y="petal_width", kind="scatter")
plt.plot(x_data, regr.predict(x_data), color='black', linewidth=3)
plt.show()
```

| ![python linear regression - sklearn]({{site.baseurl}}/assets/2016/11/blue_dots.png) |
|:--:|
| *python linear regression - sklearn* |
