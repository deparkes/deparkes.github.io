---
layout: post
title: Images From OOMMF Outputs
date: 2017-12-22 15:00:38.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- bitmap
- images
- oommf
author:
  display_name: deparkes
permalink: "/2017/12/22/images-from-oommf-outputs/"
---
Once you have <a href="{{site.baseurl}}/2014/05/18/oommf-tutorial-part-1-install-oommf-and-tcltk/">installed OOMMF</a>, and <a href="{{site.baseurl}}/2014/05/22/oommf-tutorial-part-2-running-oommf/">ran some simulations</a>, you will at some point probably want to produce some images of your simulation outputs. It's not obvious how to do this, so this post explains how you can make images from oommf outputs using the command line tool 'avf2ppm' that comes with OOMMF.
<h1>OOMMF Vector Outputs</h1>
OOMMF can produce <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Vector_Field_File_Format_OV.html">vector outputs</a> for representing magnetisation or magnetic fields. These vector outputs can viewed and explored in the <a href="https://math.nist.gov/oommf/mmdisp/mmdisp.html">mmDisp</a> vector field display tool. Often, though, it would be good to export slices of these vector outputs as bitmaps (such as for figures in presentations or papers).
<a href="{{site.baseurl}}/assets/2017/12/antidots-Oxs_TimeDriver-Magnetization-04-0002710.bmp"><img class="aligncenter wp-image-3699 size-full" src="{{site.baseurl}}/assets/2017/12/antidots-Oxs_TimeDriver-Magnetization-04-0002710.bmp" alt="Images From OOMMF Outputs - example output" width="640" height="337"></a>
It is technically possible to 'save as' a bitmap file by loading a vector file from the <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Vector_Field_Display_mmDisp.html">mmDisp</a> window. I would not recommend this though as it slow to do for multiple files and it is easy to lose track of any naming conventions or metadata held in the filename.
<h3>Automatic Vector Outputs</h3>
If you haven't already, I also suggest you read my short post about<a href="{{site.baseurl}}/2015/02/05/oommf-automatic-output/"> automating outputs in OOMMF</a>. This allows you to set OOMMF to save outputs at set intervals during the simulation rather than having to do so manually via the gui.
<h1>A Built-in Tool</h1>
OOMMF, thankfully has a useful built-in tool for converting vector outputs (describing magnetisation or magnetic fields) to bitmaps. Rather confusingly, this tool is called <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Making_Bitmaps_from_Vector_.html">avf2ppm</a>, in reference to an uncompressed bitmap format called '<a href="https://en.wikipedia.org/wiki/Netpbm_format#PPM_example">ppm</a>' which is rarely encountered outside of specialist circles. Naming aside, the avf2ppm tool is actually easy to use, and has <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Making_Bitmaps_from_Vector_.html">comprehensive documentation</a> on the OOMMF website.

I recommend you read the full documentation, but if you just want to get started with making images from oommf outputs, then you can follow these simplified instructions (this is tested in Linux, but the function should be mostly the same in windows).
Change directory to the one containing the vector files you want to convert (by default OOMMF outputs to the same directory as the mif file that it ran). In this directory there should be some 'omf' (magnetisation) or 'ohf' (H-field) files. Now run this command (making sure you set the path to your oommf.tcl correctly):

```bash
tclsh /path/to/oommf.tcl avf2ppm -format B24 *.omf
```

| ![Images From OOMMF Outputs - command to type]({{site.baseurl}}/assets/2017/12/oommf_vector_convert1.png) |
|:--:|
| *Images From OOMMF Outputs - command to type* |

  This command should take all .omf files in the directory and produce corresponding .bmp files with the same name. If you only want to convert a single vector file, then give the file name rather than the wildcard *.omf.

| ![Images From OOMMF Outputs - output log]({{site.baseurl}}/assets/2017/12/oommf_vector_convert2.png) |
|:--:|
| *Images From OOMMF Outputs - output log* |

Since we only specified a few options in this command, avf2ppm will mainly be using defaults. You may want to review the <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Making_Bitmaps_from_Vector_.html">OOMMF documentation for avf2ppm</a> to make sure you are happy with what those defaults are.
<h2>Configuration Files</h2>
avf2ppm has the option to provide a separate configuration file. The default parameters will probably be fine in many cases, but you may wish to make alterations. You can see what the <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Making_Bitmaps_from_Vector_.html#sec:avf2ppmconfig">default configuration file</a> looks like on the OOMMF documentation pages - the options are fairly clear, and there is <a href="https://math.nist.gov/oommf/doc/userguide20a0/userguide/Vector_Field_Display_mmDisp.html#sec:mmdispconfig">further documentation available</a> too.
