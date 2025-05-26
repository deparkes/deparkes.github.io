---
layout: post
title: How to install revtex4-1 in Ubuntu
date: 2013-03-27 15:43:45.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- Latex
tags:
- latex
- linux
- linux mint
- revtex
- ubuntu
author:
  display_name: deparkes
permalink: "/2013/03/27/revtex4-1-in-ubuntu/"
---
<h1>How to install revtex4-1 in Ubuntu...</h1>
I was having trouble installing <a href="https://journals.aps.org/revtex">revtex4-1</a> in <a href="http://www.ubuntu.com/">Ubuntu </a>(well, actually <a href="http://www.linuxmint.com/">Linux Mint</a>, but it's based on Ubuntu...). Suggestions to use revtex4-1.zip did not seem to work for me.
<h1>...use the 'texlive-publishers' package</h1>
In the end I found the solution to be a package "texlive-publishers" (<a href="http://ubuntuforums.org/archive/index.php/t-995840.html">http://ubuntuforums.org/archive/index.php/t-995840.html</a>)
To get revtex4-1 to work I just ran this in the terminal:

```bash
$ sudo apt-get install texlive-publishers
```
Simple.
<div id="yui_3_16_0_1_1423940581800_15312" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Bjørn Bulthuis's photostream" href="https://www.flickr.com/photos/bjornb/" data-rapid_p="25" data-track="attributionNameClick">Image: Bjørn Bulthuis; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-sa/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="52">Some rights reserved</a><a class="owner-name truncate" title="Go to Bjørn Bulthuis's photostream" href="https://www.flickr.com/photos/bjornb/" data-rapid_p="25" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1423940581800_15542" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
