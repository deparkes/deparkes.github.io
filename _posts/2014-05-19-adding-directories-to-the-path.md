---
layout: post
title: How to Add Directories to Path
date: 2014-05-19 14:02:30.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- linux
- path
- windows
author:
  display_name: deparkes
permalink: "/2014/05/19/adding-directories-to-the-path/"
---
Adding a directory to the system path allows us to run executables win that directory from the command line.
The PATH is an example of an environment variable. It is a list of directories where executable programs can be found. If we want our scripts or programs to be available from the command line we must add its directory to the PATH variable.
It can be really useful to add additional directories to the path. For me this generally happens if I have a useful script or program that I want to be able to run from any directory on my computer.
<!--more-->
The approaches to do this are different for linux and windows.
<h1>Add Directories to Path</h1>
<h2>Windows</h2>
The procedure for adding a folder to the path in windows 7 is described here:
<a href="http://www.computerhope.com/issues/ch000549.htm">http://www.computerhope.com/issues/ch000549.htm</a>
<h2>Linux</h2>
In Linux, adding to the path can generally be done by opening a terminal and typing:

```bash
export PATH=$PATH:~/scripts
```

Where here ~/scripts is the folder we wish to add to the path.

This ammendment of the path will be lost when we close our terminal window or logout. To make this path change permanent we can adjust the .bashrc file:

```bash
echo 'export PATH=$PATH:/usr/local/bin' >> ~/.bashrc
```
.bashrc is run each time you login or the terminal is loaded, so the path will be amended each time too.
We can check the current path by entering:
```bash
echo $PATH
```
 
<div id="yui_3_16_0_1_1423943112907_47407" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Kirt Edblom's photostream" href="https://www.flickr.com/photos/27190564@N02/" data-rapid_p="25" data-track="attributionNameClick">Image: Kirt Edblom; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-sa/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="30">Some rights reserved</a><a class="owner-name truncate" title="Go to Kirt Edblom's photostream" href="https://www.flickr.com/photos/27190564@N02/" data-rapid_p="25" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1423943112907_47638" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
