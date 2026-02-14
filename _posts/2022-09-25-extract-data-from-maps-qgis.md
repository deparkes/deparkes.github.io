---
layout: post
title: Extract Data From Maps QGIS
date: 2022-09-25 06:19:21.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
tags:
- data
- mapping
- maps
- qgis
author: deparkes
permalink: "/2022/09/25/extract-data-from-maps-qgis/"
---
In this blog post I'll show you how to extract data from maps using QGIS to georeference a map image and identify data points.
The steps are:
<ol>
<li>Start with a map image containing data you want to capture, such as marked locations</li>
<li>Add a base map to QGIS that you will load the map image on to</li>
<li>Import the map image and 'georeference' to get correct alignment</li>
<li>Create a data layer in QGIS and select data points</li>
<li>Export data points extracted from the map to a separate file</li>
</ol>
<h2>The Starting Map</h2>
I'm assuming you have a raster map image that you want to extract location data from. In this example I'll be using the <a href="https://en.wikipedia.org/wiki/American_airborne_landings_in_Normandy#/media/File:101st_Airborne_drop_pattern,_D-Day,_6_June_1944.JPG">drop pattern of airborne landings on D-Day</a>.
This map image has an underlying map image with identifyable locations and features. We will use these later to georeference the map image against an underlying base map.

| ![extract data from maps - starting map]({{site.url}}/assets/2022/09/101st_Airborne_drop_pattern_D-Day_6_June_1944-283x300.jpg) |
|:--:|
| *extract data from maps - starting map* |

<h2>Add Basemap</h2>
If you don't have it already you'll need to <a href="https://www.giscourse.com/quickmapservices-plugin-an-easy-way-to-add-basemaps-in-qgis/">install the QuickMapServices plugin</a>.
With that plugin installed you can import the Open Streetmap Standard base map.

| ![extract data from maps - basemap]({{site.url}}/assets/2022/09/OSM_Standard.png) |
|:--:|
| *extract data from maps - basemap* |

With the base map imported we can navigate to roughly the right location for our map image.

| ![Normandy]({{site.url}}/assets/2022/09/Normandy.jpg) |
|:--:|
| *Normandy* |

<h2>Import Map Image</h2>
We can now import the map image that we are interested in. To do this we will use the '<a href="https://docs.qgis.org/3.22/en/docs/user_manual/working_with_raster/georeferencer.html">Georeferencer</a>'.
<img class="aligncenter size-full wp-image-5574" src="{{site.url}}/assets/2022/09/Georeferencer.png" alt="Georeferencer" width="366" height="212">

| ![Georeferencer]({{site.url}}/assets/2022/09/Georeferencer.png) |
|:--:|
| *Georeferencer* |

From the Georeferencer we need to Open Raster and select the map image we want to load.

| ![Georeferencer - Open Raster]({{site.url}}/assets/2022/09/Georeferncer_OpenRaster.png) |
|:--:|
| *Georeferencer - Open Raster* |

Once we have loaded the map image we can identify and apply the georeferencing points.
<h2>Apply Georeferencing Points</h2>
The georeferencing process involves selecting features or landmarks on the map image and then finding them in the corresponding location on the base map.
<a href="https://www.qgistutorials.com/en/docs/georeferencing_basics.html">Read more about the basics of georeferencing</a>

| ![Georeferencer - add points]({{site.url}}/assets/2022/09/Georeferencer_AddPoint.jpg) |
|:--:|
| *Georeferencer - add points* |

You'll typically need to add at least four points, but <a href="https://docs.qgis.org/3.22/en/docs/user_manual/working_with_raster/georeferencer.html#available-transformation-algorithms">check the Georeferencer documentation for guidelines</a>. More points enable more accurate registration between the map image and the base map.

| ![Georeferencer - all points]({{site.url}}/assets/2022/09/Georeferencer_AllPoint.jpg) |
|:--:|
| *Georeferencer - all points* |

Before running the georeferencer, go to settings -&gt; Transformation Settings and set the transformation type to "Helmert". This is a good starting point as it won't warp your image too much but does allow both translation and rotation.
If you are playing around with different georeferencing settings you may find you need to change the output filename each time to stop filename clashes.
Minimise or close the Georeferencer window to check the result. You can switch the new map layer on and off to check you are happy with the alignment.

| ![Check the map]({{site.url}}/assets/2022/09/CheckTheMap-1.jpg) |
|:--:|
| *Check the map* |

<h2>Create Data Layer</h2>
It's at this point we can actually start extracting the location data from the map.
For this example map of Normandy airborne landings I am interested in the individual landing points, so I will create a point layer to store the point location data.
First we create a layer by going to Layer -&gt; Create Layer -&gt; Add Shapefile Layer
In the Layer Settings window we set a filename, and select 'Point' as the Geometry type. For now we don't need to worry about the other settings.

| ![New Shapefile Layer]({{site.url}}/assets/2022/09/new_shapefile_layer.png) |
|:--:|
| *New Shapefile Layer* |

<h2>Create Data Points</h2>
With the layer created we can add points to it.
First we allow editing on the layer by clicking the "Toggle Editing"

| ![Toggle Editing]({{site.url}}/assets/2022/09/ToggleEditing.png) |
|:--:|
| *Toggle Editing* |

Followed by "Add Point Feature"

| ![Add Point Feature]({{site.url}}/assets/2022/09/AddPointFeature.png) |
|:--:|
| *Add Point Feature* |

We can simply then click on the locations where we want to record a point data item. When the option to set an ID value comes up we can just hit ok.

| ![A data point]({{site.url}}/assets/2022/09/ADataPoint.png) |
|:--:|
| *A data point* |

When you are finished, hit 'Toggle Edits' again and save the changes.
<h2>Saving the Data to a File</h2>
You can export the data layer by right clicking then going to "Export" and "Save Features As...". You'll see there are many different file format options.
For now we'll export to a <a href="https://en.wikipedia.org/wiki/GeoJSON">geojson</a> file so we can easily inspect it in a text editor:

| ![Exported to geojson]({{site.url}}/assets/2022/09/my_data_geojson.png) |
|:--:|
| *Exported to geojson* |

You can also view the geojson data on <a href="https://geojson.io">geojson.io</a>
