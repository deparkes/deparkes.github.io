---
layout: post
title: How to find the Centre of a Polygon in Python
date: 2015-02-28 14:34:23.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- centroid
- geometry
- polygon
- shapely
author:
  display_name: deparkes
permalink: "/2015/02/28/how-to-find-the-centre-of-a-polygon-in-python/"
---
Finding the centre of of a polygon can be useful for many geomtrical analysis and processing techniques.
This quick guide shows you how to find the <strong>centre of a polygon</strong> in python.
<h1>The Centroid</h1>
The centre of a polygon is also known as its centroid. It the arithmetic mean position of all the points that make up the polygon.
<a href="{{site.baseurl}}/assets/2015/02/Triangle.Centroid2.png"><img class="aligncenter size-medium wp-image-1435" src="{{site.baseurl}}/assets/2015/02/Triangle.Centroid2-300x241.png" alt="How to find the Centre of a Polygon in Python" width="300" height="241"></a>
<h1>How to find the centre of a polygon in python</h1>
My preferred package for geometry analysis and processing in python is <a href="{{site.baseurl}}/2015/01/29/install-shapely-on-anaconda/">Shapely</a> which happily for us, has a <a href="http://toblerity.org/shapely/manual.html#spatial-analysis-methods"><strong>built-in method </strong></a>for finding the centroid of an object.
We can just use:

```python
mypolygon.centroid
```
This returns a <a href="http://toblerity.org/shapely/manual.html#geometric-objects">shapely POINT object</a>.
This is all well and good, but in most situations we will want to process this further. So we can do a couple of further things to this centroid.
Firstly we can output it in a more readable way:

```python
mypolygon.centroid.wkt
```
('wkt' stands for well known text), which outputs:

```python
'POINT (3.351351351351351 1.897597597597598)'
```
Alternatively we can output the centroid as a pair of coordinates:

```python
mypolygon.centroid.coords
```
('wkt' stands for well known text), which outputs a python list.

```python
[(3.351351351351351, 1.8975975975975976)]
```
Which is much more manageable.

<a href="{{site.baseurl}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.baseurl}}/assets/2015/02/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>
