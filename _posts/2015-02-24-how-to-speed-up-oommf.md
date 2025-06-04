---
layout: post
title: How to Speed Up OOMMF
date: 2015-02-24 20:16:53.000000000 +00:00
type: post
parent_id: '0'
published: true
password: ''
status: publish
categories:
- Computing
- OOMMF
tags:
- increase speed
- oommf
- oommf guide
- oommf tutorial
- speed up
author: deparkes
permalink: "/2015/02/24/how-to-speed-up-oommf/"
---
OOMMF can be incredibly useful for studying micromagnetic systems. Some calculations, however, can take an incredibly long time.
Check out these tips for how to speed up OOMMF calculations.
<h1>1. Use more (and faster) cores</h1>
This is an easy one. If you need you computation to go faster, use a faster computer. If you have access to HPC facilities, you can probably <a title="OOMMF Tutorial Part 8: OOMMF on HPC" href="{{site.baseurl}}/2015/02/05/oommf-on-hpc/">install OOMMF </a>and use it there.
See my <a title="OOMMF Tutorial Part 5: OOMMF Tips" href="{{site.baseurl}}/2014/10/16/oommf-tutorial-part-5-oommf-tips/">previous post </a>on how much speed increase you can expect by using more cores in OOMMF.
<h1>2. Increase the cell size</h1>
Another easy way to decrease calculation time is to increase the cell size of the simulation. You have to be careful though, as if you increase the cell size too much, you could go beyond the exchange length, which can introduce errors.
See more on simulation cell size <a title="OOMMF Tutorial Part 5: OOMMF Tips" href="{{site.baseurl}}/2014/10/16/oommf-tutorial-part-5-oommf-tips/">here</a>.
<h1>3. Make your calculation dimensions a power of 2</h1>
OOMMF uses <a href="https://en.wikipedia.org/wiki/Fast_Fourier_transform">fast fourier methods </a>for some of its calculations, which means you can speed up calculations by setting the x, y and z dimensions of the simultion region to be a multiple of 2.
<h1>4. Try out different Evolvers</h1>
There are two main evolvers in OOMMF: <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/Standard_Oxs_Ext_Child_Clas.html#EE">Euler </a>and <a href="https://math.nist.gov/oommf/doc/userguide12a5/userguide/Standard_Oxs_Ext_Child_Clas.html#RK">RungeKutta</a>. In many situations the RungeKutta method will be <a href="https://articles.beltoforion.de/article.php?a=runge-kutta_vs_euler&amp;hl=en">faster</a>, so be prepared to use that instead of Euler. Be careful though, as there can be some situations where Euler comes out on top.
<h1>5. Use periodic boundary conditions</h1>
Have a think about the problem you are trying to simulate. Is there anyway you can divide up a larger problem into a periodic mesh? This effectively reduces the volume that you actually need to simulate, which can dramatically decrease simulation times.
Check out my post on <a title="How to use OOMMF Oxs_PeriodicRectangularMesh" href="{{site.baseurl}}/2014/10/16/use-oommf-oxs_periodicrectangularmesh/">periodic boundary conditions in OOMMF</a>.