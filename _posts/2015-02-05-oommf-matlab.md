---
layout: post
title: 'OOMMF Tutorial Part 9: OOMMF Matlab Import'
date: 2015-02-05 17:17:55.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- matlab
- oommf
author: deparkes
permalink: "/2015/02/05/oommf-matlab/"
---
<h1>How to work with OOMMF files in Matlab</h1>
OOMMF can output both <strong>scalar</strong> and <strong>vector</strong> data. It's easy enough to view this data using the built in programs in OOMMF, but what if you want to process or analyse your data further.
This post shows you how to <strong>convert OOMMF vector files</strong> into a format that you can import into matlab for further processing.
<h1>Convert to a .mat file with OOMMFTools</h1>
The first step to working with OOMMF files in matlab is to<strong> convert them into a '.mat' file</strong> that matlab can read.
To do this I like to use the command line version of <a title="OOMMF Tutorial Part 4: OOMMF Analysis Tools" href="{{site.url}}/2014/06/10/oommf-tutorial-part-4-oommf-analysis-tools/">OOMMFTools</a>.
With this we can just run
```bash
omf2mat.py my_oommf_vector_file.omf
```
Although I've used a .omf file in this example, the same method works with any OOMMF vector file.
This will generate a .mat file containing this information:

```tcltk
GridSize; % cell size used in simulation (x,y,z)
Iteration; % iteration number of this omf file
MIFSource; % The mif file that generated this omf file
OOMMFData; % Actual vector data (x_slice, y_slice, z_slice, (x,y,z))
SimTime; % simulation time of this omf file
Stage; % simulation stage of this file
```
 
<h1>The vector data</h1>
The vector information is stored in the .mat file as <strong>'OOMMFData'</strong>. This is a 3-dimensional grid, representing the simulated geometry, with a (1x3) vector at each point representing the OOMMF vector values themselves.
See the OOMMFTools <a href="https://github.com/deparkes/OOMMFTools/blob/master/OOMMFTools-src/README.txt">Readme </a>for further <strong>discussion of the .mat data</strong>.
Once you have the data in this format, you can just use normal matlab array commands to access and manipulate the data.


<a href="{{site.url}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.url}}/assets/2015/02/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
