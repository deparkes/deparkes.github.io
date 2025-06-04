---
layout: post
title: OOMMF Radial Applied Field With Polar Coordinates
date: 2017-04-22 09:39:30.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- applied field
- oommf
- polar coordinates
- radial coordinates
- transformation
author: deparkes
permalink: "/2017/04/22/oommf-applied-field-polar-coordinates/"
---
It is often more useful to think of applied field in terms of polar coordinates - with an angle and a magnitude. By default the Zeeman term in OOMMF takes inputs in cartesian coordinates - i.e. x, y and z components. In many situations this is fine, but there are times when polar coordinates make more sense - perhaps you are investigating the angle of the applied field . In this post I show you how you can represent an applied field in OOMMF using polar coordinates.
Hopefully this simple example will help you get started with using polar coordinates with the applied field in OOMMF.
<a href="https://gist.github.com/deparkes/5b95f547241349617ae71fab6f961e82#file-radial_field_example-mif">Download an example mif file</a> of an applied field defined in terms of polar coordinates (based on OOMMF ellipsoid example).
<h1>Use The Script Zeeman Term</h1>
Rather than using the <a href="https://math.nist.gov/oommf/doc/userguide12b0/userguide/Standard_Oxs_Ext_Child_Clas.html#UZ">'standard' Zeeman term</a>, we can use the <a href="https://math.nist.gov/oommf/doc/userguide12b0/userguide/Standard_Oxs_Ext_Child_Clas.html#SU">script Zeeman</a>. This allows us to point to a function which will define our field. We'll use a function to convert an angle and magnitude into a x, y and z components.
The specify block below tells the Zeeman term to look for a function called 'Radial' (we can call the function pretty much whatever we want):

```
Specify Oxs_ScriptUZeeman [ subst {
	multiplier [expr {0.001/$mu0}]
	script Radial
}]
```

<strong><a href="https://math.nist.gov/oommf/doc/userguide12b0/userguide/Standard_Oxs_Ext_Child_Clas.html#SU">Read more about ScriptUZeeman.</a></strong>
<h1>Define The Radial Field Function</h1>
The script Zeeman term expects a script (called 'Radial' in this example) to define the applied field. We will use that function to convert an angle and magnitude into x,y and z components of the field.

```
proc Radial { x y z } {
	variable theta
	variable magnitude
	set PI [expr {4 * atan(1.)}]
	set Hx [expr $magnitude * cos(($PI/180.)*$theta)]
	set Hy [expr $magnitude * sin(($PI/180.)*$theta)]
    return [list $Hx $Hy 0  0 0 0 ]
}
```

This function will take a our angle 'theta' and magnitude and return a list x, y and z field components (Hx, Hy and Hz). In this simple example I have assumed that the z-component of the field is zero (you could change this by adding a phi angle and changing the <a href="https://keisan.casio.com/exec/system/1359534351">corresponding coordinate tranformations</a>).
<a href="https://math.nist.gov/oommf/doc/userguide12b0/userguide/MIF_2.1.html#par:supportProcs"><strong>Read more about user defined scripts in OOMMF.</strong></a>
This function refers uses '<a href="https://wiki.tcl.tk/1177#pagetocd2a8f675">variable</a>' to refer to variables defined outside of its scope. At the start of the mif file we can set the values of the variables 'theta' and 'magnitude'.

```
set theta 270
set magnitude 500
```

<a href="{{site.baseurl}}/2014/10/28/oommf-tutorial-part-6-oommf-scripting-python/">Read more about using variables in OOMMF</a>.
Examples of outputs for different angles are set out below.

| ![OOMMF Radial Applied Field]({{site.baseurl}}/assets/2017/04/radial_field_output_small.png) |
|:--:|
| *OOMMF Radial Applied Field* |
