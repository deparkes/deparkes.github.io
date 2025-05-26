---
layout: post
title: Convert From GDS to LinearRing
date: 2015-03-10 21:19:41.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- gds
- geometry
- polygons
author:
  display_name: deparkes
permalink: "/2015/03/10/convert-from-gds-to-linearring/"
---
<h1>Convert From GDS to LinearRing</h1>
GDS is a common format for <a title="Layout Design Software" href="{{site.baseurl}}/2015/02/21/layout-design-software/">electronic circuit designs</a>, <a href="http://en.wikipedia.org/wiki/Microelectromechanical_systems">MEMS </a>and other technologies.  At the moment I'm working on a <a href="https://github.com/deparkes/gds2ecp">project </a>to convert from gds to a format for electron beam lithography.
Whilst it might be possible to work directly with the gds files themselves, it made much more sense to convert them to an intermediate format that was <strong>easier to work with</strong>.
I've been using the <a href="http://toblerity.org/shapely/manual.html">Shapely Python library</a> to work with polygons, so I decided to convert from gds to LinearRing, a shapely object type.
<a href="https://github.com/deparkes/shapely_tests/blob/master/gds2ring.py">Download my script to convert gds to LinearRing</a>
<h1>GDS vs LinearRing</h1>
The gds file contains <a href="http://www.rulabinsky.com/cavd/text/chapc.html">all sorts of information</a> about units, formats and layers. Thankfully the bit that we care about is just a <strong>simple list of coordinates</strong>. This list of coordinates is called a <strong>boundary</strong>.
It turns out that GDS boundaries and LinearRings are quite similar, so we don't have to do do much to convert between them.
<h2>GDS Boundaries</h2>
GDS Boundaries are of the format
```XY: x1, y1, x2,y2, x3,y3, ... , xn, yn```
they must be explicitly closed, so that the first and last pairs of coordinate values are the same.
<h2>LinearRings</h2>
Shapely <a href="http://toblerity.org/shapely/manual.html#linearrings">LinearRing </a>objects are an ordered sequence of (x,y) tuples
e.g.```ring = LinearRing([(0, 0), (1, 1), (1, 0)])```


They can be explicitly closed, otherwise the LinearRing will be closed implicitly, by copying the first coordinate pair to the last position in the ring.
<h1>Convert GDS to LinearRing</h1>
To quickly demonstrate how to convert a shape from GDS to LinearRing I've put together a short python script.
<a href="https://github.com/deparkes/shapely_tests/blob/master/gds2ring.py">Download the gds2ring.py python script</a>
As we saw above the key difference between a gds boundary and a LinearRing is that the LinearRing is a list of tuple coordinate pairs. To extract the pairs from the gds boundary list we can use the <a href="http://stackoverflow.com/questions/4628290/pairs-from-single-list">izip function</a> from the itertools library.
In its simplest from conversion from gds to LinearRing could be something like:

```python
from itertools import izip
def pairwise(t):
    it = iter(t)
    return izip(it,it)
# Dummy gds boundary data
gds_test = (0, 0, 30000, 0, 15000, 15000, 5000, 15000, 0, 0)
# Extract the coordinates pairwise from the gds boundary
ring = list(pairwise(gds_test))
# Need to convert out list into a ring for the plotting function to work
ring = LinearRing(ring)
```
In the<a href="https://github.com/deparkes/shapely_tests/blob/master/gds2ring.py"> script in my repository</a>, I've added code from the shapely examples to let us plot the end result:

| ![GDS to LinearRing]({{site.baseurl}}/assets/2015/03/gds2ring-300x286.png) |
|:--:|
| *GDS to LinearRing* |
