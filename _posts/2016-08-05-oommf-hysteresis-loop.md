---
layout: post
title: OOMMF Hysteresis Loop - Making an M vs H curve
date: 2016-08-05 15:00:34.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- hystersis
- oommf
- oommf hystersis
- oommf tutorial
- zeeman
- zeeman energy
author:
  display_name: deparkes
permalink: "/2016/08/05/oommf-hysteresis-loop/"
---
In this post I show you how to simulate an OOMMF hysteresis loop. You can follow this tutorial with more or less any OOMMF oxsi mif file, but I will be using a version of the oxsi exchspring.mif example file that comes with OOMMF, modified to <a href="{{site.baseurl}}/2015/02/05/oommf-automatic-output/">automatically </a>display some outputs.

See also[https://www.youtube.com/watch?v=ojiVtP1LOQI](https://www.youtube.com/watch?v=ojiVtP1LOQI)

<a href="{{site.baseurl}}/2014/05/27/oommf-tutorial-part-3-mif-examples/">Read more about OOMMF example files.</a>

<h1>OOMMF Hysteresis Loops - The Zeeman Energy Term</h1>
In a physical, real-world experiment, a hysteresis loop would be made by ramping up and down a magnetic field. An OOMMF hysteresis loop is achieved in a similar way, by ramping up and down a Zeeman energy term.
The simplest way to include a Zeeman energy term in an OOMMF mif file is with an Oxs_UZeeman term which includes a uniform, homogeneous magnetic field to the simulation.
<a href="http://math.nist.gov/oommf/doc/userguide12a6/userguide/Standard_Oxs_Ext_Child_Clas.html#UZ">Read the official documentation about Zeeman terms in OOMMF</a>.
In the exchspring.mif example, the Zeeman term is:

```tcltk
Specify Oxs_UZeeman [subst {
  multiplier [expr {0.001/$mu0}]
  Hrange {
     {    0   0  0   500  50  0   10 }
     {  500  50  0  -500 -50  0   20 }
     { -500 -50  0   500  50  0   20 }
  }
}]
```

Which uses the a multiplying pre-factor to put 'Hrange' in units of mT. Each line in the Hrange represents a ramping of the simulated magnetic field.
<a href="{{site.baseurl}}/2014/10/16/oommf-tutorial-part-5-oommf-tips/">Find out more about using 'subst' for variable substitution in OOMMF.</a>
The lines are built up of two 3-value vectors for the start and finish field directions, and the number of steps that should be taken between the start and finish vectors. In other words:

```tcltk
{ Hx_start Hy_start Hz_start Hx_end Hy_end Hz_end num_steps}
```

So in this example the field is ramped from 0mT to a field with predominantly positive x component, with some y component in 10 steps. This field is then ramped to an equivalent negative field in 20 steps, before being ramped positive again in a further 20 steps.
<h2>Running The Exchspring.mif Example</h2>
If we run the exchspring.mif example that comes with oxsi (making sure to <a href="{{site.baseurl}}/2014/10/28/oommf-tutorial-part-6-oommf-scripting-python/">capture the output </a>to mmGraph) we can seee that the applied magnetic field changes as the simulation progresses:

| ![oommf hysteresis loop - iteration]({{site.baseurl}}/assets/2016/08/2016-07-30-181542_501x517_scrot.png) |
|:--:|
| *oommf hysteresis loop - iteration* |

To get the characteristic M-H hystersis loop we just need to plot the magnetisation against the applied magnetic field:

| ![oommf hysteresis loop - M vs H]({{site.baseurl}}/assets/2016/08/2016-07-30-182350_501x517_scrot.png) |
|:--:|
| *oommf hysteresis loop - M vs H* |
