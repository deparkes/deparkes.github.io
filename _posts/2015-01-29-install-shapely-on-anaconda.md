---
layout: post
title: How to install Shapely on Anaconda Python (Windows)
date: 2015-01-29 16:41:57.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- anaconda
- geometry
- install
- shapely
author:
  display_name: deparkes
permalink: "/2015/01/29/install-shapely-on-anaconda/"
---
<h1>How to Install Shapely on Anaconda (Windows)</h1>
<a href="https://pypi.python.org/pypi/Shapely">Shapely </a>is a Python package for analysis and manipulation of geometric objects.
Here's how to install Shapely in the <a href="https://store.continuum.io/cshop/anaconda/">Anaconda </a>python distribution, from <a href="https://www.continuum.io/">Continuum Analytics</a>.
Anaconda uses its '<a href="https://conda.pydata.org/docs/">conda</a>' package manager to install, remove and otherwise manage python packages. This generally works well, but in the case of Shapely the recommended install method is to download and install a '<a href="https://wheel.readthedocs.org/en/latest/">wheel</a>' with <a href="https://pypi.python.org/pypi/pip">pip</a>.
Thankfully <a href="https://store.continuum.io/cshop/anaconda/">Anaconda </a>also lets us install packages using <a href="https://pypi.python.org/pypi/pip">pip</a>.
Your best option is probably to use plain anaconda:

```python
conda install shapely
```

This seems to work fine now, so the rest of this post may be a useful starting point if you find that simple option does not work for you (for example if the version available on conda is not up to date)
<h1>Download the most recent Shapely 'wheel'</h1>
The recommended install method for Shapely on windows is to download a .whl 'wheel' package: <a href="https://www.lfd.uci.edu/~gohlke/pythonlibs/#shapely">https://www.lfd.uci.edu/~gohlke/pythonlibs/#shapely</a>
You'll want to pick the right version of Python - you probably want version 2.7, but check your Anaconda distribution. You'll also need to pick between 32- or 64-bit.
<h1>Install With Pip</h1>
Once you've downloaded the correct Shapely package, open up the 'Anaconda Command Prompt' and navigate to the folder containing the downloaded wheel.
To install run:
```bash
pip install Shapely‑1.5.5‑cp27‑none‑win32.whl
```
which will install shapely to somewhere like:
```bash
C:\Anaconda\Lib\site-packages\shapely
```
To check which packages you have already installed (with pip), run
```bash
pip list
```
or
```bash
pip freeze
```
<h1>Where to find examples</h1>
I was a bit surprised to find the examples folder to be rather bare.
If you want to get the full suite of examples, I suggest downloading the source from the project github repository: <a href="https://github.com/Toblerity/Shapely">https://github.com/Toblerity/Shapely</a>

<a href="{{site.baseurl}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.baseurl}}/assets/2015/01/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>
