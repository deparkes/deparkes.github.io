---
layout: post
title: Python OSGB to WGR84
date: 2016-05-27 15:00:58.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
- python
tags:
- conversion
- coordinates
- latlon
- map
- mapping
- obgr
- python
- wgr84
author:
  display_name: deparkes
permalink: "/2016/05/27/python-osgb-to-wgr84/"
---
<a href="https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid">OSGB </a>is the Ordnance Survey National Grid and is used for many grid references in the United Kingdom. This grid system works well for locations within the United Kingdom, but needs work if you need to combine coordinates from another system, or perhaps <a href="http://wp.me/p4DE9r-FE">plot locations on open streetmap</a>. In this post I look at python OSGB to <a href="https://confluence.qps.nl/pages/viewpage.action?pageId=29855173">WGS84 </a>conversion.
Converting between OSGB and WGS84 is possible, but it is rather <a href="http://www.hannahfry.co.uk/blog/2012/02/01/converting-british-national-grid-to-latitude-and-longitude-ii">involved</a>. Thankfully there are already some Python OSGB to WGR84 conversion modules that we can use.
<h1>Use the bng-latlon module</h1>
The OSGB grid system is also known as the British National Grid (BNG). The <a href="https://pypi.python.org/pypi/bng-latlon">bng-latlon module</a>, originally written by <a href="http://www.hannahfry.co.uk/">Hannah Fry</a>, takes the hard work out of converting between OSGB and WGS84.
You can install the bng-latlon module with
```bash
pip install bng_latlon
```
and use it with:
```python
from bng_to_latlon import OSGB36toWGS84
OSGB36toWGS84(538890, 177320)
```
which gives the output
```python
(51.47779538331092, -0.0014016837826672265)
```
It is also possible to convert from WGS84 back to OSGB with:
```
from latlon_to_bng import WGS84toOSGB36
WGS84toOSGB36(51.4778, -0.0014)
```
which gives the output as OSGB coordinates:
```python
(538890.1053365842, 177320.49650700082)
```
<h3><a href="http://wp.me/p4DE9r-FE">See how the bng-latlon package can be used to plot publicly available data.</a></h3>
<h1>Dealing With OSGB Letter Codes</h1>
One of the features (peculiarities?) of the OBGR system is that it can be represented by both letter or numbers. The <a href="https://pypi.python.org/pypi/bng-latlon">bng-latlon package</a> doesn't account for these letter codes, so you may need to use a different module for Python OSGB to WGR84 conversion such as <a href="http://all-geo.org/volcan01010/2012/11/change-coordinates-with-pyproj/">pyproj</a>, or <a href="http://pydoc.net/Python/osgb/0.2dev/osgb.convert/">osgb</a>.
<a href="https://commons.wikimedia.org/w/index.php?curid=35301574">Image</a>: By cmglee, Strebe, MansLaughter, Alexrk2 from naturalearthdata, Pethrus and nandhp, <a title="Creative Commons Attribution-Share Alike 3.0" href="http://creativecommons.org/licenses/by-sa/3.0">CC BY-SA 3.0</a>

