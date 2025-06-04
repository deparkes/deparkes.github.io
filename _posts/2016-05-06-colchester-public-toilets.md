---
layout: post
title: Colchester Public Toilets
date: 2016-05-06 09:00:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- GIS
tags:
- colchester
- data
- folium
- mapping
- open data
- public toilets
author: deparkes
permalink: "/2016/05/06/colchester-public-toilets/"
---
Use this interactive map to find Colchester public toilets. There are some as far afield as Dedham and Mersea!
<iframe src="{{site.baseurl}}/assets/maps/colch_toilets.html" name="FRAME2" width="450" height="400" frameborder="1"></iframe>
<h1>Colchester Public Toilets: Python Code</h1>
<a href="https://datashare.colchester.gov.uk/View/street-care/public-toilets#">Data</a> on the locations of the public toilets in Colchester from <a href="https://www.colchester.gov.uk/residents">Colchester Borough Council</a>.
This map was produced using the <a href="https://pypi.python.org/pypi/folium">Folium </a>python package. The code is available below, or you can download it <a href="https://gist.github.com/deparkes/a202c31809771facad1f208e00fede5a#file-colch_toilets-py">here</a>.

```python
import os
import folium
import pandas as pd
from bng_to_latlon import OSGB36toWGS84
# Load map centred on Colchester
uk = folium.Map(location=[51.5069439,-0.1510636], zoom_start=10)
# Load locally stored colchester public toilets data
toilets = pd.read_csv("public-toilets.csv")
#add a marker for each toilet
for each in toilets.iterrows():
    print(list([each[1].GeoY,each[1].GeoX]))
    print(list(OSGB36toWGS84(each[1]['GeoX'],each[1]['GeoY'])))
    folium.Marker(list(OSGB36toWGS84(each[1]['GeoX'],each[1]['GeoY'])), popup=each[1]['StreetAddress']).add_to(uk)
# Save map
uk.save("./colch_toilets.html")
```
