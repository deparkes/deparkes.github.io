---
layout: post
title: How to use OOMMF Oxs_PeriodicRectangularMesh
date: 2014-10-16 14:10:28.000000000 +01:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- OOMMF
tags:
- oommf
- oommf tips
author:
  display_name: deparkes
permalink: "/2014/10/16/use-oommf-oxs_periodicrectangularmesh/"
---
<h1>How to use the OOMMF periodic mesh</h1>
Using the OOMMF periodic mesh (<a href="https://math.nist.gov/oommf/software-12.html">version 1.2a5</a>) is very straightforward.
You can simply replace your exising Oxs_RectangularMesh:
```tcltk
Specify Oxs_RectangularMesh:mesh {
cellsize {4e-9 4e-9 4e-9}
atlas :atlas
}
```

With Oxs_PeriodicRectangularMesh, like so:

```tcltck
Specify Oxs_PeriodicRectangularMesh:mesh {
cellsize {4e-9 4e-9 4e-9}
atlas :atlas
periodic x
}
```
where the additional line
`periodic x`
simply specifies along which direction the periodicity is (in this case <em>x</em>).
If you like this, check out my <a title="OOMMF Tutorial" href="{{site.baseurl}}/oommf/oommf-tutorial/">OOMMF Tutorial</a>.
<div class="attribution-info">
<a class="owner-name truncate" title="Go to Thomas Hawk's photostream" href="https://www.flickr.com/photos/thomashawk/" data-rapid_p="25" data-track="attributionNameClick">Image: Thomas Hawk</a>;</div>
