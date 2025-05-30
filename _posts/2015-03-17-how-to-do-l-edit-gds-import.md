---
layout: post
title: How To Do L-Edit GDS Import
date: 2015-03-17 19:54:56.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- L-edit
tags:
- design
- gds
- l-edit
- layout
author:
  display_name: deparkes
permalink: "/2015/03/17/how-to-do-l-edit-gds-import/"
---
<h1>How to Do L-Edit GDS Import</h1>
GDS is a common data format for dealing with layout files. L-edit is a very powerful software package, but unfortunately for a new user even simple tasks like importing files can prove to be problematic.
To help you out, here is a quick guide for how to do <a href="https://www.tannereda.com/l-edit-pro">L-edit</a> GDS import.
<h3><a title="Layout Design Software" href="{{site.baseurl}}/2015/02/21/layout-design-software/">Check out my picks for different layout design software</a></h3>
<h2>Make Sure You Have an L-Edit Design Open</h2>
You can't just import a GDS file into a blank document - you need to open an existing or <strong>New Design</strong> first:

| ![L-edit GDS import - new file]({{site.baseurl}}/assets/2015/03/NewFile.png) |
|:--:|
| *L-edit GDS import - new file* |

<h2>Select 'Import Mask Data'</h2>
To begin the import, go to File-&gt;Import Mask Data-&gt;GDSII...

| ![L-edit GDS import  - Import mask data]({{site.baseurl}}/assets/2015/03/ImportMaskData.png) |
|:--:|
| *L-edit GDS import  - Import mask data* |

You will have the chance to select the gds import options:

| ![L-edit GDS import - GDS settings]({{site.baseurl}}/assets/2015/03/ImportGDS_pt2.png) |
|:--:|
| *L-edit GDS import - GDS settings* |

If your import works correctly, you should end up with something like this:

| ![L-edit GDS import - end result]({{site.baseurl}}/assets/2015/03/ImportGDS_pt3.png) |
|:--:|
| *L-edit GDS import - end result* |
