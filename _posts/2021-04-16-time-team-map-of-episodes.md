---
layout: post
title: Time Team Map of Episodes
date: 2021-04-16 06:59:53.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- History
tags:
- archaeology
- folium
- gis
- mapping
- maps
author:
  display_name: deparkes
permalink: "/2021/04/16/time-team-map-of-episodes/"
---
<a href="https://en.wikipedia.org/wiki/Time_Team">Time Team</a> was a TV series which involved a team of archaeologists, surveyors, artists and other specialists spending three days to investigate an archaeological site. Episodes were mainly focused on the UK, but there were also some as far afield as Spain and America. I thought it would be interesting to see how episodes were distributed around the UK and beyond, so I made a Time Team map.
<h2>Time Team Map</h2>
Zoom out to see episodes in Europe and America. Colours represent different series, and you can filter which series are shown using the layer icon in the top-right-hand corner. Click on the marker icons to see information about individual episodes and a link to more information on Wikipedia.
<iframe src="{{site.baseurl}}/assets/maps/time_team_map.html" name="time_team_map" width="600" height="400" frameborder="1"></iframe>
<h2>How the Time Team Map Was Made</h2>
<h3>Getting the Data</h3>
The episode titles and locations were gathered from Wikipedia pages in March 2021. As there were not too many pages, I copied and pasted the tables into a spreadsheet where I could easily get columns and rows into a consistent structure for further processing.
Most Time Team episodes were focused on a single location, but a few were spread across multiple sites. In these cases I just included a row for each site so that I could easily plot them.
I did consider using the <a href="https://deparkes.co.uk/2020/12/27/python-compare-wikipedia-pages/">Wikipedia API</a> or some other <a href="https://www.analyticsvidhya.com/blog/2015/10/beginner-guide-web-scraping-beautiful-soup-python/">web-scraping</a> technique, but found that there was quite a bit of variation between Time Team pages on Wikipedia, and there was no guarantee that the page structure or content would stay the same over time.
<h3>Parsing Dates</h3>
Original air dates are included on the Wikipedia pages in the format '16 January 1994'. Typically when you load a file with pandas you can that date columns should be parsed with <a href="https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.read_csv.html">the 'parse_dates' parameter</a>. By default pandas uses 'month first' dates e.g. mm-dd or mm/dd. In the simple case that you are providing a 'day first' date you can simply add the day_first=True argument. In this case the dates were in a less common format, so I needed to use a <a href="https://stackoverflow.com/questions/23797491/parse-dates-in-pandas#23797980">custom parser</a>.
<a href="https://www.w3schools.com/python/gloss_python_date_format_codes.asp">Read more about possible date format strings.</a>

```python
import pandas as pd
from datetime import datetime
custom_date_parser = lambda x: datetime.strptime(x, "%d %B %Y")
data_location = https://gist.githubusercontent.com/deparkes/9338571dbd67a6e9977d996d60ef4e37/raw/858d809549fb971588231b6e74ce0dffeef4075b/time_team_episodes.csv
episodes = pd.read_csv(data_location, parse_dates=['Original airdate'], date_parser=custom_date_parser)
```

<h3>Parsing Locations</h3>
The main challenge with handling the data was that there was not a consistent way of recording site locations. Thankfully all were in latitude and longitude rather than <a href="https://en.wikipedia.org/wiki/Ordnance_Survey_National_Grid">British National Grid</a> coordinates, so I didn't need to do <a href="https://deparkes.co.uk/2016/05/27/python-osgb-to-wgr84/">that conversion</a>.
A final complication was that some of the 'special' episodes didn't really have a particular location associated with them. The Time Team specials often covered a particular technique or time period, rather than focusing on one or two sites. In these cases I have simply omitted them from the map.

```python
series = episodes[~episodes['Coordinates'].isin(['TBA'])].dropna(subset=['Coordinates'])
```

The problem was that there was a mixture of decimal degrees and degrees, minutes and seconds, and a mixture of positive and negative values along with 'East' and 'West'.
Rather than attempt to make my own parser that could handle these different cases, I instead used the <a href="https://pypi.org/project/lat-lon-parser/">lat-lon parser</a> library in python. I found this library could intelligently handle the variety of methods of recording latitude and longitude used on the Time Team Wikipedia pages.

```python
from lat_lon_parser import parse
lat_long = series['Coordinates'].str.strip(' ')                               \
                   .str.split(' ', expand=True)                   \
                   .rename(columns={0:'latitude', 1:'longitude'})
lat_long['latitude'] = lat_long['latitude'].apply(lambda x: float(format(parse(str(x)), '.6f')))
lat_long['longitude'] = lat_long['longitude'].apply(lambda x: float(format(parse(str(x)), '.6f')))
df = pd.concat([series, lat_long], axis=1)
```

<h3>Plotting Points</h3>
Now that I had the coordinates and associated episode metadata such as Title, Episode Number etc. I wanted to plot the Time Team map using <a href="https://deparkes.co.uk/2016/05/13/python-leaflet-map-folium/">Folium</a>. To do this I largely followed the instructions on this <a href="https://geopandas.org/gallery/plotting_with_folium.html">blog post</a> for <a href="https://geopandas.org/index.html">Geopandas</a>.
Geopandas extends the functionality of basic pandas dataframes to support geographic and mapping operations.
The key step was producing a 'geometry' based on the latitude and longitudes for each episode site.

```python
geometry = geopandas.points_from_xy(df.longitude, df.latitude)
geo_df = geopandas.GeoDataFrame(df[['Series', 'SeriesNumber', 'EpisodeNumber', 'EpisodeTitle', 'Original airdate', 'WikipediaURL', 'latitude', 'longitude']], geometry=geometry)
```

Once the geodataframe had the geometry alongside the original data it can be plotted using Folium.
Rather than simply plotting all of the points in the same way, I wanted to:
<ol>
<li>Enable layers so that each series could be turned on/off on the map</li>
<li>Show basic episode information as a label against each point</li>
<li>Have a different colour for each series to help make them more visible</li>
</ol>
The code for this is the following:

```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import cm
from collections import OrderedDict
import matplotlib
# Make a selection of colours from the 'inferno' colour map
cmap = cm.get_cmap('inferno', 21)
colors = [matplotlib.colors.rgb2hex(c) for c in cmap.colors]
# Create a dictionary lookup for series names
series_lookup = {series_name:index for index, series_name in enumerate(geo_df.Series.unique())}
# Create a base map on which to plot the other elements
mapa = folium.Map(location=[55.5,0], zoom_start=5, tiles='OpenStreetMap')
for group_name, group_data in geo_df.groupby('Series'):
    # Create a feature group for each of the Series in the data frame
    feature_group = folium.FeatureGroup(group_name)
    # Run through the data in each group,
    # plotting a labelled marker for each point
    for row in group_data.itertuples():
        folium.Marker(location=[row.latitude, row.longitude],
                      popup='Episode: <a href=' + row.WikipediaURL + '>' + row.Series + '.' + str(row.SeriesNumber) + '</a><wp-br>'
                      "Title: " + row.EpisodeTitle + '<wp-br>' +
                      "Location: " + str(row.latitude) + ', ' + str(row.longitude) + '<wp-br>',
                      icon=folium.Icon(color='black',
                                       icon_color=colors[series_lookup[row.Series]])).add_to(feature_group)
    feature_group.add_to(mapa)
folium.LayerControl().add_to(mapa)
```

I'll break down the major parts of this code:
<h4>Plotting Layers</h4>
I found some code for this on <a href="https://stackoverflow.com/questions/61263787/folium-featuregroup-in-python">Stackoverflow</a>. The idea is to group by each series and then loop through the data in each of the groups, each time adding to a Folium '<a href="https://github.com/python-visualization/folium/blob/master/examples/FeatureGroup.ipynb">Feature Group</a>'.
Here's some simplified code for this:

```python
mapa = folium.Map(location=[55.5,0], zoom_start=5, tiles='OpenStreetMap')
for group_name, group_data in geo_df.groupby('Series'):
    # Create a feature group for each of the Series in the data frame
    feature_group = folium.FeatureGroup(group_name)
    # Run through the data in each group,
    # plotting a labelled marker for each point
    for row in group_data.itertuples():
        folium.Marker(location=[row.latitude, row.longitude]).add_to(feature_group)
    feature_group.add_to(mapa)
folium.LayerControl().add_to(mapa)
```

The final line in the above is important as it adds the layer control to the map, so that layers can be switched on and off.
<h4>Episode Information Labels</h4>
Adding episode information to the label is relatively simple. The Folium icons can take a 'popup' argument which which can be a simple text label, or can include <a href="https://render.githubusercontent.com/view/ipynb?color_mode=auto&amp;commit=c25c84c888415a8f242e133c97242e26c3070fe6&amp;enc_url=68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f707974686f6e2d76697375616c697a6174696f6e2f666f6c69756d2f633235633834633838383431356138663234326531333363393732343265323663333037306665362f6578616d706c65732f506f707570732e6970796e62&amp;nwo=python-visualization%2Ffolium&amp;path=examples%2FPopups.ipynb&amp;repository_id=9952134&amp;repository_type=Repository#Fancy-HTML-popup">html</a>. In this case I have built up the popup using different fields from the data frame including a URL to find more information about the episode. I've also added line breaks to help with formatting.

```python
popup='Episode: <a href=' + row.WikipediaURL + '>' + row.Series + '.' + str(row.SeriesNumber) + '</a><br>'
                      "Title: " + row.EpisodeTitle + '<br>' +
                      "Location: " + str(row.latitude) + ', ' + str(row.longitude) + '<br>'
```

<h4>Series Colours</h4>
The final styling element I wanted to apply to the plotted markers was a different colour for each series (including specials).
This is achieved by first creating our own 21-colour map based on the matplotlib 'inferno' colour map. Since one of the series groups is named 'specials' we can't just use the series name to directly access the colour from the colour map, so instead I've created a lookup based on the unique series names. This is just a dictionary with the series name as a key, and the corresponding value relating to the colour that will be applied to the icons for that series.
<a href="https://matplotlib.org/stable/tutorials/colors/colormaps.html">Read more about matplotlib colour maps.</a>
<a href="https://towardsdatascience.com/creating-colormaps-in-matplotlib-4d4de78a04b8">And some more about colour maps.</a>

```python
# Make a selection of colours from the 'inferno' colour map
cmap = cm.get_cmap('inferno', 21)
series_lookup = {series_name:index for index, series_name in enumerate(geo_df.Series.unique())}
# Use the series name as the key to lookup it's corresponding colour
icon=folium.Icon(color='black', icon_color=colors[series_lookup[row.Series]])
```

