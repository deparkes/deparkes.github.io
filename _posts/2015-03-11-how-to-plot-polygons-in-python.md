---
layout: post
title: How to Plot Polygons in Python
date: 2015-03-11 21:34:49.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- plotting
- polygon
- polygons
- shapely
author:
  display_name: deparkes
permalink: "/2015/03/11/how-to-plot-polygons-in-python/"
---
<h1>How to Plot Polygons In Python</h1>
This post shows you<strong> how to plot polygons in Python</strong>. When you're working with polygons it can be useful to be able to plot them - perhaps to check that your operation has worked as expected, or to display a final result.
The process to plot polygons in python can be different depending on whether you are happy to plot<strong> just the edges</strong> of the polygon, or you would also like to plot the<strong> area enclosed</strong> by the polygon.


<h1>Plot Polygon Edges</h1>

| ![Plot Polygons in Python - empty]({{site.baseurl}}/assets/2015/03/PolygonEdges-291x300.png) |
|:--:|
| *Plot Polygons in Python - empty* |

If you only want to <strong>plot the edges</strong> of the polygon things are quite simple. We can just <strong>extract the x and y coordinates</strong> and plot them using the <a href="http://matplotlib.org/">matplotlib plotting library</a>.

I've simplified the shapely example<a href="https://github.com/Toblerity/Shapely/blob/master/docs/code/linearring.py"> linearring.py</a> to do this.
 
<h3><a href="https://github.com/deparkes/shapely_tests/blob/master/PolyPrint.py">Download the code for plotting the edges of polygons</a></h3>
<h2>Import Modules</h2>
First we need to import the necessary modules:
```python
from matplotlib import pyplot
from shapely.geometry.polygon import LinearRing, Polygon
```

<h2>Extract Polygon Coordinates</h2>
How exactly you extract the x and y coordinates depends on exactly what type of polygon you are using. In shapely a <strong>polygon</strong> object and a <strong>linearring</strong> object are very similar, but do differ in how we treat them.
<h3>Polygon Object</h3>
How to extract the x and y coordinates from a shapely <a href="http://toblerity.org/shapely/manual.html#polygons">Polygon </a>object.

```python
poly = Polygon([(0, 0), (0, 2), (1, 1),
    (2, 2), (2, 0), (1, 0.8), (0, 0)])
x,y = poly.exterior.xy
```

<h3>LinearRing Object</h3>
How to extract the x and y coordinates from a shapely <a href="http://toblerity.org/shapely/manual.html#linearrings">LinearRing </a>object.

```python
ring = LinearRing([(0, 0), (0, 2), (1, 1),
    (2, 2), (2, 0), (1, 0.8), (0, 0)])
x, y = ring.xy
```

<h2>Plot the Polygon</h2>
Having extracted the x and y coordinates, we can <strong>plot the polygon</strong> with matplotlib:

```python
ax = fig.add_subplot(111)
ax.plot(x, y, color='#6699cc', alpha=0.7,
    linewidth=3, solid_capstyle='round', zorder=2)
ax.set_title('Polygon')
```


<h3><a href="https://github.com/deparkes/shapely_tests/blob/master/PolyPrint.py">Download the code for plotting the edges of polygons</a></h3>
<h1>Plot A Filled Polygon</h1>
<a href="{{site.baseurl}}/assets/2015/03/FilledPolygon1.png"><img class=" alignleft wp-image-1546" src="{{site.baseurl}}/assets/2015/03/FilledPolygon1-291x300.png" alt="" width="221" height="228"></a>If you want to <strong>plot the filled area</strong> of the polygon, and not just the edges, you have to go a bit further.
We'll be using the same libraries as before, with the addition of <a href="https://pypi.python.org/pypi/descartes">descartes</a>, which helps us to<strong> plot geometric objects</strong> with <a href="http://matplotlib.org/users/path_tutorial.html">matplotlib patches</a>.
This is a simplified version of the <a href="https://github.com/Toblerity/Shapely/blob/master/docs/code/cascaded_union.py">cascaded_union.py </a>shapely example.
<h3><a href="https://github.com/deparkes/shapely_tests/blob/master/FilledPolygonPlot.py">Download the code for plotting filled polygons</a></h3>

```python
from matplotlib import pyplot as plt
from shapely.geometry.polygon import Polygon
from descartes import PolygonPatch
```

And now we <strong>plot the polygon</strong> by generating and plotting a <strong>matplotlib patch</strong>:

```python
fig = plt.figure(1, figsize=(5,5), dpi=90)
ring_mixed = Polygon([(0, 0), (0, 2), (1, 1),
    (2, 2), (2, 0), (1, 0.8), (0, 0)])
ax = fig.add_subplot(111)
ring_patch = PolygonPatch(ring_mixed)
ax.add_patch(ring_patch)
```

This will plot the polygon, but we'll also do a few things to <strong>make it look nicer</strong>:

```python
ax.set_title('General Polygon')
xrange = [-1, 3]
yrange = [-1, 3]
ax.set_xlim(*xrange)
ax.set_xticks(range(*xrange) + [xrange[-1]])
ax.set_ylim(*yrange)
ax.set_yticks(range(*yrange) + [yrange[-1]])
ax.set_aspect(1)
```

<h3><a href="https://github.com/deparkes/shapely_tests/blob/master/FilledPolygonPlot.py">Download the code for plotting filled polygons</a></h3>
<a href="{{site.baseurl}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.baseurl}}/assets/2015/03/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>
