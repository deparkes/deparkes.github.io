---
layout: post
title: 'OOMMF Tutorial Part 1: Install OOMMF and Tcl/tk'
date: 2014-05-18 14:18:29.000000000 +01:00
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
- oommf tutorial
- oommf tutorial part 1
- tutorial
author: deparkes
permalink: "/2014/05/18/oommf-tutorial-part-1-install-oommf-and-tcltk/"
---
OOMMF can be an incredibly useful tool for micromagnetic simulations, but it can also be frustrating to start with. This tutorial aims to get you up and running with OOMMF and in a position to start running your own simulations.
In this first part we look at downloading and installing the correct version of OOMMF for our system.
For the full OOMMF user guide, please visit <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/">https://math.nist.gov/oommf/doc/userguide12a5/userguide/</a>
<h1>Downloading and installing OOMMF</h1>
Once installed, OOMMF works much the same in Windows and Linux, but there are some differences in which files we need to download and the install procedures we go through. In both cases we need to get OOMMF and the appropriate tcl/tk for our system.
For full install instructions please see: <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/Basic_Installation.html">https://math.nist.gov/oommf/doc/userguide12a5/userguide/Basic_Installation.html</a>
<h2>Windows</h2>
The easiest way to run OOMMF on windows is to download a precompiled binary. Download the most recent alpha release (currently 1.2a5) from <a href="https://math.nist.gov/oommf/software.html">https://math.nist.gov/oommf/software.html</a>
To run OOMMF you'll need the right tcl/tk version installed on you system. The easiest place to find this is <a href="https://www.activestate.com/activetcl/downloads" target="_blank">active tcl</a>.
Once tcl/tk is installed you should just be able to run oommf from the oommf.tcl icon in the oomf root folder (e.g. C:\oommf-1.2a5\).
This should bring up the OOMMF window.
For what to do next, please see <a title="OOMMF Tutorial Part 2: Running OOMMF" href="{{site.baseurl}}/2014/05/22/oommf-tutorial-part-2-running-oommf/">part 2</a> of this tutorial.
<h2>Linux</h2>
The install procedure for linux is slightly more involved as we must compile OOMMF from source, which can throw up issues, particularly if we don't have root access or the correct development versions of tcl/tk installed.
https://www.youtube.com/watch?v=VeWip2L_1zs
<h3><a href="{{site.baseurl}}/2012/06/02/installing-oommf-on-ubuntu-11-04/">Read more about installing OOMMF on Linux</a></h3>
<h3>If You Don't Have Root Access</h3>
If you have no root access and your system is missing the correct dev versions of tcl/tk then see <a title="Install OOMMF 1.2a5 without root" href="{{site.baseurl}}/2013/06/24/install-oommf-1-2a5-without-root/">here</a> for further install instructions.
Once you've installed OOMMF, please see <a title="OOMMF Tutorial Part 2: Running OOMMF" href="{{site.baseurl}}/2014/05/22/oommf-tutorial-part-2-running-oommf/">part 2</a> of this tutorial for running the program and loading problem files.
<a href="{{site.baseurl}}/oommf/oommf-tutorial/">

<img class=" aligncenter" src="{{site.baseurl}}/assets/2014/05/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
