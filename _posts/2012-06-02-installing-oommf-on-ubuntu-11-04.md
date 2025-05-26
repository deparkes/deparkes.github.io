---
layout: post
title: Installing OOMMF on Ubuntu 11.04
date: 2012-06-02 15:14:28.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- linux
- micromagnetic
- oommf
- ubuntu
author:
  display_name: deparkes
permalink: "/2012/06/02/installing-oommf-on-ubuntu-11-04/"
---
<h1>How to install OOMMF in Linux (Ubuntu)</h1>
I have just installed <a title="OOMMF" href="http://math.nist.gov/oommf/oommf.html">OOMMF</a> on Ubuntu 11.04. Not all of the steps I carried out were in the basic<a title="basic installation guide" href="http://math.nist.gov/oommf/doc/userguide11b2/userguide/Basic_Installation.html"> installation guide</a>, so I am putting them here:
EDIT 1: You will need g++ to be able to compile OOMMF. If you don't have it already, type:

```bash
sudo apt-get install build-essential
```
in the command line
EDIT 2: There is now a pre alpha 5 version available from the <a href="http://math.nist.gov/oommf/software-12.html">OOMMF website</a>, which is the <strong>recommended version</strong> to use. The install procedure for this newer version should be essentially as it is described here. As Vimal points out in the comments below you may <strong>have</strong> to use version 1.2a5rc if you have a 64-bit machine.
<h2>Download OOMMF</h2>
Download the source of <a title="OOMMF 1.2 pre alpha 4" href="http://math.nist.gov/oommf/software-12a4pre.html">OOMMF 1.2pre alpha 4</a> and follow the instructions in the install guide to extract the tar.gz.

```bash
gunzip -c oommf11b2_20040115.tar.gz | tar xvf -
```
I moved the resulting folder to /usr/local/bin.
From the oommf root directory run

```bash
tclsh oommf.tcl +platform
```
The resulting errors come about because the default Ubuntu install does not have the necessary development packages for tcl and tk. From the terminal run
<h2>Install the dev packages of tcl/tk</h2>

```bash
sudo apt-get install tcl8.4-dev
sudo apt-get install tk8.4-dev
```
Run tclsh oomm.tcl +platform again and the problems should be sorted.
<h2>Compile OOMMF</h2>
Finally complete the install process from the basic installation guide.
From your oommf directory run:

```bash
tclsh oommf.tcl pimake install
tclsh oommf.tcl
```
<div id="yui_3_16_0_1_1423923556097_203404" class="attribution-info">
<a class="owner-name truncate" title="Go to Andrew Mason's photostream" href="https://www.flickr.com/photos/a_mason/" data-rapid_p="25" data-track="attributionNameClick">Image: Andrew Mason</a>; <a class="photo-license-url" href="https://creativecommons.org/licenses/by/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="29">Some rights reserved</a>
</div>
