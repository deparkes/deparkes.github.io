---
layout: post
title: Python GPX Import Coordinates
date: 2016-05-20 15:00:23.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
- python
tags:
- coordinates
- gis
- gps
- mapping
- python
author: deparkes
permalink: "/2016/05/20/python-gpx-import/"
---
Gpx (<a href="https://en.wikipedia.org/wiki/GPS_Exchange_Format">GPS Exchange Format</a>) is a common file format used to store exported GPS data. In this post I use the python module <a href="https://pypi.python.org/pypi/gpxpy/1.1.1">gpxpy </a>to simply import the gpx coordinates from a gpx file.

<h1>Python GPX Import Made Easy With gpxpy</h1>
A Python GPX import is made a lot easier with the <a href="https://pypi.python.org/pypi/gpxpy/1.1.1">gpxpy </a>package, which does the hard work of parsing the GPX file is done by gpxpy:
```python
import gpx.py
import gpx.gpx
gpx = gpxpy.parse(gpx_file)
points = []
for track in gpx.tracks:
    for segment in track.segments:
        for point in segment.points:
            points.append([point.latitude, point.longitude])
```
Which gives us a list containing the points of latitude and longitude, representing the trackpoints in our route.
<h1>Visualise With Folium</h1>
We can visualise our list of coordinates with <a href="https://wp.me/p4DE9r-FU">Folium </a>- check out the code for this map <a href="https://gist.github.com/deparkes/610b112f74eadbda663806ba8dd83069">here</a>.
We can see that in this case the GPX coordinates represent movement around two areas of London.

<iframe src="{{site.url}}/assets/maps/gpx_example.html.1" name="FRAME2" width="450" height="400" frameborder="1"></iframe>

<h3><a href="https://github.com/tkrajina/gpxpy">Find more examples on the gpxpy github page</a></h3>
