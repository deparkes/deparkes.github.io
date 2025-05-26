---
layout: post
title: OOMMF Automatic Output
date: 2015-02-05 15:12:43.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- automatic output
- oommf
- scripting
author:
  display_name: deparkes
permalink: "/2015/02/05/oommf-automatic-output/"
---
To set OOMMF automatic output, just add lines similar to these to the bottom of your mif file.
You can modify the detail to select which parameters to output, and how frequently.

```tcltk
# Create destinations
Destination my_graph mmGraph
Destination my_archive mmArchive
Destination my_display mmDisp

# Specify what should be saved
Schedule DataTable my_graph Step 1
Schedule DataTable my_archive Step 1
Schedule Oxs_TimeDriver::Magnetization my_display Stage 1
Schedule Oxs_TimeDriver::Magnetization my_display Step 1
```
Watch this video for more about OOMMF automatic outputs:
[https://www.youtube.com/watch?v=-mJew6JYRZk](https://www.youtube.com/watch?v=-mJew6JYRZk)
<div id="yui_3_16_0_1_1424075039224_695" class="view attribution-view requiredToShowOnServer clear-float photo-attribution">
<div class="attribution-info">
<a class="owner-name truncate" title="Go to walknboston's photostream" href="https://www.flickr.com/photos/walkn/" data-rapid_p="25" data-track="attributionNameClick">Image: walknboston; </a><a class="photo-license-url" href="https://creativecommons.org/licenses/by/2.0/" target="_newtab" rel="license cc:license" data-rapid_p="29">Some rights reserved</a><a class="owner-name truncate" title="Go to walknboston's photostream" href="https://www.flickr.com/photos/walkn/" data-rapid_p="25" data-track="attributionNameClick">
</a>
<div id="yui_3_16_0_1_1424075039224_696" class="view follow-view clear-float photo-attribution"></div>
</div>
</div>
