---
layout: post
title: 'OOMMF 1.2a5: Increase OOMMF iteration limit'
date: 2013-05-10 08:38:20.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- OOMMF
tags:
- iterations
- oommf
- ovf
- simulation
- tcl
author:
  display_name: deparkes
permalink: "/2013/05/10/oommf-1-2a5-increase-maximum-number-of-iterations/"
---
<h1>How to Increase OOMMF Iteration Limit</h1>
I've recently had to increase OOMMF iteration limit. This little guide shows the simple steps I took.
I was having trouble saving the output from more than 1e7 iterations. The simulation would run, but the vector files would not be saved. I found I could get around this problem by modifying a line in the file<strong> /oommf/app/oxs/base/output.tcl</strong>
There are two lines which set the format of the output file names:

```
# Formats for embedding into filenames
public variable iter_fmt = "%07d"
public variable stage_fmt = "%02d"
```

If you find that you are reaching the maximum number of iterations (or stages) that can be saved, then you can simply modify this line:

```
# Formats for embedding into filenames
public variable iter_fmt = "%012d"
public variable stage_fmt = "%02d"
```
Which will allow the vector files from more iterations to be saved.
<div id="yui_3_16_0_1_1423923556097_237556" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<div id="yui_3_16_0_1_1423926486441_21261" class="view attribution-view clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Morgen Bell's photostream" href="https://www.flickr.com/photos/mrvelocipede/" data-rapid_p="25" data-track="attributionNameClick">Image: Morgen Bell; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by-nc/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="30">Some rights reserved</a>
<div id="yui_3_16_0_1_1423926486441_21492" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
<div id="yui_3_16_0_1_1423926486441_21261" class="view attribution-view clear-float photo-attribution"></div>
</div>
</div>
