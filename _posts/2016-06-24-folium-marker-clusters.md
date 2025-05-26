---
layout: post
title: Folium Marker Clusters
date: 2016-06-24 15:00:58.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
- python
tags:
- data
- gis
- mapping
- maps
- python
author:
  display_name: deparkes
permalink: "/2016/06/24/folium-marker-clusters/"
---
Marker clusters can be a good way to simply a map containing many markers. When the map is zoomed out nearby markers are combined together into a cluster, which is separated out when the map zoom level is closer. In this post I show you how <a href="https://deparkes.co.uk/2016/05/13/python-leaflet-map-folium/">Folium </a>marker clusters are easy to set up and use.

| ![folium marker clusters - cluster region]({{site.baseurl}}/assets/2016/06/marker-clusters.png) |
|:--:|
| *folium marker clusters - cluster region* |

<h1>Folium Marker Clusters - an example</h1>
To show what folium marker clusters can do I'm going to use the example of a simple map I've looked at before - <a href="https://deparkes.co.uk/2016/05/06/colchester-public-toilets/">public toilets in the town of Colchester</a>.
<h2>Before Marker Clusters</h2>
Here's what the map looked like before clustering the markers. All points are shown at all zoom levels. (You can see the code for this map <a href="https://deparkes.co.uk/2016/05/06/colchester-public-toilets/">here</a>)
<iframe src="{{site.baseurl}}/assets/maps/colch_toilets.html" name="FRAME2" width="450" height="400" frameborder="1"></iframe>
<h2>After Marker Clusters</h2>
In this next map the markers close to each other have been clustered together.
Double click on a cluster to zoom in and see the points it included.
You can also mouse-over a cluster to see the area that it represents.
<iframe src="{{site.baseurl}}/assets/maps/colch_toilets_clusters.html" name="FRAME2" width="450" height="400" frameborder="1"></iframe>
<h2>We can Also Add Markers Not Included In a Cluster</h2>
See the code below for how to do this.
<iframe src="{{site.baseurl}}/assets/maps/colch_toilets_clusters_extra_point.html" name="FRAME2" width="450" height="400" frameborder="1"></iframe>
<h1>How to Add Marker Clusters To a Map</h1>
The code to create a marker cluster is:
```python
marker_cluster = folium.MarkerCluster("Cluster Name").add_to(my_map)
```

We then add markers to this cluster, rather than directly to the map:
```python
folium.Marker([lon, lat]).add_to(marker_cluster)
```

Although we can still add points directly to the map (not attached to a cluster):
```python
folium.Marker([51.8860942,0.8336077], popup="not included in marker cluster").add_to(my_map)
```

Here is the code for the examples above:
```python
import os
import folium
import pandas as pd
from bng_to_latlon import OSGB36toWGS84
# Load map centred on Colchester
uk = folium.Map(location=[51.8860942,0.8336077], zoom_start=10, control_scale=True)
# Load locally stored colchester public toilets data
toilets = pd.read_csv("public-toilets.csv")
# create a marker cluster called "Public toilet cluster"
marker_cluster = folium.MarkerCluster("Public toilet cluster").add_to(uk)
#add a marker for each toilet, add it to the cluster, not the map
for each in toilets.iterrows():
    popup = 'Add <b>test</b>;'
    print(list([each[1].GeoY,each[1].GeoX]))
    print(list(OSGB36toWGS84(each[1]['GeoX'],each[1]['GeoY'])))
    folium.Marker(list(OSGB36toWGS84(each[1]['GeoX'],each[1]['GeoY'])), popup=popup).add_to(marker_cluster)
# we can also add a marker directly to the map, outside of the clustering
folium.Marker([51.8860942,0.8336077], popup="not included in marker cluster",icon=folium.Icon(color='red',icon='info-sign')).add_to(uk)
# Save map
uk.save("./colch_toilets_clusters.html")
```
