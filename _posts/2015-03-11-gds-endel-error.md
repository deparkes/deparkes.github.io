---
layout: post
title: GDS ENDEL Error
date: 2015-03-11 15:32:44.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
tags:
- design
- ecp
- fabrication
- gds
author:
  display_name: deparkes
permalink: "/2015/03/11/gds-endel-error/"
---
<h1>How to Get Around the Missing ENDEL Error in ECP</h1>
Get around the GDS ENDEL Error: "<strong>GDS Error: Missing ENDEL!</strong>" in ECP by first flattening your gds file.
<h1>ECP - Exposure Control Program</h1>
I use the <a href="http://www.abeamtech.com/?dir=products/Xenos&amp;pg=index">ECP CAD program</a> to write electron beam lithography patterns. Although ECP has its own primitive pattern editor, I prefer to use a separate, dedicated <a title="Layout Design Software" href="{{site.baseurl}}/2015/02/21/layout-design-software/">layout design program</a>.
The standard layout design file format is <a href="http://www.rulabinsky.com/cavd/text/chapc.html">GDS</a>, and ecp is capable of converting from gds to the ECP pattern and control files. Unfortunately, ECP can't always cope with
<h1>GDS ENDEL Error</h1>
Sometimes when I try to load a gds file into ECP I get the error "GDS Error: Missing ENDEL!":

| ![GDS Error: Missing ENDEL!]({{site.baseurl}}/assets/2015/03/ECP_Error.png) |
|:--:|
| *GDS Error: Missing ENDEL!* |

This makes it impossible to load and convert that particular GDS file.
You can solve this problem by flattening the gds file before trying to load it into ECP.
<h1>Use KLayout to Flatten GDS File</h1>
You can flatten your gds file using <a href="http://www.klayout.de/">KLayout</a>, an open source layout editor.
Just load up KLayout in <a href="http://www.klayout.de/doc/manual/edit_mode.html">editor mode</a>, then select Edit -&gt; Cell -&gt; Flatten Cell.
<h3><a title="Layout Design Software" href="{{site.baseurl}}/2015/02/21/layout-design-software/">See my other suggestions for Layout Design Software</a></h3>

| ![GDS ENDEL Error]({{site.baseurl}}/assets/2015/03/KLayout_Flatten.png) |
|:--:|
| *GDS ENDEL Error* |

Save the resulting gds file and you should be able to load this into ECP without any problems.
