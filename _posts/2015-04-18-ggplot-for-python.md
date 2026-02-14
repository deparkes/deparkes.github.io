---
layout: post
title: ggplot for Python
date: 2015-04-18 12:59:48.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- python
tags:
- data analysis
- plotting
- visualisation
author: deparkes
permalink: "/2015/04/18/ggplot-for-python/"
---
<h1>ggplot for Python</h1>
The ggplot library for python unlocks much of the philosophy and pretty graphics of ggplot2 for R. Try it out and make your data look nicer.
<h2>Bringing ggplot to Python</h2>
One of the 'killer apps' of the <a href="https://www.r-project.org/">statistics package R</a> is <a href="https://ggplot2.org/">ggplot2</a>, a plotting library based on the book The Grammar of Graphics, that takes the hassle and fiddle out of creating nice looking graphs and graphics.

Although there are powerful plotting libraries for python (<a href="https://matplotlib.org/">matplotlib </a>being the main one) , they don't have the same approach and pretty output as ggplot2 for R.
Thankfully a <a href="https://github.com/yhat/ggplot">version of ggplot for python</a> is in development so you can access the power and flexibility of ggplot2 in your python data analysis.
<h2>Using ggplot To Improve Plotting</h2>
There are plenty of places you can see a <a href="https://blog.yhathq.com/posts/ggplot-for-python.html">complete comparison</a> of the R vs python ggplot implementations, so I'll just give you a quick flavour of what to expect.
I recently plotted data about <a title="Pizza Price Comparison – Where Should You Buy Your Pizza?" href="{{site.url}}/2015/04/16/pizza-price-comparison-where-should-you-buy-your-pizza/">pizza prices</a>. Using straight matplotlib, the output graph looks like this:

| ![pizza price comparison - price vs diameter]({{site.url}}/assets/2015/04/PriceVsDiameter-1024x632.png) |
|:--:|
| *pizza price comparison - price vs diameter* |

Which certainly does the job, but I'm not sure I'd go as far to say that it was <em>pretty</em>.
To try and improve things, let's use ggplot for python:

```python
ggplot(prices, aes(x='Diameter', y='Price',color="establishment_name")) +\
    geom_line() + geom_point()
```
which creates the much nicer output:

| ![ggplot for python - ggplot prices]({{site.url}}/assets/2015/04/pizza_prices_price_ggplot.png) |
|:--:|
| *ggplot for python - ggplot prices* |

Clearly a much more artistic representation!
To be honest though I'm not sure the project is quite mature enough for met at the moment. There are one or two features and elements that aren't quite there yet, and I am having some trouble replicating exactly the features that I want in my graphs.
Going by the <a href="https://github.com/yhat/ggplot">github project page</a>, development does seem to have slowed of late, but I'm going to keep a keen eye on progress as the project shows so much promise.
In the mean time I'll make do with the rather nifty <a href="https://matplotlib.org/users/style_sheets.html">ggplot2 style for matplotlib</a>.
To use it just add this line to your code:
```python
plt.style.use('ggplot')
```
You don't get any of the usability and 'Grammar of Graphics' philosophy, but your graphs and plots do end up looking rather nice:

| ![ggplot for python - style]({{site.url}}/assets/2015/04/pizza_prices_matplotlib_style.png) |
|:--:|
| *ggplot for python - style* |

