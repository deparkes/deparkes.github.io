---
layout: post
title: 'OOMMF Tutorial Part 5: OOMMF Tips'
date: 2014-10-16 17:48:07.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- oommf
- oommf tutorial
- oommf tutorial part 5
author: deparkes
permalink: "/2014/10/16/oommf-tutorial-part-5-oommf-tips/"
---
An assortment of OOMMF tips that will hopefully make your OOMMF life easier.
<h1>Simulation cell size</h1>
One of the easiest ways to speed up your simulation is to increase the cell size. Unfortunately this is also one of the easiest ways to get spurious results.
Check out this <a href="https://www.southampton.ac.uk/~rpb/thesis/node33.html">explanation </a>of discretization, exchange length and getting your cell size right.
<h1>Periodic Mesh</h1>
I've mentioned this <a title="How to use OOMMF Oxs_PeriodicRectangularMesh" href="{{site.url}}/2014/10/16/use-oommf-oxs_periodicrectangularmesh/">before</a>, but it is handy to know, so I've included it here. Using a periodic mesh can be useful for shortening computation times and get around end-effect issues such as stray fields.
<h1>Variable substitution</h1>
Variable subsitution allows you to set variables at the start of your mif file and have the script use or modify them later on.
It's such a basic thing, and I know it's in the user <a href="https://math.nist.gov/oommf/doc/" target="_blank">manual</a>, but I remember it taking a little while for me to figure out at first. You can enable variable substitution in a specify block using 'subst' and a pair of additional brackets, as in this example

```tcltk
# Divide image file into mesh, periodic in x direction
Specify Oxs_PeriodicRectangularMesh:mesh [ subst {
cellsize {$xcell $ycell $zcell}
atlas :atlas
periodic x
} ]
```
without these extra terms OOMMF won't know what to do with $var1 $var2 etc in the Specify block.
<h1>Syntax-highlighting</h1>
Do yourself a favour and use a sensible text editor like <a title="Notepad2-mod for editing OOMMF Files" href="{{site.url}}/2014/05/13/notepad2-mod-for-editing-oommf-files/" target="_blank">notepad-2mod</a> which can do syntax highlighting on the OOMMF mif files.
Trying to find that rogue brace or missing space is made much more difficult than it needs to be when you're just using vanilla notepad.
<h1>Parallel Processing</h1>
Another way of speeding up OOMMF, which won't damage the physics.
Current versions of OOMMF come with parallelisation enabled (You'll have to make sure you've installed the correct versions of Tcl/Tk for it to activate).
Parallel processing can give a dramatic improvement in <a href="https://math.nist.gov/~MDonahue/pubs/parallel-oommf-20090518.pdf">performance</a> [pdf]. In my own tests I've seen as much as a 5x improvemetn in simulation times for 8 cores:


| ![You can get dramatic performance increases by enabling parallelization in OOMMF.]({{site.url}}/assets/2014/10/Graph4-1024x715.png) |
|:--:|
| *You can get dramatic performance increases by enabling parallelization in OOMMF.* |

<div id="yui_3_16_0_1_1413480505435_34000" class="view attribution-view clear-float">
<div class="attribution-info">
<a title="OOMMF Tutorial Part 6: OOMMF scripting with python" href="{{site.url}}/2014/10/28/oommf-tutorial-part-6-oommf-scripting-python/">Part 6</a> of this OOMMF Tutorial: Scripting with python</div>
<a href="{{site.url}}/oommf/oommf-tutorial/">
<img class=" aligncenter" src="{{site.url}}/assets/2014/10/OOMMF_tutorial.png" alt="OOMMF Tutorial" width="200" height="142" border="0">
