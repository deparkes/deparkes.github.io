---
layout: post
title: How to Find the Concave Hull in Python
date: 2015-02-01 10:25:57.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- geometry
- python
author:
  display_name: deparkes
permalink: "/2015/02/01/find-concave-hull-python/"
---
<h1>How to Find the Concave Hull in Python</h1>
The Python module <a href="https://pypi.python.org/pypi/Shapely">Shapely </a>has a built in function for determining the <strong>convex hull</strong>, but for determining the <strong>concave hull </strong>(or <a href="http://en.wikipedia.org/wiki/Alpha_shape">alpha shape</a>), you have to do a bit more work.
Thankfully a few people on the internet have already done much of the work in determining the concave hull of a shape.
For me the starting point was this <a href="http://sgillies.net/blog/1155/the-fading-shape-of-alpha/">blog post </a>post, which uses <a href="http://en.wikipedia.org/wiki/Circumscribed_circle#Triangles">circumscribing </a>of the <a href="http://en.wikipedia.org/wiki/Polygon_triangulation">triangulation</a> of the starting polygon. It uses a few functions introduced in this <a href="http://stackoverflow.com/questions/6537657/python-scipy-delaunay-plotting-point-cloud">StackOverflow answer</a>.
This <a href="http://blog.thehumangeo.com/2014/05/12/drawing-boundaries-in-python/">blog post</a> develops those ideas further, and fills in some of the blanks in the original code. Rather handily, it's also available as an <a href="http://ipython.org/notebook.html">IPython Notebook</a>.
Image:  <span class="mw-mmv-source-author"><span class="mw-mmv-author"><a title="User:Kku" href="http://commons.wikimedia.org/wiki/User:Kku">Kku</a></span>; <a class="mw-mmv-license" href="http://creativecommons.org/licenses/by-sa/4.0" target="_blank">CC BY-SA 4.0</a></span>


<a href="{{site.baseurl}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.baseurl}}/assets/2015/02/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>