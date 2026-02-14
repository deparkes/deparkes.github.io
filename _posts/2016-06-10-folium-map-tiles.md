---
layout: post
title: Folium Map Tiles
date: 2016-06-10 15:00:30.000000000 +01:00
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
- gis
- map tiles
- mapping
- maps
- python
author: deparkes
permalink: "/2016/06/10/folium-map-tiles/"
---
Using different map tiles can be a great way to change or improve the look of your map. This post shows you how to access <a href="https://pypi.python.org/pypi/folium">Folium </a>map tiles and switch between them.
<h1>Folium Map Tiles Basic Code</h1>
The basic code for changing the map tiles used by folium is to first add a specified tile layer to the map (in this case "my_map").
You can also add a control for switching between layers with the "LayerControl()" method.

```python
folium.TileLayer('openstreetmap').add_to(my_map)
# other mapping code (e.g. lines, markers etc.)
folium.LayerControl().add_to(my_map)
```

<h1>Folium Map Tiles Examples</h1>
Here are a some examples of the free Folium map tiles that work "out of the box".
<h2>Open street map</h2>
Folium defaults to using <a href="https://wiki.openstreetmap.org/wiki/Tiles">openstreetmap </a>tiles. You can also access these tiles with:

```python
folium.TileLayer('openstreetmap').add_to(my_map)
```

| ![Folium Map Tiles - open street map]({{site.url}}/assets/2016/06/open-street-map.png) |
|:--:|
| *Folium Map Tiles - open street map* |

<h2>Map Quest Open</h2>
Similar to open street map, <a href="https://open.mapquest.co.uk/">mapquestopen </a>tiles are a good general purpose tile set.
```python
folium.TileLayer('mapquestopen').add_to(my_map)
```

| ![Folium Map Tiles - open street map]({{site.url}}/assets/2016/06/mapquestopen.png) |
|:--:|
| *Folium Map Tiles - mapquestopen* |

<h2>MapQuest Open Aerial</h2>
<a href="https://open.mapquest.co.uk/">Mapquest </a>also provides open aerial photography to use as map tiles:
```python
folium.TileLayer('MapQuest Open Aerial').add_to(my_map)
```

| ![Folium Map Tiles - mapquest open aerial]({{site.url}}/assets/2016/06/mapquest-open-aerial.png) |
|:--:|
| *Folium Map Tiles - mapquest open aerial* |

<h2>Mapbox Bright</h2>
<a href="https://www.mapbox.com/">Mapbox </a>makes some nice map tiles, but the free versions only have limited levels of zoom available (i.e. you can't zoom close in).
```python
folium.TileLayer('Mapbox Bright').add_to(my_map)
```

| ![Folium Map Tiles - mapbox bright]({{site.url}}/assets/2016/06/mapbox-bright.png) |
|:--:|
| *Folium Map Tiles - mapbox bright* |

<h2>Mapbox Control Room</h2>
Control Room is another set of <a href="https://www.mapbox.com/">MapBox</a> tiles. Again there are only limited levels of zoom available for the free version, but they do look cool.
```python
folium.TileLayer('Mapbox Control Room').add_to(my_map)
```

| ![Folium Map Tiles - mapbox controlroom]({{site.url}}/assets/2016/06/mapboxcontrolroom.png) |
|:--:|
| *Folium Map Tiles - mapbox controlroom* |

<h2>Stamen Terrain</h2>
<a href="https://maps.stamen.com">Stamen </a>also produce some cool map tiles which typically work at all zoom levels. These <a href="https://maps.stamen.com/#terrain">terrain </a>tiles are only available for the USA unfortunately.
```python
folium.TileLayer('stamenterrain').add_to(my_map)
```

| ![Folium Map Tiles - stamenterrain]({{site.url}}/assets/2016/06/stamenterrain.png) |
|:--:|
| *Folium Map Tiles - stamenterrain* |

<h2>Stamen Toner</h2>
The <a href="https://maps.stamen.com/#toner">Stamen </a>toner map tiles produce a black and white map that both looks striking and would be more suitable for printing than some of the other Folium map tiles.
```python
folium.TileLayer('stamentoner').add_to(my_map)
```

| ![Folium Map Tiles - stamentoner]({{site.url}}/assets/2016/06/stamentoner.png) |
|:--:|
| *Folium Map Tiles - stamentoner* |

<h2>Stamen Watercolor</h2>
To be honest I'm not sure where the <a href="https://maps.stamen.com/#watercolor">Stamen Watercolor</a> map tiles would be useful, but they look very cool.
```python
folium.TileLayer('stamenwatercolor').add_to(my_map)
```

| ![Folium Map Tiles - stamen_watercolor]({{site.url}}/assets/2016/06/stamen_watercolor.png) |
|:--:|
| *Folium Map Tiles - stamen_watercolor* |

<h2>CartoDB Positron</h2>
The <a href="https://cartodb.com/">CartoDB </a>folium map tiles are cool looking tiles and are available in the lighter "positron", or "dark matter" (below)
```python
folium.TileLayer('cartodbpositron').add_to(my_map)
```

| ![Folium Map Tiles - cartodbpositron]({{site.url}}/assets/2016/06/cartodbpositron.png) |
|:--:|
| *Folium Map Tiles - cartodbpositron* |

<h2>CartoDB Dark Matter</h2>
The <a href="https://cartodb.com/">CartoDB </a>Dark Matter tiles are essentially a darker version of the above positron tiles.
```python
folium.TileLayer('cartodbdark_matter').add_to(my_map)
```

| ![Folium Map Tiles - cartodbdark_matter]({{site.url}}/assets/2016/06/cartodbdark_matter.png) |
|:--:|
| *Folium Map Tiles - cartodbdark_matter* |
