---
layout: post
title: Seaborn Python Plotting Library
date: 2015-05-05 19:36:41.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- python
tags:
- data visualisation
- plotting
- python
- seaborn
author:
  display_name: deparkes
permalink: "/2015/05/05/seaborn-python-plotting-library/"
---
I've recently been looking into python packages that could help improve the appearance of <a href="http://matplotlib.org/">matplotlib </a>- the venerable, go-to plotting library for Python. For quickly plotting some data vanilla matplotlib generally does just fine, but for truly 'publication-ready' plots, you'll probably want to look to one of the more advanced libraries.
In this post a take a quick look at the <a href="http://stanford.edu/~mwaskom/software/seaborn/">Seaborn </a>python plotting library. Seaborn is a broad and <a href="http://stanford.edu/~mwaskom/software/seaborn/introduction.html">powerful package</a>, so you should check it out for yourself to <a href="http://stanford.edu/~mwaskom/software/seaborn/examples/index.html">see what it can really do</a>, but hopefully this post will give you a taste, and possibly inspire you to give it a go yourself.
Primarily developed by researchers at <a href="https://www.stanford.edu/">Stanford University</a>, Seaborn builds on matplotlib, so your existing plotting code should for the most part already be compatible. It's also well integrated with <a href="{{site.baseurl}}/2015/04/05/python-pandas-for-physics/">Pandas</a>, a data structure and analysis library for python. Seaborn is still very much in <a href="https://github.com/mwaskom/seaborn">active development</a>, so you can expect a few bugs, but also rapid bug fixes and new features.
Many of the features of Seaborn are aimed at <a href="http://stanford.edu/~mwaskom/software/seaborn/introduction.html">advanced statistical processin</a>g and plotting, but even basic usage can help deliver <strong>better looking plots</strong>.
<h3><a href="http://stanford.edu/~mwaskom/software/seaborn/tutorial.html">Take things further with the Seaborn tutorial</a></h3>
I'm going to be modifying the <a href="http://matplotlib.org/users/pyplot_tutorial.html">multiple plot example</a> from the matplotlib documentation. First of all let's look at the default matplotlib output:

| ![seaborn python  matplotlib default]({{site.baseurl}}/assets/2015/05/defaults.png) |
|:--:|
| *seaborn python  matplotlib default* |

And now let's see what happens when we import the Seaborn package. Although Seaborn has its own <a href="http://stanford.edu/~mwaskom/software/seaborn/tutorial/plotting_distributions.html">plot types</a>, its styles can be applied equally well to the standard matplotlib plots. To turn on the Seaborn styles, you just need to import the module:

```python
import seaborn as sns
```
Here's the Seaborn output.

| ![seaborn python - seaborn]({{site.baseurl}}/assets/2015/05/seaborn.png) |
|:--:|
| *seaborn python - seaborn* |



If you're not too keen on the grey background, we can easily change from the default grey background, to a more conventional white with the command
```python
sns.set_style("whitegrid")
```


| ![seaborn python - whitegrid]({{site.baseurl}}/assets/2015/05/whitegrid.png) |
|:--:|
| *seaborn python - whitegrid* |

Another nice touch is the use of '<strong>contexts</strong>' which you can use to set and save appearance parameters. The standard ones are notebook (the default), poster, talk, and paper context.
Here's an example of the 'paper' context, which makes the plot more compact, so as to fit better into a paper.

| ![seaborn python - paper]({{site.baseurl}}/assets/2015/05/paper_context.png) |
|:--:|
| *seaborn python - paper* |

One final cool feature I'd like to point out is the broad range of colours and <a href="http://stanford.edu/~mwaskom/software/seaborn/tutorial/color_palettes.html">colour palettes</a> available, including the <a href="http://xkcd.com/color/rgb/">954 named colours</a> produced by the<a href="http://blog.xkcd.com/2010/05/03/color-survey-results/"> xkcd colour survey</a>.
