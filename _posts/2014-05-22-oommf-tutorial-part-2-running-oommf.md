---
layout: post
title: 'OOMMF Tutorial Part 2: Running OOMMF'
date: 2014-05-22 23:01:27.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- featured
- how to
- oommf
- oommf tutorial
- oommf tutorial part 2
- tutorial
author: deparkes
permalink: "/2014/05/22/oommf-tutorial-part-2-running-oommf/"
---
<h1>Starting OOMMF</h1>
Part 2 of this <a href="https://math.nist.gov/oommf/">OOMMF </a>tutorial covers how to start OOMMF, and some tricks for starting OOMMF via the command line in both Windows and Linux.
For more details on starting OOMMF, please see the official <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/">manual.</a>
<h2>Windows</h2>
One way to load oommf is to double click on the oommf icon. If you installed tcl correctly (see <a title="OOMMF Tutorial Part 1: Download OOMMF and Tcl/tk" href="{{site.baseurl}}/2014/05/18/oommf-tutorial-part-1-download-oommf-and-tcltk/">part 1</a>), then it should load oommf with no problems.
I sometimes find it easier to load oommf from the command line. To help me with this I've made a simple batch script to save having to remember the location of tcl and oommf:

```
REM oommf.bat
tclsh C:\oommf-1.2a5\oommf.tcl %*
```
The %* also allows me to pass command line arguments to oommf, something which will become useful when performing analysis (see future part of this tutorial).
I put this in a scripts folder, which I've added to the path. I can then easily load oommf, or use any of its command line programs from any location. To open a command prompt in a folder I can shift-right click on the folder, or go into the folder and type 'cmd' into the address bar. Running oommf.bat starts oommf from this directory.
See also: <a title="Adding directories to the PATH" href="{{site.baseurl}}/2014/05/19/adding-directories-to-the-path/">Adding directories to the path</a>
<h2>Linux</h2>
In Linux I also use a simple startup script to load oommf:

```bash
# oommf.sh
#!/usr/bin/bash
tclsh /path/to/oommf/oommf.tcl $@
```

Again, I save this in a scripts directory in my home directory. I run sudo chmod u+x oommf.sh and I can then run this when ever you want to load oommf.
See also: <a title="Adding directories to the PATH" href="{{site.baseurl}}/2014/05/19/adding-directories-to-the-path/">Adding directories to the path</a>
<h1>Starting Oxsii</h1>
Whether we started OOMMF from the command line with one of the startup scripts, or by clicking on the icon, we should be greeted with the OOMMF window.

To get to something useful we need to click through the check boxes until we get a list of possible OOMMF sub-programs. We'll be looking at the 3d micromagnetic solver 'Oxsii', so click that.

| ![Clicking through the OOMMF windows to load Oxsii]({{site.baseurl}}/assets/2014/05/Slide3.png) |
|:--:|
| *Clicking through the OOMMF windows to load Oxsii* |


In part 3 of this tutorial we'll look at oommf problem files and some of the examples that come with oxsii.
<a href="{{site.baseurl}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.baseurl}}/assets/2014/05/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
</a>
