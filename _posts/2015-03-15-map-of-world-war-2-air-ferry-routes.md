---
layout: post
title: Map of World War 2 Air Ferry Routes
date: 2015-03-15 13:53:57.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- GIS
- History
tags:
- data
- maps
- qgis
- world war 2
author:
  display_name: deparkes
permalink: "/2015/03/15/map-of-world-war-2-air-ferry-routes/"
---
<h1>Map of World War 2 Air Ferry Routes</h1>
During the World War 2 air ferry routes were used to safely transport equipment, personel and supplies across the globe.

The wikipedia articles for the main routes didn't seem to have a map image, so I thought I'd have a go at making one myself.


| ![Air Ferry Routes of World War II]({{site.baseurl}}/assets/2015/03/AirFerryRoutesOfWWII_small-1024x561.png) |
|:--:|
| *Air Ferry Routes of World War II* |

<h1>How I Made the Map</h1>
<h2>Get Coordinates From Wikipedia Page</h2>
The articles have the coordinates for the different bases and airstrips used for each of the air ferry routes, so I figured it must be possible to plot them out.
The three principal air ferry routes were:
<ul>
<li><a href="http://en.wikipedia.org/wiki/North_Atlantic_air_ferry_route_in_World_War_II">North Atlantic Air Ferry Route</a></li>
<li><a href="https://en.wikipedia.org/wiki/South_Atlantic_air_ferry_route_in_World_War_II">South Atlantic Air Ferry Route</a></li>
<li><a href="http://en.wikipedia.org/wiki/South_Pacific_air_ferry_route_in_World_War_II">South Pacific Air Ferry Route</a></li>
</ul>
By saving each of these pages as an html file and loading into Excel/LibreOffice Calc, I could extract the relevant data tables.
I saved each data table as a separate tab-delimited text file, from which I could extract the coordinates with a python script.
<h3><a href="https://github.com/deparkes/AirFerry/blob/master/StripCoords.py">Download my python script to help get the coordinates</a></h3>
<h2>Set Up The World Map in QGIS</h2>

To set up the background world map to show the routes I followed <a href="http://www.qgistutorials.com/en/docs/making_a_map.html">this guide</a>

| ![World War 2 Air Ferry Routes - QGIS]({{site.baseurl}}/assets/2015/03/QGIS_AirFerry-300x169.png) |
|:--:|
| *World War 2 Air Ferry Routes - QGIS.* |


This tutorial uses the <a class="reference external" href="http://kelso.it/x/nequickstart">Natural Earth Quickstart Kit</a>.
<h2>Load Coordinates into QGIS</h2>
I just followed <a href="http://www.qgistutorials.com/en/docs/importing_spreadsheets_csv.html">this guide</a> to loading comma separated values. You go to <strong>Layers</strong> -&gt; <strong>Add Layer</strong> -&gt; <strong>Add Delimited Text Layer</strong>.

| ![World War 2 Ferry Routes - Delimited Text File]({{site.baseurl}}/assets/2015/03/TextDelimitedFile-300x192.png) |
|:--:|
| *World War 2 Ferry Routes - Delimited Text File.* |

Across the <strong>international date line</strong> the coordinates change sign, and QGIS isn't sure how to correctly interpret this, which means I had to <strong>break up the files</strong> so that they would plot as vectors more or less correctly.
<h2>Convert Points to a Vector</h2>
I could have just left the coordinates of the routes as individual points, but I thought it would be clearer to join them together to <strong>show the paths</strong> between them.
I converted the points to vectors using the <a href="https://plugins.qgis.org/plugins/points2one/">Points2One </a>QGIS plugin. You can install it from the <a href="http://www.qgistutorials.com/en/docs/using_plugins.html">QGIS plugin menu</a>.
Run by going to <strong>Vector</strong> -&gt; <strong>Points2One</strong> -&gt; <strong>Points2One</strong>.

Select the points you want to use to form the vector, and select "Lines" to make a path, rather than a polygon.

| ![World War 2 Air Ferry Routes - Points2One]({{site.baseurl}}/assets/2015/03/Points2One-221x300.png) |
|:--:|
| *World War 2 Air Ferry Routes - Points2One* |
