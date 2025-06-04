---
layout: post
title: UK University Locations
date: 2016-07-08 15:00:11.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
- python
tags:
- folium
- leaflet
- map
- mapping
- sql
- uk
- universities
author: deparkes
permalink: "/2016/07/08/uk-university-locations/"
---
The UK has around 160 universities, located around the country. Here is a map of UK University Locations, made using <a href="{{site.baseurl}}/2016/05/13/python-leaflet-map-folium/">Folium</a>.

<iframe src="{{site.baseurl}}/assets/maps/universities.html" name="FRAME2" width="450" height="400" frameborder="1"></iframe>
<a href="https://gist.github.com/deparkes/3b100ddb7068f82c1262b2236a153e01">Download the UK university locations data [csv]</a>
<a href="https://www.hesa.ac.uk/component/heicontacts/">Access the list of UK universities</a>
<h1>Python Code For UK University Locations</h1>

```python
import pandas as pd
import folium
from pandas import compat
compat.PY3 = True
universities = pd.read_csv("uk_universities_locations.csv")
uk = folium.Map(location=[universities.lat.mean(axis=0),universities.lon.mean(axis=0)], zoom_start=5)
marker_cluster = folium.MarkerCluster("Universities").add_to(uk)
#add a marker for each university
for each in universities.iterrows():
    folium.Marker(list([each[1]['lat'],each[1]['lon']]),popup=each[1]['Name']).add_to(marker_cluster)
uk.save("universities.html")
```

<a href="https://wp.me/p4DE9r-HX">How to convert postcodes to coordinates</a>
