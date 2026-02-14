---
layout: post
title: Python Leaflet Map With Folium
date: 2016-05-13 15:00:49.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- data
- GIS
tags:
- data
- data science
- folium
- gis
- mapping
- python
author: deparkes
permalink: "/2016/05/13/python-leaflet-map-folium/"
---
<a href="https://leafletjs.com/">Leaflet </a>is a powerful Javascript library for interactive maps. I've wanted to have a go at using Leaflet for a while, but learning Javascript for just one library seemed over the top. Thankfully I've recently found <a href="https://pypi.python.org/pypi/folium">Folium </a>- a python package that makes it easy to produce a Python Leaflet map.
<h1>A Simple Python Leaflet Map</h1>
Here's a simple example of the kind of map that is possible in Leaflet (taken from a <a href="https://wp.me/p4DE9r-FE">post</a> of mine). This example has a base layer of an
<a href="https://www.openstreetmap.org/#map=5/51.500/-0.100">OpenStreetMap</a> map centred on Colchester in the UK. Overlaid on the map are some markers, which when you click on them reveal a label indicating the location of the marker (in this case public toilets).

<iframe src="{{site.url}}/assets/maps/colch_toilets.html" name="colch_toilets" width="450" height="400" frameborder="1"></iframe>

Find out more about this map, and download the python code <a href="https://wp.me/p4DE9r-FE">here</a>.
<h1>How to Install Folium</h1>
For a full install guide visit the <a href="https://folium.readthedocs.org/en/latest/#">Folium docs</a>, but to get you going you can just run

```
pip install folium
```

Creating a map is then simple:

```python
import folium
map_osm = folium.Map(location=[45.5236, -122.6750])
map_osm.save('london.html')
```

which saves a map that looks a bit like this:

<iframe src="{{site.url}}/assets/maps/london.html" name="london" width="450" height="400" frameborder="1"></iframe>

Visit the <a href="https://pypi.python.org/pypi/folium">Folium Getting Started guide</a> for more tips to get you going.
<h1>Folium Features</h1>
Visit the <a href="https://pypi.python.org/pypi/folium">Folium pypi page </a>for more about its features. You can also find a features library filled with examples <a href="https://nbviewer.jupyter.org/github/python-visualization/folium/tree/master/examples/">here </a>and <a href="https://nbviewer.jupyter.org/github/ocefpaf/folium_notebooks/tree/master/">here</a>.
Folium is still very much under development, so also check out the project's <a href="https://github.com/python-visualization/folium">github page </a>for more updates and information.
