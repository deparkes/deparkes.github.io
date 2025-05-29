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
