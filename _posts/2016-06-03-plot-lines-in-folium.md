---
layout: post
title: Plot Lines In Folium
date: 2016-06-03 15:00:56.000000000 +01:00
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
- folium
- mapping
- maps
- python
- visualisation
author: deparkes
permalink: "/2016/06/03/plot-lines-in-folium/"
---
In this post I show you how to plot lines in <a href="https://wp.me/p4DE9r-FU">F</a><a href="https://wp.me/p4DE9r-FU">olium </a>- the python module for plotting leaflet maps.
<h1>Add PolyLine to Map</h1>
Like 'markers', lines are added to folium map objects with the add_to() method
```python
folium.PolyLine(points).add_to(my_map)
```
where "points" is a list of tuples containing latitude and longitude information, and "my_map" is a folium map object.
By default this will give an output similar to:

| ![default polyline]({{site.baseurl}}/assets/2016/06/default_polyline.png) |
|:--:|
| *default polyline* |

<h1>Adjust Line Properties</h1>
We can alter the line properties (<strong>colour</strong>, <strong>weight</strong> and <strong>opacity</strong>) with:

```python
folium.PolyLine(points, color="red", weight=2.5, opacity=1).add_to(my_map)
```

| ![Plot Lines In Folium - thin red line]({{site.baseurl}}/assets/2016/06/red_polyline.png) |
|:--:|
| *Plot Lines In Folium - thin red line* |

<h1>Plot Lines and Markers</h1>
It can also be useful to plot both lines and markers on the same map. This can be easily done by using the Marker.add_to() method, and looping over each of the coordinate pairs in our list:

```python
#add markers
for each in points:
    folium.Marker(each).add_to(my_map)
#add lines
folium.PolyLine(points, color="red", weight=2.5, opacity=1).add_to(my_map)
```

| ![Plot Lines In Folium - line and markers]({{site.baseurl}}/assets/2016/06/red_with_marker_polyline.png) |
|:--:|
| *Plot Lines In Folium - line and markers* |

<h1>An Example</h1>
Here's an example involving loading in GPX coordinates from a GPS device. You can also download the code <a href="https://gist.github.com/deparkes/9a0b45c69beb9a614f54d13bc7c551b5">here</a>.
```python
import gpxpy
import gpxpy.gpx
import folium
gpx_file = open('path_to_gpx_file.gpx', 'r')
gpx = gpxpy.parse(gpx_file)
points = []
for track in gpx.tracks:
    for segment in track.segments:
        for point in segment.points:
            points.append(tuple([point.latitude, point.longitude]))
print(points)
ave_lat = sum(p[0] for p in points)/len(points)
ave_lon = sum(p[1] for p in points)/len(points)
# Load map centred on average coordinates
my_map = folium.Map(location=[ave_lat, ave_lon], zoom_start=14)
#add a markers
for each in points:
    folium.Marker(each).add_to(my_map)
#fadd lines
folium.PolyLine(points, color="red", weight=2.5, opacity=1).add_to(my_map)
# Save map
my_map.save("./gpx_berlin_withmarker.html")
```
