---
layout: post
title: 'OOMMF Tutorial Part 4: OOMMF Analysis Tools'
date: 2014-06-10 14:01:40.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- featured
- oommf
- oommf tutorial
- oommf tutorial part 4
- tutorial
author:
  display_name: deparkes
permalink: "/2014/06/10/oommf-tutorial-part-4-oommf-analysis-tools/"
---
When doing micromagnetic simulations it is easy to end up with hundreds of output files, so part four of this OOMMF Tutorial covers some of the tools available for analysing OOMMF data.  This list isn't exhaustive - if I've missed out your favourite - please leave a comment!
OOMMF outputs two types of data: vector, such as magnetisation or demagnetising fields; and scalar such as energies and total magnetisations. There are tools available for processing both types.
If you haven't already please check out parts <a title="OOMMF Tutorial Part 1: Install OOMMF and Tcl/tk" href="{{site.baseurl}}/2014/05/18/oommf-tutorial-part-1-install-oommf-and-tcltk/">one</a>, <a title="OOMMF Tutorial Part 2: Running OOMMF" href="{{site.baseurl}}/2014/05/22/oommf-tutorial-part-2-running-oommf/">two </a>and <a title="OOMMF Tutorial Part 3: mif Files and Examples" href="{{site.baseurl}}/2014/05/27/oommf-tutorial-part-3-mif-examples/">three</a> of this tutorial.
<h1>Built-in analysis tools</h1>
OOMMF already comes with some simple tools for viewing, saving and analysing your data. They're not necessarily the most advanced, or easy to use, but they allow at least for quickly checking progress of calculations so can be invaluable.
<h2>mmDisp</h2>
The most straight forward tool for analysing vector data is to use mmDisp. You can even set OOMMF to automatically display to mmDisp as the calculation runs.

| ![Using mmDisp to examine magnetisation vector data.]({{site.baseurl}}/assets/2014/06/Built-in-analysis-300x225.png) |
|:--:|
| *Using mmDisp to examine magnetisation vector data.* |

With mmDisp you can view different components of vector data as well as derivatives. You can select from a number of different colour schemes for both image pixels and arrows.
See more about mmDisp in the OOMMF <a href="http://math.nist.gov/oommf/doc/userguide/userguide/Vector_Field_Display_mmDisp.html">documentation</a>.
<h2> mmGraph</h2>
mmGraph is the scalar equivalent of mmDisp. It lets you quickly and easily view the data table output from your OOMMF simulations. In terms of functionality the plotter is quite straightward, so you'll probably want to use separate software for producing production quality graphs.

| ![Built-in graph viewer. Plot different scalar parameters such as simulation time, total energy, magnetisation.]({{site.baseurl}}/assets/2014/06/mmGraph_example-282x300.png) |
|:--:|
| *Built-in graph viewer. Plot different scalar parameters such as simulation time, total energy, magnetisation.* |

You can export the plotted data as a graphic, but I often cheat by using Alt+Print Screen to copy the window to the clip board. I find this handy for quickly producing summaries of simulations.
See more about mmGraph in the OOMMF <a href="http://math.nist.gov/oommf/doc/userguide/userguide/Data_Graph_Display_mmGraph.html">documentation</a>.
<h2>External Tools</h2>
There are a number of different external tools for analysing oommf data. Many of them are listed on the oommf nist website (link).
I will focus on OOMMFTools since that is the one that I am most familiar with.
<h3>OOMMFTools</h3>
<a href="https://github.com/deparkes/OOMMFTools">OOMMFTools </a>is a suite of tools designed to make it easier to analyse OOMMF output data. The tools come in GUI and a command line form.
The suite of tools makes it easy to convert single or multiple OOMMF files into other formats more readily viewed or further processed than the standard output formats.


| ![Options for processing oommf data with oommf tools.]({{site.baseurl}}/assets/2014/06/Slide13-300x225.png) |
|:--:|
| *Options for processing oommf data with oommf tools.* |

The basic operations available in OOMMFTools are vector format -&gt; matlab/python readable file; vector format -&gt; bitmap, video; scalar data table -&gt; plain text.
<h2>odt2dat.py</h2>
To make the scalar data table easier to understand it is good to convert it to a plain text ascii .dat file. odt2dat.py lets you do this.
The column headings are shown below. Once you know the number of the column you can easily <a title="Labtalk plotting in Origin" href="{{site.baseurl}}/2013/04/18/labtalk-plotting-in-origin/">plot it</a> against any other column using your favourite graphing software.
```
Total energy
Energy calc count
Max dm/dt
dE/dt
Delta E
FeGa UniformExchange Energy
Max Spin Ang
Stage Max Spin Ang
Run Max Spin Ang
Strain Energy
UZeeman Energy
B
Bx
By
Bz
Demag Energy
Iteration
Stage iteration
Stage
mx
my
mz
Last time step
Simulation time
```
<h2>omf2mat.py</h2>
Easily convert vector outputs into matlab .mat files or python pickle files. From there it is easy to extract line scans and perform more advanced analysis on individual cells in the mesh.
I'll show a sample matlab m file to read in the resulting .mat file in a future post.
<h2>avf2bmp.py</h2>
This is essentially a wrapper for the built-in OOMMF command line program avf2ppm.py. It uses your OOMMF install to convert vector files to bitmaps.

```bash
avf2bmp.py my_omf.omf
```

for single files, or run

```bash
avf2bmp.py *.omf
```

for all .omf files in the directory.
<h2>bmp2avi.py</h2>
One of the most striking ways to present time-evolving data is as a video. OOMMFTools uses ffmpeg (available as part of <a href="http://www.imagemagick.org/">ImageMagick</a>) to convert a folder of bitmaps into an avi video.
<h1>You might also consider</h1>
There are some other tools that I'm not so familiar with that you might also be interested in using. The best place to find analysis tools is probably the OOMMF <a href="http://math.nist.gov/oommf/contrib/">website</a>.
<a href="{{site.baseurl}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.baseurl}}/assets/2014/06/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
