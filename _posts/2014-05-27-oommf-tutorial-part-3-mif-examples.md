---
layout: post
title: 'OOMMF Tutorial Part 3: mif Files and Examples'
date: 2014-05-27 11:00:29.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- examples
- featured
- oommf tutorial
- oommf tutorial part 3
author:
  display_name: deparkes
permalink: "/2014/05/27/oommf-tutorial-part-3-mif-examples/"
---
Part 3 of this getting started tutorial for OOMMF introduces mif problem files and some of the example files that come with OOMMF distributions.
<a title="OOMMF Tutorial Part 1: Download OOMMF and Tcl/tk" href="{{site.baseurl}}/2014/05/18/oommf-tutorial-part-1-download-oommf-and-tcltk/">Part 1</a> covered downloading and installing OOMMF.
<a title="OOMMF Tutorial Part 2: Running OOMMF" href="{{site.baseurl}}/2014/05/22/oommf-tutorial-part-2-running-oommf/">Part 2</a> covered running OOMMF.

<h1>mif Files</h1>
Micromagnetic calculations in OOMMF are set up in a mif problem file. A mif file is written in tcl and includes<span style="line-height: 1.5;"> components such the calculation region, mesh size, initial magnetisation configuration and magnetic anisotropy energies. </span>Some of the elements of a mif file are required, whereas some depend on exactly what you are trying to simulate.
Rather than write your mif file from scratch, it's often best to use an existing file as a starting point and modify it to your needs.

[https://youtu.be/UMnJ_j4V0hs](https://youtu.be/UMnJ_j4V0hs)
OOMMF comes with a number of very useful example files, but it can sometimes be difficult to know where to start. I've selected here some of those that I've found useful and picked out the relevant sections of the files.
<a title="Problem Specification File" href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/Problem_Specification_File_.html">OOMMF Help on mif files</a>
<h1>OOMMF Examples</h1>
OOMMF comes with a 3d micromagnetic problem solver, Oxsii. Getting started with this can be a bit daunting, but thankfully it comes with a range of examples which you can use to build up the different component that you need for your simulation system.
I've picked out some of the examples that I've found useful in the past. For each one I've tried to pick out and highlight the most relevant sections.
You can find these and many more similar examples in oommf/app/oxs/examples
[https://www.youtube.com/watch?v=4OORBusgFoY](https://www.youtube.com/watch?v=4OORBusgFoY)
<h2>Example 1: Exchspring.mif</h2>
<ul>
<li> Multiple layers</li>
<li>Setting initial magnetisation</li>
<li>Uniaxial anisotropy</li>
<li>Simulating and applied field</li>
</ul>

| ![Exchangepring.mif: Multiple layers, initial magnetisation, uniaxial anisotropy, applied field]({{site.baseurl}}/assets/2014/05/Slide4.png) |
|:--:|
| *Exchangepring.mif: Multiple layers, initial magnetisation, uniaxial anisotropy, applied field* |

<h2>Example 2: Squarecubic.mif</h2>
<ul>
<li>cubic anisotropy</li>
</ul>

| ![Squarecubic.mif: use of cubic anisotropy in a problem file.]({{site.baseurl}}/assets/2014/05/Slide5-300x300.png) |
|:--:|
| *Squarecubic.mif: use of cubic anisotropy in a problem file.* |

<h2>Example 3: Imageatlas.mif</h2>
<ul>
<li>Using a bitmap to define the simulation geometry.</li>
<li>Colours define different regions within the simulation.</li>
<li>Setting anisotropy and initial magnetisation for different regions.</li>
</ul>

| ![Imageatlas.mif: Using a bitmap to define simulation regions.]({{site.baseurl}}/assets/2014/05/Slide6-300x225.png) |
|:--:|
| *Imageatlas.mif: Using a bitmap to define simulation regions.* |

<h2>Example 4:varalpha.mif</h2>
<ul>
<li>Use a 'proc' to define a time-varying field</li>
</ul>

| ![Varalpha.mif: using a proc to define a time-varying magnetic field.]({{site.baseurl}}/assets/2014/05/Slide7-300x276.png) |
|:--:|
| *Varalpha.mif: using a proc to define a time-varying magnetic field.* |

<h2>Example 5: one of my own</h2>
<ul>
<li>Setting automatic output</li>
</ul>
```tcl
# Create destinations
Destination my_graph mmGraph
Destination my_archive mmArchive
Destination my_display mmDisp
# Specify what should be saved
Schedule DataTable my_graph Step 1
Schedule DataTable my_archive Step 1
Schedule Oxs_TimeDriver::Magnetization my_display Stage 1
Schedule Oxs_TimeDriver::Magnetization nbsp;my_display Step 1
```
A step is a single iteration, while a stage is for example reaching equilibrium after one value of applied field.
<h1>Going further</h1>
As you carry out your own simulations and introduce more complicated elements you'll begin to build up a library of your own useful examples. Rather than starting from scratch each time you'll be able to build on these.


<a href="{{site.baseurl}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.baseurl}}/assets/2014/05/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
