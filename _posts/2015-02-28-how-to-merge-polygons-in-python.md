---
layout: post
title: How to Merge Polygons in Python
date: 2015-02-28 13:51:24.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- geometry
- shapely
author: deparkes
permalink: "/2015/02/28/how-to-merge-polygons-in-python/"
---
I've been working with the Shapely python package in python. This is a short guide for <strong>how to merge polygons in python</strong>.
This guide is based on "cascaded_union.py" in the shapely examples.
Find out how to install shapely in python <a title="How to install Shapely on Anaconda Python (Windows)" href="{{site.url}}/2015/01/29/install-shapely-on-anaconda/">here</a>.
<h1>How to Merge Polygons in Python</h1>
Download the script for this guide <a href="https://github.com/deparkes/shapely_tests/blob/master/cascaded_union.py">here</a>.
In a most simple sense we can just do something like this to merge polygons:
[code language="python"]
from shapely.geometry import Polygon
from shapely.ops import cascaded_union
polygon1 = Polygon([(0, 0), (5, 3), (5, 0)])
polygon2 = Polygon([(0, 0), (3, 10), (3, 0)])
polygons = [polygon1, polygon2]
u = cascaded_union(polygons)
[/code]
This will produce a merged polygon "u".
Let's build on this to <strong>plot</strong> the original polygons, <strong>merge</strong> them, and then <strong>plot the merged polygon</strong>, too.
First, <strong>plot the original polygons</strong>:

```python
# plot these two polygons separately
fig = plt.figure(1, figsize=SIZE, dpi=90)
ax = fig.add_subplot(111)
poly1patch = PolygonPatch(polygon1, fc=BLUE, ec=BLUE, alpha=0.5, zorder=2)
poly2patch = PolygonPatch(polygon2, ec=BLUE, alpha=0.5, zorder=2)
ax.add_patch(poly1patch)
ax.add_patch(poly2patch)
xrange = [-2, 12]
yrange = [-2, 8]
ax.set_xlim(*xrange)
ax.set_xticks(range(*xrange) + [xrange[-1]])
ax.set_ylim(*yrange)
ax.set_yticks(range(*yrange) + [yrange[-1]])
ax.set_aspect(1)
```
Which gives us this output:

| ![Two polygons to merge]({{site.url}}/assets/2015/02/MergePolygons2.png) |
|:--:|
| *Two polygons to merge* |

Now merge the two polygons and plot them:

```python
# Make the merged polygons
u = cascaded_union(polygons)
# Make new figure for the merged polygon
fig2 = plt.figure(2, figsize=SIZE, dpi=90)
ax2 = fig2.add_subplot(111)
patch2b = PolygonPatch(u, fc=BLUE, ec=BLUE, alpha=1, zorder=2)
ax2.add_patch(patch2b)
xrange = [-2, 12]
yrange = [-2, 8]
ax2.set_xlim(*xrange)
ax2.set_xticks(range(*xrange) + [xrange[-1]])
ax2.set_ylim(*yrange)
ax2.set_yticks(range(*yrange) + [yrange[-1]])
ax2.set_aspect(1)
fig2.show(2)
```
Which gives us the output:

| ![Merged polygons]({{site.url}}/assets/2015/02/MergePolygons3-300x220.png) |
|:--:|
| *Merged polygons* |

Get the python file for this guide <a href="https://github.com/deparkes/shapely_tests/blob/master/cascaded_union.py">here</a>.


<a href="{{site.url}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.url}}/assets/2015/02/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>
