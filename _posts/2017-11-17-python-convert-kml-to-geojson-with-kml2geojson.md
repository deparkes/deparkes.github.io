---
layout: post
title: Python Convert KML to GeoJSON
date: 2017-11-17 15:00:04.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- convert
- geojson
- gis
- json
- kml
- mapping
- python
author:
  display_name: deparkes
permalink: "/2017/11/17/python-convert-kml-to-geojson-with-kml2geojson/"
---
<a href="https://stackoverflow.com/questions/4262607/which-data-source-is-preferable-for-google-maps-kml-or-json">GeoJSON and KML</a> are formats for storing spatial information. KML files are commonly found with <a href="https://en.wikipedia.org/wiki/Google_Earth">Google Earth</a> type applications, so it can be useful to convert <a href="https://en.wikipedia.org/wiki/Keyhole_Markup_Language">KML </a>to <a href="https://en.wikipedia.org/wiki/GeoJSON">GeoJSON</a>.  The python library <a href="https://pypi.python.org/pypi/kml2geojson/4.0.2">kml2geojson </a>can be used to convert KML to GeoJSON. kml2geojson works as either a tool from the command line, or can be used as a library within other programs.
<h2>Installation</h2>
Install kml2geojson using pip:

```bash
pip install kml2geojson
```

<h2>Use As A Command Line Tool</h2>
kml2geojson can be used as a tool from the command line. You can use it this way if you have some kml files that you just need to convert, without any additional programming.
The general usage of kml2geojson is:

```bash
k2g [options] kml_file output_dir
```

For basic usage we can run:

```bash
k2g test.kml json_files
```

Which will convert the file 'test.kml' to 'test.json' (a GeoJSON '<a href="https://macwright.org/2015/03/23/geojson-second-bite#featurecollection">Feature Collection</a>') and put the output into a directory 'json_files'. If the directory 'json_files' does not exist, then it is created.
To see more advanced features, run:

```bash
k2g --help
```


Or checkout the kml2geojson <a href="https://rawgit.com/araichev/kml2geojson/master/docs/_build/singlehtml/index.html">documentation</a>.
<h2>Use As a library</h2>
kml2geojson can also be called as a library so you can convert kml to geojson within other programs.
Basic conversion using the kml2geojson library can be done with:

```python
kml2geojson.main.convert(kml_file, output_directory)
```
E.g.
```python
import kml2geojson
kml2geojson.main.convert('./test.kml', '../data/json_files')
```

See more advanced options at the the <a href="https://rawgit.com/araichev/kml2geojson/master/docs/_build/singlehtml/index.html">kml2geojson documentation</a>.
