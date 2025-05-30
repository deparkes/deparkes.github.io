---
layout: post
title: Trapezoidal Decomposition of Polygons in Python
date: 2015-02-05 21:48:00.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- python
tags:
- geometry
- polygons
- python
- Trapezoidal decomposition
author:
  display_name: deparkes
permalink: "/2015/02/05/trapezoidal-decomposition-polygons-python/"
---
<h1>Trapezoidal Decomposition</h1>
<a href="https://www0.cs.ucl.ac.uk/staff/m.slater/Teaching/CG/1997-98/Solutions/Trap/">Trapezoidal decomposition</a> of polygons involves breaking a polygon into a series of smaller trapezoids.
I've been working on a project - <a href="https://github.com/deparkes/gds2ecp">gds2ecp</a> - to decompose lithography design files into compound shapes that can be written by <a href="https://en.wikipedia.org/wiki/Electron-beam_lithography">electron beam lithography</a>.
I was sure that there would be an existing library to do the polygon decomposition for me, or at least get me part of the way, but I couldn't find exactly what I was after.
<h1>Poly2tri.py</h1>
After much searching I found the library I was looking for:<a href="https://code.google.com/p/poly2tri/source/browse?repo=archive#hg%2Fpython"> poly2tri.py</a>. As far as I can work out this is an archived work as part of the C-based <a href="https://code.google.com/p/poly2tri/">poly2tri </a>project, which is for the <em>triangulation</em> of polygons.
The heavy lifting in poly2tri is done by seidel.py, which uses an algorithm based on "<a href="https://www.cs.princeton.edu/courses/archive/fall05/cos528/handouts/A%20Simple%20and%20fast.pdf">A simple and fast incremental randomized algorithm for computing trapezoidal decompositions and for triangulating polygons</a>", a paper by <a href="https://www-tcs.cs.uni-sb.de/">Raimund Seidel</a>
The algorithm finds the intersections of vertical lines eminating from the vertices building up the original polygon.
<h1>poly2trap.py</h1>
Since poly2tri.py actually goes beyond what I need I've put together a small script - <a href="https://github.com/deparkes/poly2trap/">poly2trap.py</a> - to take the trapezoid output from seidel.py.
All of the hard work is done by seidel.py. The output I'm after is the trapezoids which define the initial shape.
Here's an example of the output which uses the 'dude' example file.

| ![Trapezoidal Decomposition]({{site.baseurl}}/assets/2015/02/test-300x202.png) |
|:--:|
| *Trapezoidal Decomposition* |

<h1>More Testing Needed</h1>

<a href="https://github.com/deparkes/poly2trap/">poly2trap.py</a> is currently almost completely untested - the base code seidel.py seems pretty solid, but since it came from the poly2tri 'archive', I'm not sure if it incorporates all of the features and bug-testing that may have been introduced later.

More testing required...


<a href="{{site.baseurl}}/python-polygons/"><img class="aligncenter wp-image-1479" src="{{site.baseurl}}/assets/2015/02/path4186-300x162.png" alt="python polygons" width="220" height="119"></a>
