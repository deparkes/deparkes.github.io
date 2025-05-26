---
layout: post
title: Matplotlib XKCD Style Plots
date: 2018-04-16 15:30:59.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Data Science
tags:
- chart
- data
- data visualisation
- graph
- matplotlib
- plotting
- python
- visualisation
- xkcd
author:
  display_name: deparkes
permalink: "/2018/04/16/matplotlib-xkcd-style-plots/"
---
Matplotlib is the excellent workhorse plotting library for python. As great as matplotlib is, it could occasionally do with a little stylistic improvement <a href="{{site.baseurl}}/2015/05/05/seaborn-python-plotting-library/">[1]</a> [<a href="{{site.baseurl}}/2015/04/18/ggplot-for-python/">2]</a>. I recently came across a cool feature in <a href="https://matplotlib.org/api/_as_gen/matplotlib.pyplot.xkcd.html">matplotlib</a> that lets you plot in the style of the popular <a href="https://www.xkcd.com/">XKCD</a> comics, with a fun font and a more 'sketchy' line style.

Using xckd-style plots is <a href="https://www.chrisstucchio.com/blog/2014/why_xkcd_style_graphs_are_important.html">not just for fun</a>. You can use the xkcd style when you want to emphasise the uncertainty in your modelling or analysis. They look so unofficial that your audience or reader will have to question if your analysis is correct or not.
<h1>Matplotlib XKCD Style Plots</h1>
Matplotlib XKCD style plots are easy to create - it is as simple as including 'plt.xkcd()' at the start of your plotting script. For example:

```python
from matplotlib import pyplot as plt
import numpy as np
from scipy.stats import norm
plt.xkcd():
x_axis = np.arange(-10, 10, 0.001)
mu = 0
variance = 1
plt.plot(x_axis, norm.pdf(x_axis,mu,variance))
plt.xlabel('X VALUES')
plt.ylabel('Y VALUES')
plt.title('NORMAL DISTRIBUTION')
plt.show()
```

Which should output this

| ![Matplotlib XKCD Style - xkcd]({{site.baseurl}}/assets/2018/04/xkcd_normal.png) |
|:--:|
| *Matplotlib XKCD Style - xkcd* |

<h1>More Control Over XKCD Plots</h1>
You will find that once you have included plt.xkcd() in your scripts <em>all</em> of your plots in that session will have an xkcd style. To have a bit more control over the xkcd style, you can use 'with plt.xkcd()' instead. For example.

```python
from matplotlib import pyplot as plt
import numpy as np
from scipy.stats import norm
# An xkcd-style plot
with plt.xkcd():
    x_axis = np.arange(-10, 10, 0.001)
    mu = 0
    variance = 1
    plt.plot(x_axis, norm.pdf(x_axis,mu,variance))
    plt.xlabel('X VALUES')
    plt.ylabel('Y VALUES')
    plt.title('NORMAL DISTRIBUTION')
    plt.show()
# The same plot with matplotlib defaults
x_axis = np.arange(-10, 10, 0.001)
mu = 0
variance = 1
plt.plot(x_axis, norm.pdf(x_axis,mu,variance))
plt.xlabel('X VALUES')
plt.ylabel('Y VALUES')
plt.title('NORMAL DISTRIBUTION')
plt.show()
```

This code will produce two plots of the same data, but with different styles. The second one will use matplotlib defaults and look more like this:

| ![Matplotlib XKCD Style - defaults]({{site.baseurl}}/assets/2018/04/xkcd_defaults.png) |
|:--:|
| *Matplotlib XKCD Style - defaults* |

<h1>Improve the Text</h1>
To improve the appearance (or at least make it more like XKCD), you can install the font '<a href="https://github.com/shreyankg/xkcd-desktop/blob/master/Humor-Sans.ttf">Humor Sans</a>'. After you install the Humor Sans font you might find that matplotlib cannot find it immediately. To help things you can reset the matplotlib font manager with:

```python
import matplotlib
matplotlib.font_manager._rebuild()
```

