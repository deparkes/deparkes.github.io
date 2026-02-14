---
layout: post
title: L-Edit Export GDS File How To
date: 2015-03-17 21:34:39.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- L-edit
tags:
- export
- gds
author: deparkes
permalink: "/2015/03/17/l-edit-export-gds-file-how-to/"
---
<h1>L-Edit How to Export a GDS File</h1>
<a href="https://www.tannereda.com/l-edit-pro">L-Edit</a>, part of the <a href="https://www.tannereda.com/">Tanner Tools</a> suite of circuit design software uses it's own 'tda' file format. If you want to send your designs to other people for review or production, you're probably going to want to use the GDS format.
This short guide shows you how to <strong>export your file as a GDS</strong>.
<h3><a title="How To Do L-Edit GDS Import" href="{{site.url}}/2015/03/17/how-to-do-l-edit-gds-import/">Find out how to import a GDS file into L-Edit</a></h3>
<h1>Export Mask Data</h1>
It's quite easy to export a GDS file in L-Edit. Just go to File -&gt; Export Mask Data -&gt; GDSII...

| !["L-Edit Export GDS - file menu]({{site.url}}/assets/2015/03/ExportGDS-menu.png) |
|:--:|
| *L-Edit Export GDS - file menu* |

<h1>Choose GDS Export Settings</h1>
You will be presented with a dialogue to select the <strong>GDS export settings</strong>. You can probably leave most of these as default, but you may wanto change the <strong>output file name</strong> or location, or select whether you want to export the <strong>active cell</strong> only, or <strong>all cells</strong>.

<h1>Check The Output Log</h1>
When you output a GDS file from L-edit a log file will be produced inside  your L-Edit design. This file will tell you the export settings and let you know  if there have been any warnings or errors.

| !["L-Edit Export GDS - messages]({{site.url}}/assets/2015/03/ExportGDS-messages.png) |
|:--:|
| *L-Edit Export GDS - messages* |
