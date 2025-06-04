---
layout: post
title: Convert Postcode Coordinates
date: 2016-07-01 15:00:03.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- data
- GIS
- python
tags:
- geocoding
- gis
- mapping
- sql
author: deparkes
permalink: "/2016/07/01/convert-postcode-coordinates/"
---
It's common to have the <a href="https://en.wikipedia.org/wiki/Postcodes_in_the_United_Kingdom">postcode </a>of an address and need to plot this on a map. In this post I show you two options for how to convert postcode coordinates using an online tool or data available for free online.
<h1>Option 1. Use an Online Conversion Tool</h1>
Often the easiest way to convert postcode coordinates is to use an online tool like this <a href="https://www.gridreferencefinder.com/postcodeBatchConverter/">one</a>. You can upload your address data at it will give you <a href="https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid">OS grid reference coordinates</a>, <a href="https://en.wikipedia.org/wiki/Easting_and_northing">eastings and northings</a>, as well as <a href="https://en.wikipedia.org/wiki/Geographic_coordinate_system">latitude and longitude</a>.

| ![convert postcode coordinates - output]({{site.baseurl}}/assets/2016/07/output_data.png) |
|:--:|
| *convert postcode coordinates - output* |

The tool also gives you the option to view your points in an interactive map:

| ![convert postcode coordinates - map]({{site.baseurl}}/assets/2016/07/grid_reference_finder.png) |
|:--:|
| *convert postcode coordinates - map* |


<a href="https://www.gridreferencefinder.com/postcodeBatchConverter/">Check out Postcode Batch Converter Tool at UK Grid Reference Finder</a>
<h1>Option 2. Do It Yourself</h1>
It sometimes makes more sense for you to convert postcode coordinates yourself. In this case I would recommend downloading the most recent <a href="https://parlvid.mysociety.org/os/">ONS Postcode Directory</a>  which contains a list of all postcodes and their corresponding coordinates.
Once you have this then it is just a case of matching your list of postcodes with the correct ones in the ONS directory. To do this in SQL, you would want something like:

```sql
SELECT
T1.Name, T2.Lat, T2.Long
FROM
my_data as T1, ons_directory as T2
WHERE
REPLACE(T1.Location, ' ', '') = REPLACE(T2.pcd, ' ', '')
```

which joins the two tables together on the postcode. And gives the latitude and longitude for the postcodes in the "my_data" table. Once you have the latitude and longitude from the ONS directory you can convert to other coordinate systems as needed.
Which ever way you do this you will probably need a line like:

```sql
REPLACE(T1.Location, ' ', '') = REPLACE(T2.pcd, ' ', '')
```

to deal with postcodes being written with different amounts of whitespace.
