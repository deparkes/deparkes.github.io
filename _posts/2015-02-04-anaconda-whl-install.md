---
layout: post
title: How to install whl files in Anaconda
date: 2015-02-04 09:09:44.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- python
tags:
- andaconda
- install
- pip
- python
- whl
author:
  display_name: deparkes
permalink: "/2015/02/04/anaconda-whl-install/"
---
<h1>Anaconda whl Install</h1>
The <a href="https://pypi.python.org/pypi/wheel">whl </a>format is a special zip format for Python packages. These are Anaconda whl install instructions.
Here's how to install a whl package in the <a href="https://store.continuum.io/cshop/anaconda/">Anaconda </a>Python distribution from <a href="http://www.continuum.io/">Continuum Analytics</a>.
<h1>Download the 'wheel'</h1>
Find and download your whl file. In this example I'm going to be installing the 'Shapely' geometry package, available from here: <a href="http://www.lfd.uci.edu/~gohlke/pythonlibs/#shapely">http://www.lfd.uci.edu/~gohlke/pythonlibs/#shapely</a>
You'll want to pick the right version of Python - you probably want version 2.7, but check your Anaconda distribution. You'll also need to pick between 32- or 64-bit.
<h4><a href="https://www.amazon.co.uk/gp/search/ref=as_li_qf_sp_sr_il_tl?ie=UTF8&amp;tag=deparkescouk-21&amp;keywords=python&amp;index=aps&amp;camp=1634&amp;creative=6738&amp;linkCode=xm2&amp;linkId=d3a1421318db00a92b4ef19fc11de057">Search for Python books on Amazon</a></h4>
<h1>Install With Pip</h1>
<a href="https://store.continuum.io/cshop/anaconda/">Anaconda </a>prefers to use its own '<a href="http://conda.pydata.org/">conda</a>' package manager, but it's also possible to install packages using <a href="https://pypi.python.org/pypi/pip/">pip </a>- the <a href="https://python-packaging-user-guide.readthedocs.org/en/latest/current.html">PyPA recommended</a> tool for installing Python packages. See a comparison of the package managers <a href="http://stackoverflow.com/questions/20994716/what-is-the-difference-between-pip-and-conda">here</a>.
Once you've downloaded the correct wheel file, open up the '<strong>Anaconda Command Prompt</strong>' and navigate to the folder containing the downloaded wheel.
To install this Shapely whl file I run:

```bash
pip install Shapely‑1.5.5‑cp27‑none‑win32.whl
```

which will install the Shapely package to somewhere like:

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
